# S3

## S3概要

### ストレージの種類

- S3はオブジェクトストレージとなる。
  - 安価かつ高い耐久性

- その他には以下がある。
  - ブロックストレージ
    - EBS, インスタンスストア
  - ファイルストレージ
    - EFS

### S3とは

- Simple Storage Service

- 特徴
  - 容量制限なく保存可能なマネージド型
  - 月額1GB/約2.5円
  - 高い耐久性 99.999999999%(eleven nine)
  - 冗長化
  - データ容量に依存しない性能が保証
  - 転送中や保存時に暗号化が可能
    - 設定が必要
    - Glacierは自動で暗号化される。

- 保存形式
  - バケット
    - 保存場所で名前はグローバルでユニークである必要がある。
  - オブジェクト
    - S3に格納されるファイルで、URLが付与される。
    - バケット内のオブジェクトは無制限
  - オブジェクトのデータサイズ
    - 0kBから5TBまで保存可能。

### S3のオブジェクト構成要素

- Key
  - オブジェクトの名前。バケット内のオブジェクトは一意に識別。
- Value
  - データそのもの。バイトデータで構成される。
- Version ID
  - バージョン管理を有効とする場合その管理に用いるID。
- metadata
  - オブジェクトに付随する属性の情報。
- sub resource
  - ACLなど管理するためのサポートを提供。

### S3のストレージタイプ

|タイプ|特徴|耐久性|可用性|
|:---|:---|:---|:---|
|STANDARD|基準。この中では最も高いが標準。|99.999999999%|99.99%|
|STANDARD-IA|低頻度アクセス用。スタンダードに比べて安価|99.999999999%|99.9%|
|One Zone-IA|可用性が99.5%に低下。安全ではなくてもよいデータ。バックアップの一時用途など。|99.999999999%|99.5%|
|RRS(Reduced Redundancy Storage)|低冗長化ストレージ。耐久性が低下。非推奨でアップデートされておらず、スタンダードよりも高いため現在は使わない。|99.99%|99.99%|
|Amazon Glacier|最安のアーカイブ用ストレージ。データ抽出に3～5時間を要する。迅速取り出しタイプでも1～5分必要。|99.999999999%|N/A|

- IAはinfrequency access（低頻度アクセス）

- 耐久性
  - データが失われない確率。
- 可用性
  - サービスが停止する確率(頻度)。

- Glacierにはいろんなタイプがある。
  - Glacier Instant Retrieval
    - ミリ秒単位で瞬時にアクセス可能。アクセスが４半期に一度程度を想定
  - Glacier Flexible Retrieval(旧Glacier)
    - 数分～数時間でアクセス可能。アクセスが年に一度程度を想定
  - Glacier Deep Archive
    - 数時間でアクセス可能。アクセスが年に一度未満を想定

### S3 Intelligent-Tiering

- 低頻度アクセスのオブジェクトを自動的に低頻度アクセス層に移動することでコストを削減する。
- 低頻度アクセス層の法が値段が安いが、取り出しに時間がかかるレイヤ。
- 基本的には30日間アクセスがないと低頻度アクセス層に移動する。
- 低頻度アクセス層のデータをアクセスした場合は、自動的に高頻度アクセス層に戻る。

### S3のpricing

- 以下に応じて課金される。
  - 保存データ容量
  - データ取得リクエスト
    - PUT, COPY, POST, LIST
    - GET, SELECT, その他
  - データ転送アウト
    - インは無料
    - アウトは有料
      - 1GB/monthまでは無料。
      - 転送費用がもっとも掛かると思ってよい。(約0.1USD/GBなど)

- 値段はリージョンによって多少変動する。

### S3の整合性モデル

- ~高い可用性を実現するため、データの更新・削除には結果整合性モデルを採用している。~
- 同時書き込みはタイムスタンプ順に処理。
- 整合性モデル
  - CREATE: Consistency Read
  - UPDATE: Eventual Consistency Read
  - DELETE: Eventual Consistency Read

- 整合性モデルとは？
  - 同時に複数の人がデータにアクセスした際の取り決め

- 結果整合性
  - 変更中のデータが完了していない場合でも他の人は古いデータを参照できる。
  - つまり、参照しているデータが古い可能性がある。
