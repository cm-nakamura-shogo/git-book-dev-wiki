# terraform

## terraformとは

IaCツールの一つで、HashiCorpにより開発されたオープンソース。

## インストール

exeを落としてPATHを通すのみで良い。インストール不要。

exeは以下からダウンロードする。

- [https://www.terraform.io/downloads](https://www.terraform.io/downloads)

## 基本コマンド

- init: 最初に実行する。そのフォルダで初回のみ必要。


```sh
terraform init
```

- plan: 設定値を確認する。initを1回もしてない場合は、initしてからやる。つ。


```sh
terraform plan
```


- apply: 実際にリソースを作る。途中でyesを入力する必要がある。


```sh
terraform apply
```


- destroy: リソースを消す。途中でyesを入力する必要がある。


```sh
terraform destroy
```

## やった方が良いコマンド

- validate: 文法チェック

```sh
terraform validate
```

- fmt: コード整形

```sh
terraform fmt
```


## 基本的な手順

tfファイルを記述する。いくつかの複数ファイルに分けても良い。相互の参照は自動で行われる。

### 単にS3を作成するだけのサンプル

シンプルには以下のような内容のファイルを`main.tf`などとして作成しておけば良い。


```tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }
  required_version = ">= 1.2.0"
}

provider "aws" {
  profile = "{プロファイル名}"
}

resource "aws_s3_bucket" "sample_bucket" {
  bucket = "dev-sample"
  force_destroy = true
}
```


`terraform {}`はterraformに関する設定が書かれている。

`provider "aws" {}`は認証情報やリージョンなど普段使用するIAMユーザなどと同じ設定を入れることができる。

`resouce "リソース種" "リソースの任意の名前" {}`が実際にリソースを記述する部分である。上記の例はS3バケットの例である。

### 変数を使う場合

`variable "変数名" {}`という記述を用いる。その中で型やデフォルト値も記述可能。


```tf
variable "prefix" {
  type = string
  default = "dev"
}

resource "aws_s3_bucket" "sample_bucket" {
  bucket = "${var.prefix}-sample"
  force_destroy = true
}
```


値を設定したい場合は、以下のようplanやapply時に引数を指定することが可能。


```sh
terraform plan -var 'prefix=sample-dev'
```


またあらかじめ、環境変数として`TF_VAR_prefix`と、`TF_VAR_`を付けた形で定義しておけば、同様のことが可能。


また別の方法として、定義ファイルを以下のように作成して、読み込ませることでも可能。

- 定義ファイルの例(`dev.tfvars`)

```
prefix = "sample-dev"
```

- 実行時(もちろんapplyでも同様の記述)

```sh
terraform plan -var-file=dev.tfvars
```

## 書き方のコツ

### 依存関係順できちんとデプロイする

例えば、bucketとbucket_versioningを作成したい場合、bucket側のattributeを使って、bucket_versioning側のattributeを設定することで、bucket -> bucket_versioningの順で作成される。

```tf
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

## Drift検出

Terraform Cloudを使用すればDrift Detectionが使用可能らしい。(2022-09にGA)

- [Terraform CloudでAWSリソースの手動変更を検出してみる(Drift Detection) | DevelopersIO](https://dev.classmethod.jp/articles/terraform-cloud-drift-detection/)

## 参考記事

- 公式
  - [Query Data with Outputs | Terraform - HashiCorp Learn](https://learn.hashicorp.com/tutorials/terraform/aws-outputs?in=terraform/aws-get-started)
- [10分で理解するTerraform - Qiita](https://qiita.com/Chanmoro/items/55bf0da3aaf37dc26f73)
- [Terraform で変数を使う - Qiita](https://qiita.com/ringo/items/3af1735cd833fb80da75)
- DevIO
  - [Terraformが依存関係を理解できるようにコードを書こう | DevelopersIO](https://dev.classmethod.jp/articles/dependency-in-terraform/)
