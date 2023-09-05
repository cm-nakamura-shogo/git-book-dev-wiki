# IaC

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
- [2023-07-25「Terraformのデプロイパイプラインに使用できるツールをまとめてみる」というテーマのビデオセッションで話しました #devio2023 | DevelopersIO](https://dev.classmethod.jp/articles/tf-deploy-piepline-video-devio2023/)
- [Terraform（AWS）の構成を公開します – てっくぼっと！](https://blog.applibot.co.jp/2023/08/09/terraform-architecture-for-aws/)
- [Xユーザーの濱田孝治（ハマコー）さん: 「コレすごいなぁ。検証用リソースをterraformで作るとき、積極的に使っていきたい。 / X](https://twitter.com/hamako9999/status/1693852961859154100?s=12&t=0nszgXsDXAd-L4WiCutIWg)
- [Terraformのディレクトリパターン集 - Qiita](https://qiita.com/reireias/items/253529c889cafb3fa4c7)
- [I-2 : 「それ、どこに出しても恥ずかしくないTerraformコードになってるか？」 - YouTube](https://www.youtube.com/watch?v=0IQ4IScqQws)
- [後で楽できるTerraformの書き方（※ただし書くときは辛い） - SMARTCAMP Engineer Blog](https://tech.smartcamp.co.jp/entry/easy-terraform-later)
- [【Terraform】モジュールを利用した際のoutputs.tfの作成](https://rurukblog.com/post/Terraform-module-outputs/)
- [Creating Modules | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/modules/develop)
- [後で楽できるTerraformの書き方（※ただし書くときは辛い） - SMARTCAMP Engineer Blog](https://tech.smartcamp.co.jp/entry/easy-terraform-later)
- [Terraform を使用するためのベスト プラクティス  |  Google Cloud](https://cloud.google.com/docs/terraform/best-practices-for-terraform?hl=ja)
- [実践Terraform　AWSにおけるシステム設計とベストプラクティス | 野村 友規 |本 | 通販 | Amazon](https://www.amazon.co.jp/dp/4844378139/ref=redir_mobile_desktop?_encoding=UTF8&%2AVersion%2A=1&%2Aentries%2A=0)
- [I-2 : 「それ、どこに出しても恥ずかしくないTerraformコードになってるか？」 - YouTube](https://www.youtube.com/watch?v=0IQ4IScqQws)
- [GitHub - terraform-aws-modules/terraform-aws-eventbridge: Terraform module which creates EventBridge resources on AWS 🇺🇦](https://github.com/terraform-aws-modules/terraform-aws-eventbridge)
- [Terraformのmoduleとoutput | DevelopersIO](https://dev.classmethod.jp/articles/terraform%E3%81%AEmodule%E3%81%A8output/)
- [TerragruntでTerraformのbackend周りのコードをDRYにする | DevelopersIO](https://dev.classmethod.jp/articles/terragrunt-makes-your-terraform-backend-code-dry/)
- [Terraform だけだとハードモードなので Terragrunt を使おう - Qiita](https://qiita.com/ssc-ksaitou/items/c3eedd46a5eb04d731cc)
- [Terraformのコンポーネント分割について検討する - Qiita](https://qiita.com/fukubaka0825/items/103c900a4072121bb4ae)
- [Terraform構成をビジュアライズできるツール Pluralithを使ってAWS構成図を自動作成してみる | DevelopersIO](https://dev.classmethod.jp/articles/terraform-visualise-pluralith/#toc-3)
- [Terraform ベストプラクティスを整理してみました。 | DevelopersIO](https://dev.classmethod.jp/articles/terraform-bset-practice-jp/)
- [TerraformでAWSのセキュリティグループのルールを作成する方法の比較と注意点 | DevelopersIO](https://dev.classmethod.jp/articles/terraform-security-group/)