- 強整合性
  - 変更中のデータが完了するまで他の人は参照できない。
  - 見えているものは最新であることが保証される。

### S3のアクセス管理

- IAMユーザーポリシー
  - IAMユーザー・リソースに対してS3へのアクセス権限を設定することが可能。
  - S3サービスへの権限となる。個々のバケットなどへの設定は、バケットポリシーやACLで実施する。
- バケットポリシー
  - アクセス権をJSONで設定。
    - IPアドレスを制限したり、など。
  - 他アカウントへの許可も可能。
  - バケット単位の高度なアクセス管理向け。
- ACL
  - バケットと個々のオブジェクトへのアクセス権限をXMLで設定する。
  - 他アカウントへの許可も可能。
  - 簡易的なアクセス管理向け。（このオブジェクトのみを公開したい場合など）
- 署名付きURL
  - AWS SDKで作成した署名付きURLでS3のオブジェクトへの一定時間アクセスを許可。

- S3はインターネットからのパブリックアクセスが可能。
  - デフォルトはオフの設定でる。

### S3の暗号化

- SSE-S3(Server Side Encryption)
  - S3の標準暗号化方式で簡易に利用可能。
  - キーの作成・管理をS3で自動で実施。
  - AES-256でデータを暗号化。

- SSE-KMS
  - AWS KMSに設定した暗号化キーを利用した暗号化。
  - ユーザー側でキーを作成・管理することが可能。
  - クライアント独自の暗号キーを利用可能

- SSE-C
  - ユーザーが指定したキーによるサーバー側の暗号化を使用することが可能。
  - 利用設定や管理が煩雑。
  - マネジメントコンソールではなくSDKなどを使用した設定が必要。

- CSE(クライアントサイド暗号化)
  - S3に送信する前にデータを暗号化する方式。
  - AWS KMSなどを利用してキー作成を実施。
  - アプリケーション内に保存したマスターキーを使用。

## S3アクセスポイント

- S3上のデータを使用するアプリケーションへのアクセス管理を実施。

- 手順
  - アクセスポイントを作成
  - アクセス制限を設定（特定のIPやウェブサービスなど）
  - VPCに対して特定のS3バケットへのアクセス制限を設定
  - アプリケーション向けのアクセス対象を制限・拡大などをコントロール

- バケットポリシーとの違い
  - バケットポリシーはバケットに一つのみ設定できる、共通の設定。
  - 複数の設定やより複雑なアクセス制限はアクセスポイントで実現できる。
    - ユーザーによって権限を変えるなど。
    - アクセスポイントを経由しないアクセスを禁止する、なども可能のようだ。
      - https://dev.classmethod.jp/articles/explain-the-good-point-of-s3-access-points/

### オブジェクトlambdaアクセスポイント

- オブジェクトを何かしら変換してそのデータを取得することが可能。

### マルチリージョンアクセスポイント

- 複数のリージョンにある複数のバケットを一つのアクセスポイントに接続できる。

## S3アクセスアナライザー

- 外部ユーザーにも公開して使われるユースケースも多いため、アクセスアナライザーが存在する。

- アクセスポリシーに沿っているかを確認。
  - 不正なアクセスが発生してないか
- IAMアクセスアナライザーを有効化して、S3に適用させたもの。
- 監視対象は対象は以下
  - バケットポリシー
  - ACL
- パブリックアクセスや共有バケットの設定なども確認できる。

- IAM側でアクセスアナライザーが作成されている必要がある。

- アクセスアナライザーはポリシーの利用状況を確認する。

- CloudTrailなどで実施するログの分析は操作などのログを分析し、そこが使い分けるポイントである。

## ブロックパブリックアクセス設定

- パブリックアクセスはデフォルトを設定できる。
- 初期状態ではブロックの設定となっている。

## ライフサイクル管理

- バケット内のオブジェクト単位でストレージタイプの変更や削除時期などを設定し、自動化できる。
  - バケット全体やprefixに設定
  - 毎日0:00UTCにキューを実行
  - 最大1000個のルールを設定可能
  - IAに移動できるのは128KB以上のオブジェクト
  - MFA Deleteが有効の場合、設定不可。

