## はじめに

AWS CDKはインフラをコードで管理できるものです。

Terraformと同様の位置づけですが、TypeScriptなどのプログラミング言語を使ってリソースをデプロイすることが可能です。またCloudFormationを出力することもできるので、AWSリソースとの相性もよいです。

AWSリソースの仕組みを詳しく知るのにも向いていると思います。

## コンテンツ

- [実践！AWS CDK #1 導入 | DevelopersIO](https://dev.classmethod.jp/articles/cdk-practice-1-introduction/)

## 進め方

実践CDKシリーズをやっておけば間違いないかと思います。

ただしこのシリーズで注意点が２点あります。

- アカウント x リージョン単位で初回に実行が必要なbootstrapの手順が別途必要
- 途中まではCDK v1の処理となっている。
- 抽象クラスなどを使っている点は賛否あり
    - IaCはもう少し宣言的に書いた方が見通しが良くなるという考えがある

bootstrapは以下を参照ください。

- https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html

bootstrapについて知りたい方は以下を参照ください。

- [CDK BootstrapのModern templateで何が変わるのか | DevelopersIO](https://dev.classmethod.jp/articles/cdk-bootstrap-modern-template/#toc-1)
- [CDK Bootstrapをカスタマイズしてみた | DevelopersIO](https://dev.classmethod.jp/articles/customize-bootstrap/)

## 基本的なコマンド

※cdkコマンドはaws-vault経由環境の場合はaws-vault経由で実行ください

- CDKのインストール

```bash
npm install -g aws-cdk
cdk --version # 確認
```

- プロジェクト作成

```bash
mkdir my-cdk-project
cd my-cdk-project
cdk init app --language typescript
```

- 初回（アカウント、リージョン毎に初回のみ）

```bash
cdk bootstrap
```

実行後以下のようなS3バケットが作成されます。

- `arn:aws:s3:::cdk-{何かの記号}-assets-{カウントID}-{リージョン名}`

- リソースの記述

`./lib/`配下にtsファイルが作成されているはずなので、そこにリソースを記述していきます。

```bash
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as s3 from 'aws-cdk-lib/aws-s3';

export class SampleCdk202401Stack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const bucket = new s3.Bucket(this, 'CreateBucket', {
      bucketName: "cm-nakamura-2024-01-03",
      removalPolicy: cdk.RemovalPolicy.DESTROY // デフォルトではdestroyでバケットが消えない
    });
  }
}
```

- Cfnのテンプレート出力

```bash
cdk synth > template.yml
```

ymlファイルにはCDKのメタデータなど様々なものが含まれますが、Resourcesのみを基本確認すればOKです。

余計なものを消したければ以下のようにしてみましょう

```bash
cdk synth --path-metadata false --no-version-reporting > template.yml
```

- デプロイ

```bash
cdk deploy
```

- リソース削除

```bash
cdk destroy
```

あとは実践CDKシリーズをするか、実務に似た演習をしてみてください。