# smilesolar-cs

契約者登録フォーム（フロントエンド）。

- 公開URL（想定）: https://unfinished-llc.com/smilesolar-cs/
- 実体: [index.html](index.html)（単一HTML。送信先はGASウェブアプリ）
- ホスティング: お名前.com RSサーバー（`main` への push で GitHub Actions が FTP 自動デプロイ）

## デプロイの仕組み

`main` ブランチに push すると [.github/workflows/deploy.yml](.github/workflows/deploy.yml) が動き、
`index.html` をFTPでサーバーの公開ディレクトリへアップロードします。

### 必要な GitHub Secrets

リポジトリの **Settings → Secrets and variables → Actions** に以下を登録してください。

| Secret 名 | 内容 | 例 |
|---|---|---|
| `FTP_SERVER` | RSのFTPホスト名 | `ftp.onamae.ne.jp` |
| `FTP_USERNAME` | FTPユーザー名 | RS管理画面で発行 |
| `FTP_PASSWORD` | FTPパスワード | RS管理画面で発行 |
| `FTP_SERVER_DIR` | 公開ディレクトリ（末尾スラッシュ必須） | `/public_html/smilesolar-cs/` |

> `FTP_SERVER_DIR` の正確なパスはRSの構成により異なります。`unfinished-llc.com/smilesolar-cs/` で
> 開けるよう、ドメインの公開領域配下に `smilesolar-cs/` を含めて指定してください。

> ⚠️ お名前.com RS が **FTPS/SFTP のみ**の場合は `deploy.yml` の `protocol` 調整が必要です
> （FTPS: `protocol: ftps` / SFTPはこのアクション非対応のため別手段）。

## 補足
- フォームの送信先（GASウェブアプリURL）は `index.html` 内に設定済み。
- バックエンド（スプレッドシート追記・ドライブ自動フォルダ作成のGASコード等）は
  社内資料のため本リポジトリには含めていません。