## レプリケーション

- デフォルトでも複数AZで冗長性を持つが、クロスリージョンでレプリケーションすることで更に耐障害性を高められる。
- リージョンに別々のバケットを作成し、レプリケーションを設定する。
- トリガー
  - create, update deleteなどをトリガにする。
- バージョン機能を有効にする必要がある。
- 双方向にレプリケーションすることも可能。
- データの転送には費用がかかる。

## バージョン管理

- ユーザーによる誤操作で削除・上書きされてしまってもバージョンから復元が可能。
- バージョン毎にデータが作成されるため容量を使用してしまう。
- そのため、ライフサイクル管理により保存する期間も指定可能。

## バックアップ

- Glacierを利用してバックアップと復元が可能。
- ライフサイクル設定によりGlacierに移動させることができる。

## S3利用状況の確認

### S3の分析(ストレージクラス分析)

- データのアクセスパターンの可視化が可能。
- CSV形式で出力可能。
- 出力先のバケットを指定したりすることが可能。
- アクセス頻度の低いデータや保存期間を確認し、ライフサイクルポリシー設定に活かすことが可能。

### イベントの通知

- バケット内のイベント発生をトリガーにしてSNS/SQS/Lambdaに通知設定が可能。
- シームレスなシステム連携処理を実現。

## S3データの解析

- 用途に応じて複数サービスから選択が可能。

- S3 Select (Glacier Select)
  - S3内で直接クエリを実行しデータを取得できる。
  - 検索に使うイメージ。
  - gzipデータや、CSV、JSONに対して実行可能

- Amazon Athena
  - S3内のデータを直接・簡単に分析できるようにするインタラクティブなクエリサービス
  - より複雑なクエリを実行する場合に使用。分析に使うイメージ。
  - Athena SQL クエリで、SageMaker機械学習モデルを呼び出し、推論することも可能。

- Amazon Macie
  - 機械学習によりS3の機密データを検出・分類・保護できるフルマネージド型サービス。
  - 機密データ検出や調査を実施できる。
  - コンプライアンス調査などに使用する。

- Amazon Redshift Spetrum
  - S3の格納データに対して、Amazon Redshiftから直接クエリを実行できる機能。
  - Redshiftクラスターが必要なため、Redshiftを使用している場合はお勧め。

## CORS

- 同じドメインからしか通常データにアクセスできないが、それを回避するCORSの設定。
- これがS3でもできる？

## マルチパートアップロード

- 大容量のデータを分割してアップロード可能。
  - 最大サイズは5TB。
  - 分割は5MB～5GBのサイズ。ただし最後は5MB以下でもOK。
  - 分割数は1～10,000を指定可能。
- 失敗した場合はパートデータが残る。ライフサイクル管理でクリーンアップ設定が可能。

## バッチオペレーション

- S3オブジェクトの大量データに対して一括処理が可能。
  - 数十億などのオーダーでも実施可能。
- ジョブ
  - ジョブを作成し、実行するために必要な情報を登録。
  - オブジェクトのリストを渡し、それらのオブジェクトに対して実行するアクションを指定。
- マニフェスト
  - オブジェクトキーをリストするS3オブジェクト
  - マニフェストオブジェクトキー、ETAG、およびオプションでバージョンIDを指定。
  - S3インベントリレポート、CSVファイルの２つの形式で設定可能。

## Storage Lens

- アカウント全体のストレージの使用状況とアクティビティの傾向を可視化することができる。
- ただしrootアカウントでは使用できず、IAMアカウントでアクセスする必要がある。

- 使用状況とアクティビティの傾向を確認できる。

- 使用する際はダッシュボードの作成が必要
  - Organizationの設定をしていた場合、対象範囲をOrganizationにした分析も可能。
  - 対象のバケットのを選択できる。
- アクセスする際は権限が付与されたIAMユーザーである必要がある。

### AWS Organizationsの設定

- Organizationsで管理している複数アカウントについてもStorage Lensを使用することが可能。

## S3のMarketplace

- バックアップやデータ分析などのS3用のソフトウェアを確認可能。

## Tranfer Acceleration

