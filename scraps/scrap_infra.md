# インフラ（ネットワーク、セキュリティ含む）

### [2023-04-18 LocalStack 2.0がリリース](https://www.publickey1.jp/blog/23/awslocalstack_20.html)

- 無料で使えるオープンソース版では、Amazon S3やDynamoDB、AWS Lambdaなど主要なAPIが利用可能
- IAM、ElasticCache、Amazon RDS、Custom DNSなどは有償

### [2023-04-14 DNSにちょっとだけ詳しくなりたい人に贈る少し突っ込んだDNSの話](https://dev.classmethod.jp/articles/devio_day1_dns/)

- DNSマスター大瀧さんの解説

### [2023-04-13 prismatixでのTerraform運用で活用しているツールの紹介](https://dev.classmethod.jp/articles/developersio-day-one-terraform-and-related-tools-utilized-by-prismatix/)

- シングルテナントのためアカウント数がとても多いのでTerraformを使っている
- Atlantisとは、GitHubなどと連携してTerraformのプロビジョニングを自動化する
- tflintとは、Terraformを静的解析するもので、CI/CDツールとも連携が可能
- tfsecとは、Terraformを静的解析し、セキュリティ上の問題を検出するツール
  - ただし、tfsecからTrivyへの以降が推奨されている
- Trivyとは、Dockerイメージで使用されるパッケージや依存関係の脆弱性をスキャンするツールで、Terraformにも対応
- terraform-docsとは、コードのドキュメンテーションを自動生成するツール

### [2023-04-11 AWS / Google Cloud / Azure それぞれの推しサービス](https://dev.classmethod.jp/articles/developersio-day-one-favorite-services-aws-google-cloud-azure/)

### [2023-03-19 個人的 Finch CLI チートシート を作ってみた](https://dev.classmethod.jp/articles/the-finch-cli-cheat-sheet-v0-4-1/)

- Windows使いなので今のところ触る機会がない
- 標準になる可能性も秘めているので、いずれは使うことになるのかも。

### [2022-12-06 Docker on Lima なツールを色々試してみた](https://developers.freee.co.jp/entry/freee-docker-desktop-alternative)

- Docker１強時代の終焉にあたり読む必要がありそう
- とはいえ今のところWindows向けじゃない気も
