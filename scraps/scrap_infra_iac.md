# Container

## Books

## Articles

- [2023-04-13 prismatixでのTerraform運用で活用しているツールの紹介](https://dev.classmethod.jp/articles/developersio-day-one-terraform-and-related-tools-utilized-by-prismatix/)
  - シングルテナントのためアカウント数がとても多いのでTerraformを使っている
  - Atlantisとは、GitHubなどと連携してTerraformのプロビジョニングを自動化する
  - tflintとは、Terraformを静的解析するもので、CI/CDツールとも連携が可能
  - tfsecとは、Terraformを静的解析し、セキュリティ上の問題を検出するツール
    - ただし、tfsecからTrivyへの以降が推奨されている
  - Trivyとは、Dockerイメージで使用されるパッケージや依存関係の脆弱性をスキャンするツールで、Terraformにも対応
  - terraform-docsとは、コードのドキュメンテーションを自動生成するツール