- 高速エンドポイントを使用して転送を高速化する。
- クライアントとS3バケット間で長距離ファイル転送を、高速・簡単・安全に実行。
- 世界中のクライアントからアップロードされる。
- 大陸間で定期的にギガバイト・テラバイト単位のデータ転送を行う。

## リクエスタ支払い

- データを取り出したアカウント側に課金するための仕組み

## 静的ウェブサイトホスティング

- 静的なウェブサイト（動きのない）はS3でデプロイできる。

## S3の用途

- 大量データを長期保存するという観点から以下が挙げられる。
  - コンテンツの配信・保管
  - ログ・バッチの保管
  - バックアップ、ディザスタリカバリ
  - Webの静的ホスティング
    - ランディングページ程度であれば安く済ませることができる。
    - 独自ドメインをバケット名として指定。任意のドメインへのリダイレクト機能など。
    - 異なるドメインからのアクセスを実現するためにはCORSを利用。
    - CloudFrontと連携して高速で配信することも可能。
  - データレイク
    - S3やGlacierに保存する。
    - 分析や短期用にはRedshiftを使うなどのすみわけ


## S3の実際の動作

### S3の作成

- S3はリージョンを指定して作成する（AZではないし、VPCも指定しない）。
- 既存のバケットからコピーすることも可能。
- ACLの設定
- ブロックパブリックアクセス設定
- バケットのバージョニング
- 暗号化
  - マネジメントコンソールで指定可能なのはSSE-S3とSSE-KMSのみ。
- オブジェクトロック
  - 削除または上書きを無効にする機能。監査ログの保存用など。
  - 有効にするためには、バージョニングが有効である必要がある。

### S3のプロパティ

- バージョニング
- タグ
- 暗号化
- Intelligent-Tiering Archive
- サーバーアクセスログの記録
- CloudTrailデータイベント
- イベント通知(EventBridge)
- Transfer Acceleration
- ロック
- リクエスタ支払い
- 静的ホスティング

### S3のアクセス許可

- ブロックパブリックアクセス
- バケットポリシー
- オブジェクト所有者
- ACL
- CORS
  - 静的ホスティング時に使用

### S3のメトリクス

- バケットサイズやオブジェクト数
- ストレージクラス分析
- レプリケーションのメトリクス
  - レプリケーションの実行状況を確認できる。

- リクエストメトリクス
  - フィルターを指定して、リクエスト毎(POST, GETなど)のメトリクスを取得できる。

### S3の管理

- ライフサイクルルール
- レプリケーションルール
- インベントリ設定
  - オブジェクトのリストなどを収集

### S3のアクセスポイント

- アクセスポイント

### オブジェクトのアップロード

- アップロード時に以下が変更可能
  - バージョニングの有効化
  - ACLの設定
  - ストレージクラスの選択
  - 暗号化の設定

### パブリックアクセスの設定

- パブリックブロックアクセスをオフにする。
- ACLの有効化
  - 以下のアカウント毎に設定ができる。
    - バケット所有者
    - 全員 (パブリックアクセス)
    - Authenticated User (AWSアカウントをもつすべてのユーザー)
    - S3ログ配信グループ？
  - 全員を選択すれば、パブリックアクセスとなる。
    - バケット側にACLを全員(パブリックアクセス)に公開設定としていれば、アップロードした瞬間に公開することができる。
- 公開したいオブジェクトを選択し、オブジェクトアクションで「ACLを使用して公開する」を実施。


### 署名付きURL

- 特定のユーザーへ一時的に公開したい場合などに署名付きURLを使用する。
- 公開したいオブジェクトを選択肢、オブジェクトアクションで「署名付きURLで公開する」を実施。
- URLを知っている人のみがアクセスできる
- 有効な時刻を設定することが可能。
- パブリックブロックアクセスを有効化してもアクセスできる。

### バージョニングの有効化

- バケットの設定で有効化できる。
- 更新した場合は、再度公開設定を実施する必要がある。
- 削除をしてものも、オブジェクトのバージョンリストの表示で確認することができる。
- バージョン自体の完全な削除は、MFAを有効化して安全にすることも可能
  - これには、マネジメントコンソールでは実行できないため、CLIやAPIでの設定が必要。

### Intelligent tiering archive

