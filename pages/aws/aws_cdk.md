# AWS CDK

## 最初の一歩

### install

```
npm install -g aws-cdk
cdk --version
```

### create project

```
cd my-cdk-project
cdk init app --language typescript
```

### 編集

- さしあたり./lib/sample-cdk-stack.tsを編集していく

### synth

- Cfnのyamlを出力できる。同時に./cdk.outに色々生成される。

```
cdk synth
```

### bootstrap

- まずは使用するprofileをaws cliに設定する。

- wslなどであれば

```
$ export AWS_PROFILE={プロファイル名}
```

- powershellであれば

```
> $env:AWS_PROFILE = "cm-nakamura-test-mlflow"
```

- bootstrap時に必要なIAMポリシーは以下

```
IAMFullAccess
AmazonS3FullAccess
AmazonSSMFullAccess
AmazonEC2ContainerRegistryPowerUser
AWSCloudFormationFullAccess
```

- SSM, ECR, IAMはModern版bootstrapで追加されたもの。
- 詳細は下記参照
  - [CDK BootstrapのModern templateで何が変わるのか | DevelopersIO](https://dev.classmethod.jp/articles/cdk-bootstrap-modern-template/)

- bootstrapをすると、CDKToolkitとしてCloud Formationにスタックが作成される。

- 公式ドキュメントは以下を参照。
  - https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html

```
cdk bootstrap
```

bootstrapをカスタマイズすることも可能らしい。

- 参考記事
  - [CDK Bootstrapをカスタマイズしてみた | DevelopersIO](https://dev.classmethod.jp/articles/customize-bootstrap/)

### deploy

```
cdk deploy
```

## [実践！AWS CDK #1 導入](https://dev.classmethod.jp/articles/cdk-practice-1-introduction/)

- CDKではConstructが３つのレイヤに分けられている。

- L3: Patterns
  - 複数のリソースを含む構成パターンを事前定義したもの
- L2: High-level constructs
  - デフォルト値や便利なメソッドを定義した AWS リソースを表すクラス
- L1: Low-level constructs
  - CFn リソースおよびプロパティと 1:1 で対応

- L2ではベストプラクティスに沿うため、記述した以上のリソースが作成される。
- 勉強時はL1で組み立てる（生のCfnに近い）。
- L1は頭にCfnと付いているようだ。(ex. CfnVpc)

## [実践！AWS CDK #2 VPC](https://dev.classmethod.jp/articles/cdk-practice-2-vpc/)

- CfnVPCを使った構築。

## [実践！AWS CDK #3 テスト](https://dev.classmethod.jp/articles/cdk-practice-3-test/)

- 3つの種類
  - Snapshot tests
    - ベースラインとの差分を比較するテスト。L2を使う場合には意図しない変更がないか確認できる。
    - 差分があるとfailedになる、かつL1を扱うので、この記事ではやっていない。
  - Fine-grained assertions
    - 以下のような項目をチェックできます。この記事で扱っている。
      - どんなリソースがあるか
      - リソースのプロパティ
      - リソースの数
      - 出力（Outputs）の内容
  - Validation tests
    - 単体テストのようなイメージ。複雑なConstructを使用する場合に使う。

- ./test配下に.test.tsという拡張子を付けてシナリオを記述するみたい。
- 以下は要注意かも。

> haveResource メソッドや countResources メソッドの第一引数にはリソースタイプを string 型で指定します。ここに指定すべき文字列は CFn でサポートされている リソースタイプ識別子 となります。 これらが string 型となっていることから予想できますが、プロパティ部分に関しては IDE の補完が効きません。またここで指定すべきプロパティのキー値は CFn のドキュメントに書かれているもの となります。具体的に言うと CfnVPCProps の cidrBlock は無効であり、AWS::EC2::VPC の CidrBlock（先頭大文字！）が有効な値となるのでご注意ください。テスト時は生成された CFn のテンプレートと比較を行っているので、CFn の仕様が正となります。

- 要は、コード側はPropsに沿って書けるけど、テストコードは先頭を大文字にしたうえで確認プロパティをIDE補完無しで書く必要がある。

## [実践！AWS CDK #4 Context](https://dev.classmethod.jp/articles/cdk-practice-4-context/)

- ContextはCFnのパラメータみたいなもの。
- キーと値のペアで与え、どちらもstring
- CfnParameterというものもあるが、こちらは非推奨でcdk synth実行時に値が取得できない。
- 与える方法は複数ある。
  - 現在の AWS アカウントから自動的に
  - CDK コマンドの --context オプション
  - プロジェクトの cdk.context.json ファイル
  - プロジェクトの cdk.json ファイル
  - ~/.cdk.json ファイルの context キー
  - construct.node.setContext メソッド
- 記事では、以下の使い方
  - デフォルト値には、cdk.jsonを使う。
  - それ以外は--contextまたは-cで与える。(実行時に与える方が優先)
- 注意点として、テスト実行時は値が取得できないので、それを見越してundefinedで埋める。

## [実践！AWS CDK #5 サブネット](https://dev.classmethod.jp/articles/cdk-practice-5-subnet/)

- Subnetを作成する。
- CDKでもIntrinsic Functionがあるが、これをやる場合testができなくなる点が注意。

```ts
import { Fn } from 'aws-cdk-lib';

export class SampleCdkStack extends Stack {
  constructor(scope: Construct, id: string, props?: StackProps) {
    super(scope, id, props);

    const subnet = new CfnSubnet(this, 'subnet', {
      cidrBlock: '10.0.11.0/24',
      vpcId: vpc.ref,
      availabilityZone: Fn.select(0, Fn.getAzs("")),
      tags: [
        { key: 'Name', value: `${systemName}-${envType}-subnet-public-1`}
      ]
    })
```

- 記事では、上記のAZ部分は普通に文字列で記述。
- cdk diffで、デプロイ済みのバージョンと現在の構成を比較できる。

## [実践！AWS CDK #6 Metadata](https://dev.classmethod.jp/articles/cdk-practice-6-metadata/)

- MetadataとはCFnのテンプレートセクションの一つ。
- 任意項目なので無くても良い。何を入れても良い。
- 以下のような特殊なMetadataも存在する。
  - AWS::CloudFormation::Authentication
  - AWS::CloudFormation::Init
  - AWS::CloudFormation::Interface
- CDKではこのMetadataが自動で付与され、さらに別にAWS::CDK::Metadataというリソースが含まれる。
- これはAWS CDKの改善に使用される情報のようです。
- 記述は以下でオフにすることができる。

```cdk.json
{
  "versionReporting": false,
}
```

- ただ各リソースのmetadataはこれでもオフにできないため、最終は以下のようにする。

```
cdk synth --no-version-reporting --path-metadata false
```

- package.jsonにこう書けば省略できる。

```json
{
  // ...
  "scripts": {
    // ...
    "synth": "cdk synth --path-metadata false --no-version-reporting > cfn.yaml"
  },
  // ...
}
```

## [実践！AWS CDK #7 ファイル分割](https://dev.classmethod.jp/articles/cdk-practice-7-split-file/)

- コードを読みやすくするためファイルの分割をしていく。
- これはCDKというより一般的なJavaScriptの勉強みたいな部分がある。

## [実践！AWS CDK #8 抽象化](https://dev.classmethod.jp/articles/cdk-practice-8-abstraction/)

- 同上。抽象クラスを使う。

## [実践！AWS CDK #9 リファクタリング](https://dev.classmethod.jp/articles/cdk-practice-9-refactoring/)

- 同上。処理の共通化。

## 補足: tsconfig.jsonやcdk.jsonのチューニング

- tsconfig.jsonのbuild時の出力先を設定して、build時の入力を設定する(build出力先を見に行かないように制限)。

```json
{
  "compilerOptions": {
    // ...
    "outDir": "dist",
  },
  "include": [
    "lib",
    "test",
    "bin"
  ],
  // ...
}
```

- tsconfig.jsonのbaseUrlを編集して、cdk.jsonのts-nodeコマンドも修正する。

```json
{
  "compilerOptions": {
    // ...
    "baseUrl": "./",
  },
  // ...
}
```

- cdkはこんな感じで、tsconfig-pathsのオプションを追加。

```json
{
  "app": "npx ts-node -r tsconfig-paths/register --prefer-ts-exts bin/sample-cdk.ts",
  // ...
}
```
- 以下が情報元
  - [CDK(TypeScript)のimport文で絶対パスを使用する | DevelopersIO](https://dev.classmethod.jp/articles/cdk-typescript-absolute-path-import/)

- 加えてjest.config.jsに以下を設定するとjestも絶対パスで動作させることができる

```js
module.exports = {
  // ...
  moduleDirectories: ['node_modules', '.']
};
```

- この情報源は以下。
  - [typescript — Jest + TypeScript +絶対パス（baseUrl）でエラーが発生する：モジュールが見つかりません](https://www.web-dev-qa-db-ja.com/ja/typescript/jest-typescript-%E7%B5%B6%E5%AF%BE%E3%83%91%E3%82%B9%EF%BC%88baseurl%EF%BC%89%E3%81%A7%E3%82%A8%E3%83%A9%E3%83%BC%E3%81%8C%E7%99%BA%E7%94%9F%E3%81%99%E3%82%8B%EF%BC%9A%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%8C%E8%A6%8B%E3%81%A4%E3%81%8B%E3%82%8A%E3%81%BE%E3%81%9B%E3%82%93/839007256/)

## [実践！AWS CDK #10 インターネットゲートウェイ | DevelopersIO](https://dev.classmethod.jp/articles/cdk-practice-10-internet-gateway/)

- IGWとVPCにアタッチするためのVPCGatewayAttachmentを使う。
- VPCGatewayAttachmentはアタッチにしか使わないので、IGWのクラス外には出していないようだ。

## [実践！AWS CDK #11 Elastic IP](https://dev.classmethod.jp/articles/cdk-practice-11-elastic-ip/)

- NATゲートウェイ用なので、少し構成を変えてNATゲートウェイ用の中でEIP作成した。
- ので次と同時に実装。

## [実践！AWS CDK #12 NAT ゲートウェイ](https://dev.classmethod.jp/articles/cdk-practice-12-nat-gateway/)

- 同上。
- NATGWは、2台で1日$2.83くらいかかるので要注意。

## [実践！AWS CDK #13 ルートテーブル](https://dev.classmethod.jp/articles/cdk-practice-13-route-table/)

- ルートテーブルを作成し（作成時にVpcIdを指定）、ルートを作成。
- その後Subnetとルートテーブルを関連付ける。
- ここで気づいたことがあるが、VPC作成時点で、メインルートテーブルが作成されており、それとは別にルートテーブルを追加していく。
  - これをカスタムルートテーブルと呼ぶ。
- Subnetを作成した場合、デフォルトではメインルートテーブルに関連付けられている。
  - これを明示的にカスタムルートテーブルに関連付けた場合は、変更される。
  - 複数のルートテーブルをSubnetに関連付けすることはできない。
- メインルートテーブルも、カスタムルートテーブルも以下のルートは作成時に自動で設定される。
  - 送信先: VPC内のCIDR、ターゲット: local
- ちなみにルートはロンゲストマッチであるため、サブネットマスクが長い方が優先される。
- ここまでの話は、NACLについても同様みたい。
- あとは、testコードのanything便利そう。

## [実践！AWS CDK #14 ネットワーク ACL](https://dev.classmethod.jp/articles/cdk-practice-14-network-acl/)

- ルートテーブルとほぼ同じ。デフォルトのNACLはVPCのメインネットワークACLとなっている。
- Subnetを作成した場合、デフォルトではメインネットワークACLに関連付けられている。
- メインネットワークACLはinbound/outbound共に以下のルールとなっている。
```
ルール番号 タイプ               プロトコル ポート範囲 送信元/送信元 許可/拒否
100        すべてのトラフィック すべて     すべて     0.0.0.0/0     Allow
*          すべてのトラフィック すべて     すべて     0.0.0.0/0     Deny
```
- カスタムなNACLも*のルールは自動で付与されるので、100に相当するEntryのみ記事では作成している。
- またすべてのプロトコルは-1を指定すればよい。

## [実践！AWS CDK #15 IAM ロール](https://dev.classmethod.jp/articles/cdk-practice-15-iam-role/)

- IAMロールを作成している。
- PolicyDocumentはPolicyDocument.fromJsonを使った方が楽そうなのでこちらを採用。
- EC2にはSession Managerからアクセスするので、`AmazonSSMManagedInstanceCore`をポリシーとしている。
- RDSには拡張モニタリング用に`AmazonRDSEnhancedMonitoringRole`をポリシーとしている。
- 実装は少し面倒だったので、今回からべた書き風にした。。。
- テスト時に自動でPolicyDocumentにVersionが付与されるため、部分一致のテストコードとして`haveResourceLike`を使用している。
- EC2に与えるロールは、CfnInstanceProfileがコンテナとして必要なので注意する。
  - 普段意識しないが、よく見たらマネコン画面でもロールを選択するとインスタンスプロファイルのことが書いてあるようだ。
>IAM ロールを作成したあとは CfnInstanceProfile クラスを利用し EC2 のインスタンスプロファイルも作成しています。
インスタンスプロファイルとは IAM ロールをインスタンスに渡すためのコンテナ だそうです。マネジメントコンソールで EC2 の IAM ロールを作成するときは IAM ロールと同じ名前でこのインスタンスプロファイルが作成されるため、普段は意識する必要はありません。しかし今回のように手動で IAM ロールを作成する場合はインスタンスプロファイルも作る必要があります

## [実践！AWS CDK #16 セキュリティグループ](https://dev.classmethod.jp/articles/cdk-practice-16-security-group/)

- SecurityGroupはCfnと同様、ルールを別リソースにするか、SecurityGroupのプロパティで与えるか２つ方法がある。
- 各ルールの割り当ては以下のように行う。
  - 別リソースの場合
    - GroupIdで紐づけるSecurityGroupを指定
    - 複数ある場合は都度リソースを作って紐づける
  - プロパティ指定の場合
    - リストでプロパティに与える。
    - 複数ある場合はリストに追加するだけでよい。
    - 単独の場合もリストにする必要があるので忘れがちな点に注意。
- ここはちょっと記事から離れた実装をトライしてみた。
  - propsを関数化する、なるべく定義済みのpropsの型を使う。
  - 元実装では、定義済みの型と同じような型を定義するのがつらかった。
  - これにより、記事では別リソースだが、SecurityGroupのプロパティでの実装に対応できた。
- ルールについて
  - ソースはCIDRおよびsgを指定できる。
  - ToPortとFromPortを違うように設定できるが、その場合どうなるのだろう？？
- SG自体は、NACLやRouteTableと同様VPCに属する。
- RouteTableやNACLと同様VPCにデフォルトのSGがある。
  - インバウンドは同一SGからすべてを許可
  - アウトバウンドは0.0.0.0/0にすべて許可

## [実践！AWS CDK #17 EC2](https://dev.classmethod.jp/articles/cdk-practice-17-ec2/)

- EC2はsubnetに対して割り当てる。
- SSMでのアクセス失敗。NATGWを落としていたせいかも。
  - 基本はNATGWが必要。
  - それが嫌な場合は、VPCエンドポイントを使えば行けるようだ。
  - [セッションマネージャーでEC2に接続できない時に確認した点](https://dev.classmethod.jp/articles/session-manageer-confirmation-item/)

## [実践！AWS CDK #18 ALB](https://dev.classmethod.jp/articles/cdk-practice-18-alb/)

- プロパティについて
  - ipAddressType
    - v4かv4,v6のdualを選択。基本v4でOK
  - name
    - 名前
  - scheme
    - internalかinternet-facingを指定。internet-facingの場合public IPが付与される。
    - なお、gateway loadbalancerの場合はこのschemeは指定不可。
  - securityGroups
    - セキュリティグループ。複数指定可能なのでリストで渡す。
  - subnets
    - subnetを指定する。AZ毎に１つのsubnetしか指定できない。
    - 似たプロパティとしてSubnetMappingsがあり、こちらはEIPで指定するで両方は使えない。
  - type
    - application | gateway | networkを指定できる。CLBはたぶん別クラス。
- LBのターゲットとして、targetGroupが必要
  - name
    - 名前
  - port
    - ターゲットが受信するポート。登録時にoverrideされない場合はこちらが使用される。
    - GENEVE(GLB)の場合、6081がポートとなる。
    - lambdaがターゲットの場合、このポートは使用されない。
  - protocol
    - GENEVE | HTTP | HTTPS | TCP | TCP_UDP | TLS | UDP から選択。
    - ALBでは、HTTP | HTTPS
    - NLBでは、TCP | TCP_UDP | TLS | UDP
    - GLBでは、GENEVEが選択可能。
    - lambdaがターゲットの場合、この設定は使用されない。
  - TargetType
    - alb | instance | ip | lambda から選択。
  - VpcId
    - lambda以外の場合はこちらの指定が必要。
- 関連付けるために、Listenerも必要となる。
  - loadBalancerArn
    - albのrefで良いみたい。
  - port
  - protocol
  - defaultActions
    - デフォルトのアクションを設定する。
    - Actionは、forward, fixed-response, or redirectから選択する。
    - 条件に応じてtargetを変更する場合はListenerRuleを使用して、ListenerRuleで、ListenerArnを関連付ける。
  - テスト等はEC2の作成と一緒にやる。

- ユーザーデータの例が見れたのは良かった。
  - 普通にプロパティにbase64で指定する。

```
userData: fs.readFileSync(Ec2.userDataFilePath, 'base64')
```

- ただしユーザーデータは、updateでは反映してくれないので、EC2インスタンスをコメントアウトして、deploy２回やるなどの対応が必要。

## [実践！AWS CDK #19 Secrets Manager](https://dev.classmethod.jp/articles/cdk-practice-19-secrets-manager/)

- プロパティ名などが結構理解できなかった（いまだによくわからない）。
- とりあえずgenerateSecretStringにより、自動的に生成ができるということ。
- そしてそれが２パターンある。
- 以下はユーザー名とパスワードが作成され、パスワードが自動生成される。

```ts
generateSecretString: {
  excludeCharacters: '"@/\\\'',
  generateStringKey: "password",
  passwordLength: 16,
  secretStringTemplate: {"username": "admin"},
}
```

- ユーザー名が不要な場合は、secretStringTemplateを空で渡せばよい。

```ts
  generateSecretString: {
    excludeCharacters: '"@/\\\'',
    generateStringKey: "password",
    passwordLength: 16,
    secretStringTemplate: {},
  }
```

- このsecretStringTemplateという名前の意味が分かってないが、ユースケースとしてはこの２種類っぽい。
- これにより、以下のようなダイナミック参照が可能となる。

```ts
  public static getDynamicReference(secret: CfnSecret, secretKey: SecretKey): string {
    return `{{resolve:secretsmanager:${secret.ref}:SecretString:${secretKey}}}`;
  }
```

- enumは使わない方が良いみたい。
  - [さようなら、TypeScript enum | Kabuku Developers Blog](https://www.kabuku.co.jp/developers/good-bye-typescript-enum)

## [実践！AWS CDK #20～#23 RDS関連]

- これらはまとめてやりました。
- 必要なものが複数ある。
  - SubnetGroup ... RDSを設置するSubnet(AZ)を決めるために必要。
  - ParameterGroup ... DBインスタンス用のパラメータ。たくさんあるのでデフォルトから変更したいもののみ修正する。
  - ClusterParameterGroup ... DBクラスター用のパラメータ。たくさんあるのでデフォルトから変更したいもののみ修正する。
  - Cluster ... DBクラスター
  - Instance ... DBインスタンス

- CfnDdInstanceは、RDS意外にも同名のものがneptuneなどにもあるので、import間違いには気を付ける。
- IAMロールを参照するには、refではなくきちんとattArnを使う必要があるので注意
  - EC2インスタンスのInstanceProfileのときは、ref参照で行けたが、これには気を付けた方がよさそう。
  - 以下がInstanceProfile
  ```yaml
    InstanceProfileEc2:
      Type: AWS::IAM::InstanceProfile
      Properties:
        Roles:
          - Ref: RoleEc2
  ```
  - 以下はRds
  ```yaml
    RdsDbInstance1a:
      Type: AWS::RDS::DBInstance
      Properties:
        # ...
        MonitoringRoleArn:
          Fn::GetAtt:
            - RoleRds
            - Arn
  ```

- instancetypeは`t3.small`に変更
  - 対応タイプは以下の通り。`t2.micro`にしたら怒られた。
    - [Aurora DB instance classes - Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.DBInstanceClass.html)
- auroraの場合、Performance InsightはR系のインスタンスでしか使えないようだ。
  - [AWSのサポートも間違えるのPerformance insightsの注意点 - 片岡空の上の空](https://katawo.hatenablog.com/entry/2019/04/10/120940)
- なのでPerformance Insightは無効化してみる。以下の通りにpropsを無効化すればOK。

```json
    const commonProps = {
      // ...
      // enablePerformanceInsights: false,
      // performanceInsightsRetentionPeriod: 7,
      // ...
    }
```

- EC2のmysqlインストールはGPG keyのエラーがでたため以下を追記必要

```sh
$ sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```

- 接続はできたものの実際にはクラスターエンドポイントが不明なので、どうにかしてEC2に情報を渡す必要がありそう。

## [実践！AWS CDK #24 デバッグ](https://dev.classmethod.jp/articles/cdk-practice-24-debug/)

- こちらは読むだけにとどめました

## [実践！AWS CDK #25 Session Manager で SSH 接続](https://dev.classmethod.jp/articles/cdk-practice-25-session-manager-ssh/)

- 以下にしたがってインストールする。
  - [https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html#install-plugin-windows](https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html#install-plugin-windows)

- ProxyCommandはWindowsの場合は以下でできた。
  - `C:\Users\nakamura.shogo\.ssh\config`を以下のように編集する
  ```
  Host i-* mi-*
      ProxyCommand aws ssm start-session --target %h --document-name AWS-StartSSHSession --parameters "portNumber=%p" --profile your-profile
  ```
  - あとは以下でOK
  ```
  ssh -i .\cdkpractice-stg-key-pair.pem ec2-user@i-0369b219f667e42dc
  ```

- OpenSSHのバージョンによっては、awsをフルパスで書いたり、pemファイルを`C:\Users\nakamura.shogo\.ssh`配下に置かないとダメだったりすることもあるみたい。
  - [Windwos10でssh ProxyCommandの多段SSHの設定 - suzu6の技術ブログ](https://www.suzu6.net/posts/205-ssh-config-proxycommand-windows10/)

- 踏み台にしてWindowsインスタンスにRDPで接続するなど、いろいろできるみたい
  - [AWS Systems Manager セッションマネージャーで Windows 10 でSSH・SCPしてみた | DevelopersIO](https://dev.classmethod.jp/articles/ssm-session-manager-support-for-tunneling-ssh-scp-on-windows10/#toc-10)

## 参考記事

### CDKでLambda関数のビルド

nodejsの場合ビルドには通常、Docker Desktop上のesbuildを使用するらしい。ローカルのesbuildを使うようにする場合は以下の記事を参考にする。

- [AWS CDKでDocker Desktopを使わずにLambda関数（aws_lambda_nodejs）をローカルビルドする | DevelopersIO](https://dev.classmethod.jp/articles/local-build-a-lambda-function-nodejs-without-docker-desktop-with-aws-cdk/)


### [[AWS CDK] Bootstrap リソースのカスタマイズ（修飾子 `hnb659fds` の変更）をしてみた | DevelopersIO](https://dev.classmethod.jp/articles/changing-the-aws-cdk-bootstrap-environment-from-the-default-qualifier-hnb659fds/)

### [2023-05-20 3年間運用したCDKの失敗から学ぶCDK開発のプラクティス | ドクセル](https://www.docswell.com/s/integrated1453/5GXL7N-AWS-CDK-Conference-Japan-2023)

- CDK使う場合に読んでおいた方がいい
