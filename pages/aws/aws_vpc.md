# Amazon VPC

基本となる仮想ネットワーク。Virtual Private Cloudの略

### ルートテーブル(サブネットルートテーブル)

基本はサブネットに関連付けて以下のように使用する。

- VPC作成時点でメインルートテーブルが作成され、作成したものはカスタムルートテーブルとなる。
- カスタムルートテーブルは、VPCに関連付けて作成する。
- サブネットとの関連付けには、`SubnetRouteTableAssociation`という普段意識しないリソースを使用。
- サブネットはデフォルトでメインルートテーブルに関連付けされているが、カスタムルートテーブル関連付けた場合は解除される。
  - つまり、サブネットには一つのルートテーブルしか関連付けできない。

### ルート

- メインルートテーブルも、カスタムルートテーブルも以下のルートは作成時に自動で設定される。
  - 送信先: {VPC内のCIDR}、ターゲット: local
- カスタムで設定例する例としては以下。
  - 送信先: 0.0.0.0/0、ターゲット: IGW
  - 送信先: 0.0.0.0/0、ターゲット: NATGW
- ルートはロンゲストマッチであるため、サブネットマスクが長い方が優先される。
  - サブネットマスクが長い == 左側の固定部分が長い奴のこと
  - つまり以下が設定されいている場合、VPC内のIPはlocalに送信され、それ以外はIGWに送信される。
    - 送信先: {VPC内のCIDR}、ターゲット: local
    - 送信先: 0.0.0.0/0、ターゲット: IGW

### ゲートウェイルートテーブル

IGWおよびVGWに関連付けられたルートテーブル。関連付けには、エッジアソシエーションを使用する(リソースだと`GatewayRouteTableAssociation`)。

ゲートウェイルートテーブルには以下の制限がある。

- 送信先として指定できるのはVPCのCIDRの範囲内のみ
- ターゲットに指定できるのは「local」か「ネットワークインタフェース」のみ
- 「ルート伝達」が有効であってはならない

ゲートウェイルートテーブルによって、VPCへのインバウンドを細かくルーティング可能。(2019-12に発表)

これにより、元々は  送信先: {VPC内のCIDR}、ターゲット: local  しか設定できなかったものが、細かく指定可能となり、IDSなどでインターセプトすることが容易にできるようになっている。

IDSが動作するEC2ではIPフォワードを有効にし、EC2パラメータでデフォルトで有効になっている「送信先/送信元チェック」を外しておく必要がある。

- 参考記事
  - [VPC Ingress Routingとは何かを噛み砕いて理解してみる | DevelopersIO](https://dev.classmethod.jp/articles/what-is-vpc-ingress-routing/)

### トランジットゲートウェイルートテーブル

Transit Gatewayを使用する際のVPC側ではなく、Transit Gateway側に関連付けるルートテーブル。

### ローカルゲートウェイルートテーブル

Outpostsを利用する際のローカルゲートウェイに関連づけるルートテーブル


### インターネットゲートウェイ

Ingressな通信は、クライアントからのアクセス時に、NATテーブルに基づいてPublic IPをPrivate IPに変換する。


### VPC Reachability Analyzer

ネットワークが目的通りに設定されているか確認するためのツール

- [新機能 – VPC Reachability Analyzer | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/new-vpc-insights-analyzes-reachability-and-visibility-in-vpcs/)

### AWS Transit Geteway

多数のVPC接続を管理できる。VPC Peeringなどで複雑になる場合は、Transit Gatewayを利用する。
これによりハブ・アンド・スポークス構成を使用できる。

## 参考記事

### [2022-08-07 Amazon VPCを「これでもか！」というくらい丁寧に解説 - Qiita](https://qiita.com/c60evaporator/items/2f24d4796202e8b06a77)

### [2022-08-14 【ベストプラクティス】Amazon VPC の構築方法を分かりやすく解説 - Qiita](https://qiita.com/c60evaporator/items/b9e645b96afa3a34f41e)