- 通常のIntelligent-Tieringとは違い、Glacierを使う。

- GlacierとGlacier Deep Archiveに低頻度のデータを移動することができる。
  - Glacierは3～5時間取り出しに掛かる。
  - 日数を指定する。
  - Deep Archiveは最大12時間かかる
  - 年に1回程度しかアクセスしないものを置くと良い。

### アクセスログの有効化

- 同じバケットのフォルダにも保存が可能。

### イベント通知の設定

- prefixやsuffixを指定することができる。
- イベントのPUT, POSTなど操作毎に記録するかどうかを設定できる。
- lambda, SNS, SQSなどの送信先と連携できる。
  - 送信先のリソースは作成が必要。

### Transfer acceleration有効化

- グローバルなロケーションを使って高速化エンドポイントを使う。
- この機能はバケット全体に設定される。
- 有料？？

### リクエスタ支払いの有効化

- データ転送アウトとリクエスト数に応じた分の料金を、実行したAWS側に課金することができる。

### 静的Webホスティング

- 静的Webサイトと他のデータのバケットの混在はあまりしない方がよい。
- 専用のバケットを作成する。
- 公開する際はACLを有効化、パブリックアクセスブロックをオフにする必要がある。
- 静的ウェブサイトを有効化する。

- ホスティングタイプは２つある。
  - 静的ウェブサイトのホスト
  - オブジェクトのリクエストのリダイレクト

- リソースを指定する(index.htmlなど)。
- その他リダイレクトルールをJSONで設定可能。

- その後設定したリソースをACL経由で公開する。(普通のオブジェクト公開と同じ)

