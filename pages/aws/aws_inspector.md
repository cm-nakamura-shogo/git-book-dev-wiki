# Amazon Inspector

## アップデート

### [Amazon Inspector で AWS Lambda コードスキャンがプレビュー利用出来るように](https://dev.classmethod.jp/articles/code-scans-lambda-functions-amazon-inspector/)

以下のような違いがある。

- Amazon Inspector Lambda 標準スキャン（デフォルト）
  - コードとレイヤーで脆弱性のあるパッケージが使用されているかスキャン
- Amazon Inspector Lambda コードスキャン
  - カスタムコードをセキュリティベストプラクティス（CodeGuru Detector）に基づいてスキャン
