## Terraformとは

IaCツールの一つで、HashiCorpにより開発されたオープンソース。有償サービスのTerraform Cloudもある。AWSやGoogle Cloud、Snowflakeなどのリソースをコード管理できます。

## セットアップ

exeなどの実行ファイルを落としてPATHを通すのみでOKです。インストーラ等は不要なはず。

exeは以下からダウンロードできます。

- https://www.terraform.io/downloads

## 基本的な使い方

tfファイルを記述すればすぐに使用できます。いくつかの複数ファイルに分けてもOKです。

相互の依存関係の考慮は基本的に自動で行われます。

以下は、S3バケットを作成するだけのサンプルです。

こちらを`main.tf`などとして作成しておけばOKです。

```
resource "aws_s3_bucket" "sample_bucket" {
  bucket = "cm-nakamura-sample-2024-01-03"
  force_destroy = true
}
```

`resouce "リソース種" "リソースの任意の名前" {}`が実際に新規リソースを記述する部分です。

以下で初期化します。

以降、aws-vault配下の場合は `aws vault exec {プロファイル名} --`を冒頭に付けてください。

（"The security token included in the request is invalid" というエラーが出る場合は、`aws vault exec {プロファイル名} --no-session --`を付ければ回避できます）

- [https://github.com/99designs/aws-vault/issues/260#issuecomment-397601165](https://github.com/99designs/aws-vault/issues/260#issuecomment-397601165)

```bash
terraform init
```

リソースをデプロイします。マネジメントコンソールからバケットが作成されているか確認してみてください。途中でyesを入力する必要があります。

```bash
terraform apply
```

作成したリソースを破棄します。途中でyesを入力する必要があります。

```bash
terraform destroy
```

## コマンド

### 基本コマンド

次に基本的なコマンドを説明します。

- init: 最初に実行します。そのフォルダで初回または後述のモジュール作成時にのみ必要です。

```
terraform init
```

- plan: 変更点を確認します。applyでも変更点を示した後にユーザの実行を挟みますが、こちらの方が安全です。

```
terraform plan
```

- apply: 実際にリソースを作ります。途中でyesを入力する必要があります。

```
terraform apply
```

- destroy: リソースを消します。途中でyesを入力する必要があります。

```
terraform destroy
```

### 知っておいた方が良いコマンド

- validate: 文法チェック

```
terraform validate
```

- fmt: コード整形

```
terraform fmt
```

## その他の知識

### resourceとdataとは

`resource`と`data`の違いは、新規作成するか既存リソースかどうかの違いです。

### variable: 変数を使う場合

`variable "変数名" {}`という記述をtfファイルに記載します。

その中で型やデフォルト値も記述可能です。

```
variable "prefix" {
  type = string
  default = "dev"
}

resource "aws_s3_bucket" "sample_bucket" {
  bucket = "${var.prefix}-sample"
  force_destroy = true
}
```

値を設定したい場合は、以下のようplanやapply時に引数を指定することが可能です。

```
terraform plan -var 'prefix=sample-dev'
```

またあらかじめ、システムの環境変数として`TF_VAR_prefix`と、`TF_VAR_`を付けた形で定義しておけば、同様のことが可能となります。

また別の方法として、定義ファイルを以下のように作成して、読み込ませることでも可能です。

- 定義ファイルの例(`dev.tfvars`)

```
prefix = "sample-dev"
```

実行時は以下のように指定します。

```
terraform plan -var-file=dev.tfvars
```

### outputの使い方

以下のように記述すると、作成結果の名前を取得できます。

```bash
resource "aws_s3_bucket" "sample_bucket" {
  bucket        = "cm-nakamura-sample-2024-01-03"
  force_destroy = true
}

output "sample_bucket_arn" {
  value = aws_s3_bucket.sample_bucket.arn
}
```

applyをすると以下のような出力が得られます。

```bash
terraform apply

#
# (色々表示されて、ユーザがyesと入力して、作成ログが流れた後...)
#
# Outputs:
# 
# sample_bucket_arn = "arn:aws:s3:::cm-nakamura-sample-2024-01-03"
```

１回applyしておけば、outputで出力値を得ることが可能です。

```bash
terraform output

# sample_bucket_arn = "arn:aws:s3:::cm-nakamura-sample-2024-01-03"
```

S3バケットの場合は実行前にARNは分かりますが、自動で決まる名前（known_applyと表現される）を得たい場合などに役立ちます。

### tfstateの共有

tfstateはデフォルトではローカルに作成されますが、開発者間で共有するには設定が必要です。

一例としてS3バケットで共有する方法を示しておきます。

あらかじめtfstate用のバケットを作成しておき、以下のように`main.tf`に記載します。

```bash
terraform {
  backend "s3" {
    bucket = "cm-nakamura-for-tfstate"
    key    = "terraform.tfstate"
    region = "ap-northeast-1"
  }
}
```

そのうえで`terraform init`を実行すればOKです。

### locals: ローカル変数の使い方

tfファイル内で使うことのできるローカル変数を以下のように作成することが可能です。

```bash
locals {
  bucket_name = "cm-nakamura-sample-2024-01-03"
}

resource "aws_s3_bucket" "sample_bucket" {
  bucket        = local.bucket_name
  force_destroy = true
}
```

localsの中では、他のローカル変数やvariableを参照することが可能です。

```bash
variable "bucket_suffix" {}

locals {
  bucket_prefix = "cm-nakamura-sample"
  bucket_name   = "${local.bucket_prefix}_${var.bucket_suffix}"
}

resource "aws_s3_bucket" "sample_bucket" {
  bucket        = local.bucket_name
  force_destroy = true
}
```

### アカウントIDやデフォルトリージョンを取得する

以下のようにすれば、今有効なAWSプロファイルの情報を取得できます。

```bash
data "aws_caller_identity" "current" {}
data "aws_region" "curent" {}

locals {
  account_id      = data.aws_caller_identity.current.account_id
  region          = data.aws_region.current.name
  repository_name = "sample-image"
  ecr_image_uri   = "${local.account_id}.dkr.ecr.${local.region}.amazonaws.com/${local.repository_name}"
}
```

## モジュール分割

ある程度リソースが増えてくるとモジュール分割の必要性を感じると思います。

どのみちdev、stg、prdなどの環境の使い分けを考えると、最初からベストプラクティスに沿ったフォルダ設計を意識しておいた方が良いので仕組みを理解しておきましょう。

```bash
environments/
  └ dev/
    └ main.tf
  └ stg/
    └ main.tf
modules/
  └ s3/
    └ main.tf
```

`dev/main.tf`は以下のようにモジュールを参照します。

```bash
module s3 {
  source = "../modules/s3"
  bucket_name = "cm-nakamura-2024-01-03"
}

output s3_bucket_arn {
  value = module.s3.sample_bucket_arn
}
```

モジュールの入力（引数のようなもの）は`bucket_name`などのように指定でき、これをモジュール側の`variable`として記載しておく必要があります。

モジュールの出力（戻り値のようなもの）は`module.{モジュール名}.{モジュールのアウトプット名}`で呼び出し元から参照できます。

つまり、`modules/s3/main.tf`は以下のように記載します。

```bash
variable bucket_name {}

resource "aws_s3_bucket" "sample_bucket" {
  bucket        = var.bucket_name
  force_destroy = true
}

output "sample_bucket_arn" {
  value = aws_s3_bucket.sample_bucket.arn
}
```

variableは`variables.tf`に、outputは`outputs.tf`にそれぞれ記載することもあります。

以下も参考にされてください。

- module入門
    - [terraform_module_ Beginner - Speaker Deck](https://speakerdeck.com/yonasou/terraform-module-beginner)
- [[Terraform]Moduleを作ると環境毎のデプロイが便利 | DevelopersIO](https://dev.classmethod.jp/articles/terraform-deploy-module/)
- [後で楽できるTerraformの書き方（※ただし書くときは辛い） - SMARTCAMP Engineer Blog](https://tech.smartcamp.co.jp/entry/easy-terraform-later)

## その他ノウハウ

### depend_onを使うと依存関係を明示的に指定可能

基本的にはTerraformが自動でお互いの参照関係を用いて依存関係を解決しますが、明示的にリソースのattributeとしてdepend_onを指定すれば、依存関係順にデプロイすることができます。

### 依存関係順できちんとデプロイ

先ほどと関連するのですが、自動できちんと依存関係を考慮してくれるような工夫が必要です。

例えば、bucketとbucket_versioningを作成したい場合、bucket側のattributeを使って、bucket_versioning側のattributeを設定することで、bucket -> bucket_versioningの順で作成されます。

```
locals {
  bucket_name = "kazue-hogehoge"
}

resource "aws_s3_bucket" "sample" {
  bucket = local.bucket_name
}

resource "aws_s3_bucket_versioning" "sample" {
  bucket = aws_s3_bucket.sample.bucket
  versioning_configuration {
    status = "Enabled"
  }
}

```

### Drift検出

Terraform Cloudを使用すればDrift Detectionが使用可能らしいです。(2022-09にGA)

- [Terraform CloudでAWSリソースの手動変更を検出してみる(Drift Detection) | DevelopersIO](https://dev.classmethod.jp/articles/terraform-cloud-drift-detection/)

### aws_iam_policy_attachmentは使用しない方がよい

似たようなリソース名があるのですが、aws_iam_policy_attachmentは使用しないようにご注意ください。既存の紐づけ済みのIAMエンティティ(user, group, role)からポリシーが剥がれてしまうことがあるようです。

代わりに、以下それぞれのエンティティに対応したものを使用します。

- aws_iam_user_policy_attachment
- aws_iam_group_policy_attachment
- aws_iam_role_policy_attachment

参考

- [terraform の aws_iam_policy_attachment は使わないほうが無難 - Qiita](https://qiita.com/bilzard/items/8b54c40351e2ff39afa0)

## 参考記事

- 公式
    - [Query Data with Outputs | Terraform - HashiCorp Learn](https://learn.hashicorp.com/tutorials/terraform/aws-outputs?in=terraform/aws-get-started)
- その他
    - [10分で理解するTerraform - Qiita](https://qiita.com/Chanmoro/items/55bf0da3aaf37dc26f73)
    - [Terraform で変数を使う - Qiita](https://qiita.com/ringo/items/3af1735cd833fb80da75)
- DevIO
    - [Terraformが依存関係を理解できるようにコードを書こう | DevelopersIO](https://dev.classmethod.jp/articles/dependency-in-terraform/)
    - [Terraformのデプロイパイプラインに使用できるツールをまとめてみた | DevelopersIO](https://dev.classmethod.jp/articles/terraform-deploy-pipeline-tool)
        - 非常によくメリット・デメリットがまとまっていてよい。