- それに加えてバケットポリシーを設定する必要がある。
  - なぜ？
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadForGetBucketObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucket-name/*"
        }
    ]
}

```

### ライフサイクル管理

- ルールの作成
  - プレフィックスでフィルターしたり、すべてのオブジェクトに対して指定する。

- アクションを選択できる。（複数選択可）
  - オブジェクトの最新バージョンをストレージクラス間で移動
  - オブジェクトの非現行バージョンをストレージクラス間で移動
  - オブジェクトの現行バージョンを有効期限切れにする
  - オブジェクトの非現行バージョンを完全に削除
  - 有効期限切れのオブジェクト削除マーカーまたは不完全なマルチパートアップロードを削除

- オブジェクトの現行バージョンをストレージクラス間に移行する
  - GlacierからStandard-IAなど逆の設定はできない
  - 選択先には、Intelligence Tieringなども選択可能

- オブジェクトの非現行バージョンをストレージクラス間で移動
  - 最新でなくなった日付で指定

- オブジェクトの現行バージョンを有効期限切れにする
  - バージョンを自動的に作成し、現行バージョンを古いバージョンとする。
  - バージョニングが有効でない場合は削除される。
  - 「オブジェクトの現行バージョンをストレージクラス間に移行する」を指定している場合、それより後である必要がある。

- オブジェクトの非現行バージョンを完全に削除
  - 古いバージョンを削除する。

- 有効期限切れのオブジェクト削除マーカーまたは不完全なマルチパートアップロードを削除
  - そのまま

- 最後にタイムラインの概要が確認できる。

## S3とEC2の連携

- IAMロールを使う
- EC2のセキュリティで、IAMロールを変更する。
  - S3Accessを付与する。

- 以下でS3のURIを使ってコピーする。
```sh
aws s3 ls
aws s3 cp s3://bucket-name/index/html /var/www/html
```

## AWS CLI

### CLIの設定

```sh
$ aws configure
Access Key:
Secret Key:
region:
output format:
```

### バケット操作

- 作成
```python
aws s3 mb s3://bucket-name
```

- 削除
```python
aws s3 rb s3://bucket-name
```

## Cloud Shell

- マネジメントコンソールから起動できるシェル。

## リージョン間レプリケーション

### 設定

- バケット作成し、既存のバケットから設定をコピーするをチェックして設定する。
- レプリケーションはバージョン管理を有効化する必要がある。
  - バージョンの変化をトリガにレプリケーションするため。

- レプリケーションルールを作成する。
  - ステータスは有効にする。
  - プレフィックスで対象を絞ることもできる。
  - 送信先の設定
    - 別アカウントのバケットを設定することもできる。
  - IAMロール
    - 新しいロールを作成すると、自動で必要なロールが作成される。
  - 暗号化されたオブジェクトをレプリケートするかどうか
    - 復号化のキーを指定する。
  - 送信先のストレージクラスを設定する。
    - スタンダード以外を選択することも可能。
  - 追加のレプリケーションオプション
    - レプリケーション時間のコントロール (RTC)
      - 新しいオブジェクトの 99.99% が 15 分以内にレプリケートされ、レプリケーションのメトリクスと通知が提供されます。追加料金が適用されます。
    - レプリケーションメトリクスと通知
      - Cloudwatch メトリクスを使用してレプリケーションルールの進行状況をモニタリングします。Cloudwatch メトリクスの料金が適用されます。
    - 削除マーカーのレプリケーション
      - S3 削除オペレーションによって作成された削除マーカーはレプリケートされます。ライフサイクルルールによって作成された削除マーカーはレプリケートされません。
    - レプリカ変更の同期
      - このバケットのレプリカに行われたメタデータの変更をレプリケート先バケットにレプリケートします。

### コピーの実行

- レプリケーションを設定しただけでは、それまでの状態は複製されない。

- レプリケーションの準備段階として、同じオブジェクトを持つ構成にします。

- 以下でバケット全体の複製ができます。
  - コンソール上では、バケット全体の複製ができない。

```sh
$ aws s3 cp --recurisive s3://bucketname s3://bucketname
```

- エラーが出る場合、timezoneを確認して日本時間にしてみてください。

- その後ファイルなどを作成すれば15分いないにレプリケーションされる。

## クロスアカウントアクセス

- 別アカウントのIAMユーザ、ロールからのアクセスを許可する設定。

- ３つの方式がある。
  - バケットポリシーとIAMポリシー
  - ACLとIAMポリシー
  - IAMロールによる権限移譲

- バケットポリシーとIAMポリシー
  - S3バケットへのアクセスするIAMポリシーを作成
  - IAMユーザーとロールにIAMポリシーをアタッチ
  - バケット全体への権限をバケットポリシーでアカウントを指定して許可をする。
- ACLとIAMポリシー
  - S3バケットへのアクセスするIAMポリシーを作成
  - IAMユーザーとロールにIAMポリシーをアタッチ
  - オブジェクトへの権限をACLでアカウントを指定して許可をする
- IAMロールによる権限移譲
  - IAMロールの権限移譲を利用してプログラムまたはコンソールアクセス用のクロスアカウントIAMロールを設定する。
  - AssumeRoleの実行を許可したロールにより別のアカウントのユーザー権限を移譲する。

### 手順

- アカウントB（別アカウント）でS3バケットを作成。
- S3バケットにアカウントAのIAMユーザーへの権限を与える。
- アカウントAのIAMユーザーを使って、AWS CLIを用いて、S3バケットにアクセスする。

- クロスアカウント用のバケットポリシーは以下。
```json
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Sid": "Only allow writes to my bucket with bucket owner full control",
         "Effect": "Allow",
         "Principal": {
            "AWS": [
               "arn:aws:iam::860853660447:user/udemyB"
            ]
         },
         "Action": [
            "s3:PutObject"
         ],
         "Resource": "arn:aws:s3:::awsdoc-example-bucket/*",
         "Condition": {
            "StringEquals": {
               "s3:x-amz-acl": "bucket-owner-full-control"
            }
         }
      }
   ]
}
```

- アップロードコマンドは以下

```sh
$ aws s3 cp test.text s3://cm-cross-account --acl bucket-owner-full-control
```

### オブジェクト所有者

- オブジェクトをアップロードしたユーザーがオブジェクト所有者になる。

- クロスアカウントの場合も同様。

- それを回避するため、オブジェクトの所有権を変更するACLを付与しながら、アカウントAのアップロードを実施する。

- オブジェクトの所有者が「オブジェクトライター」となっているため、これを「希望するバケット所有者」に変更する。

### ACLでのクロスアカウント許可

- メールアドレスか正規ID(長い文字列)を指定すれば、許可することができる。

- これはバケット単位でもオブジェクト単位でもACLで制御することができる。

  - バケット単位で設定した場合でも、既にアップロード済みのオブジェクトについては、個々に設定する必要がある。

## CORSの設定

- CORSはポリシーなどと同様にJSON形式で指定する。

- 静的ホスティングなどの場合に別ドメインへ参照できるようになると思われる。

```json
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "POST",
            "DELETE"
        ],
        "AllowedOrigins": [
            "http://www.example.com"
        ],
        "ExposeHeaders": []
    }
]
```

## インベントリの作成

- インベントリは目録のことで、バケット内にどのようなデータが入っているのかを収集できる。

- prefixの設定が可能。

- インベントリの送信先に、別のバケットを設定可能。

- フォーマットは、CSVなどを指定可能。

## アクセスポイント

- アクセスポイントの作成
  - VPCからか、インターネットからかを選択することが可能。
  - パブリックアクセスブロックの選択ができる
  - アクセスポイントポリシーの設定
    - AWSには別のアカウントのIAMユーザーを指定する。
  ```json
  {
    "Version":"2012-10-17",
    "Statement": [
    {
        "Effect": "Allow",
        "Principal": {
            "AWS": "arn:aws:iam::123456789012:user/Charles"
        },
        "Action": "s3:ListBucket",
        "Resource": "arn:aws:s3:us-west-2:123456789012:accesspoint/my-access-point"
    }]
  }
  ```

- アクセスポイントは複数作成できる。
  - バケットポリシーの代わりに使用でき、IAMユーザー専用の制御ができる。
  - バケットポリシーは一つしか作成できないが、アクセスポイントはIAMユーザー毎などに作成できる。
  - このように複数のアカウントについてポリシーをそれぞれ制御したい場合は、アクセスポイントを使用する。

## マルチリージョンアクセスポイント (MRAP)

- 複数のリージョンの、複数のバケットを一つのアクセスポイントに紐づけすることができる。

## オブジェクトlambdaアクセスポイント

- lambdaアクセスポイントは、オブジェクトを取得する際にlambdaによるカスタム変換を実行できる。

- lambdaアクセスポイントを使用するためには、既存のアクセスポイントを作成したうえで選択が必要。

- 変換用のlambda関数も指定できる。

- アクセスポイントポリシーをバケットポリシーと同様に指定することができる。

## AWS Storage Gateway

- オンプレからS3にバックアップしたい場合などに使用。
- 標準的なストレージプロトコルを利用して接続する。
- 利点
  - オンプレ側からAWSが有する機能や性能を活用できる。
  - オンプレとのシームレスな連携が可能
- 用途
  - ビックデータ処理、クラウドバースティング、システム移行のために一時的にデータを置きたい。
  - バックアップ・アーカイブ・災害対策
- ３つのタイプ
  - ファイルゲートウェイ
    - S3オブジェクトにファイルデータを格納
    - 仮想アプライアンスでNFS v3 / v4.1 のインターフェースを提供
    - データは非同期でAWSに転送
    - ファイルとオブジェクトは1対1のマッピング
    - ライフサイクルポリシー、バージョニング、クロスリージョンレプリケーションなどが利用可能
  - ボリュームゲートウェイ
    - S3およびEBS snapshotsをバックエンドとしたブロックストレージ
    - ディスクデータをSnapshotとしてS3に取得し、AWSでDisaster Recoveryを実現
    - iSCSIでインターフェースを提供
    - オンプレミスのローカルディスクのバックアップを自動的にAWSに実施
    - データは非同期でAWSに転送
    - オンプレ側へのリストアやAWSのEBSディスクへのリストアも可能
  - テープゲートウェイ
    - S3およびGlacierにデータを保管する仮想テープストレージ
    - VTL(virtual tape library)対応バックアップソフトウェアを利用
    - オンプレおよびEC2環境で利用可能

## Snowball

- 物理ストレージデバイスを使用し、インターネットをつかわず物理的にデータセンターにもっていって、データを転送するサービス。
- 時間がかかりすぎるデータを転送したい場合に実施する。
- すべてのリージョンで80TBモデルを使用可能。
- 暗号化が強制され、保管中や輸送中のデータを保護する。

## S3 Glacier

- S3よりも安価なストレージ。
- S3と同じ耐久性だが、データ取得の迅速性が低い。

### Glacierの特徴

- アーカイブ単位で保存される。
- 1つのアーカイブの最大サイズは40TB。(S3のオブジェクトは5TBであった)
- アーカイブIDが一意に割り当てられ、作成後はアーカイブを更新できない。
  - 更新の際は新しいアーカイブを作成することになる。
- アーカイブを保存するためのコンテナとしてボールトという単位がある。(S3のバケットに相当)
- ボールトは一つのAWSアカウントに最大1000個まで使用可能。
- AEC-256を使用してデフォルトで自動的に暗号化。(S3と同じ)
- S3と異なり直接データをアップロード・取得ができないため、S3ライフサイクル管理か、プログラムによる処理が必要
- Glacierの最低保持期間は90日。
  - 削除できないため一時的なストレージには不向き。30日間などの場合はS3で30日使う方が安い。

- Glacierには３つのタイプがある。
  - Glacier Flexible Retrieval(旧Glacier)
    - 数分～数時間でアクセス可能。アクセスが年に1,2回度程度を想定。
    - 通常のデータ検索（３～５時間）、迅速取り出し（2～5分）は有料で取り出し。
    - 一括検索（５～１２時間）で無料で取り出し可能。
    - ボールトロック機能でデータを保持。
  - Glacier Instant Retrieval
    - ミリ秒単位で瞬時にアクセス可能。アクセスが４半期に一度程度を想定
    - 医用画像やニュースメディアなど。
    - S3と同じパフォーマンスでのデータ取り出し。
    - 可用性は少し低め（99.9%）
  - Glacier Deep Archive
    - 数時間でアクセス可能。アクセスが年に一度未満を想定
    - ７～10年以上保持されるめったにアクセスしないデータ向け。
    - 標準取り出しで12時間以内、大容量取り出しで48時間以内にデータ取得。

### Glacierの仕組み

- ボールト==バケット、アーカイブ==オブジェクト
- ジョブ
  - アーカイブにSELECTクエリを実行したり、アーカイブを取得したり、ボールトのインベントリを取得したりする実行単位
- 通知
  - ジョブには時間がかかるため、SNSと連携した通知設定が可能。

### Glacierのデータ取り出しタイプ

- 取り出し方法により時間と料金が変わる。

- 迅速
  - 1～5分で使用可能になる。
- プロビジョニングキャパシティ
  - 迅速取り出しを事前に予約して保証する仕組み
  - 迅速とセットで使用する。
- 標準
  - 3～５時間で完了
- 大容量取り出し
  - 最も安価な取り出しオプション
  - ５～１２時間で完了。

- 取り出しタイプはマネジメントコンソールでは扱えず、CLIなどで行う。

### Glacierのアクセス管理

- IAMポリシー
  - IAMユーザーやリソースに対してアクセス権限を設定する。
- ボールトポリシー
  - バケットポリシーのようなもの。
- データ取り出しポリシー
  - データ取り出しに関する制限を定義。
  - 無料利用枠に制限、無料利用枠を超える容量を取り出したい場合は、最大取得率を指定すると取り出し速度を制限し、コストの上限を設定することができる。
- ボールトロックポリシー
  - ロックにより変更を禁止することにより、コンプライアンス管理を強力に実施可能
- 署名
  - 認証保護のために全リクエストに対して認証が必要。

### Glacierの料金

- S3と異なる点は、取り出しがS3よりも高いこと。

- 容量料金はS3標準は0.25USD、Glacierは0.005USD。
- データ取り出し料金
  - GB単位とリクエスト単位で課金。
- プロビジョニングされた迅速取り出し
  - 予約する場合はより料金がかかる
- データ転送（イン）は無料。
- インターネットへのデータ転送（アウト）は1GB/monthまで無料、以降は有料。

### Glacier Deep Archive

- Glacierよりも値段が安く、データ取得がより遅い。
- 基本的なデータモデル、管理はGlacierと同じ。

### ボールトの作成

- 作成時に通知用のSNSトピックを作成することができる。
- あくまでバックアップ用途のため画面上では操作はできない。