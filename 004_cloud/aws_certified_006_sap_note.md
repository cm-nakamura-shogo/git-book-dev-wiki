# SAA

---
## storage

### S3

- 冗長化
  - デフォルトでAZ冗長構成となっている。
  - さらに冗長構成を高めるためには、クロスリージョンレプリケーションを使用する。
    - 使用するためにはバージョニングが有効である必要がある。
  - クロスリージョンレプリケーション設定後は、アクションに応じて非同期にレプリケーションされる。
  - その際、今までのオブジェクトは手動で(CLIなどで、マネコンは不可)レプリケーションが必要。
  - また、双方向レプリケーションするためには、お互いに設定が必要。

- 高速化
  - prefix
    - 処理並列化の工夫として日付やタイプ別のprefixを付与し、prefix毎に並列化することが可能。
  - Transfer Acceleration
    - グローバルなサービスで長距離にわたって高速転送をする場合は、Transfer Accelerationを使用する。

- オンプレとの連携
  - ストレージゲートウェイを使用する。
  - 標準的なプロトコル(NFS, SMB, iSCSI)を使用可能。
  - ２つのタイプがある。
  - 保管型ボリューム
    - プライマリをローカル、AWSに非同期にバックアップ可能。
    - データは、EBSスナップショットとしてS3にバックアップされる。
  - キャッシュ型ボリューム
    - プライマリをS3として使用し、アクセスするデータをローカルに保持する。

- エンドユーザーへの一時アクセス許可
  - 事前署名付きURLを使用可能。

- ストレージクラス
  - Standard
    - 標準
  - Standard IA
    - 低頻度アクセス用
  - One-zone IA
    - 重要でなく、低頻度アクセス用
    - なぜかログファイルなら重要でないという解釈になる模擬問題もあって？となっているが...
  - RRS
    - より耐障害性が低く、Standardよりも高いため、非推奨方式
  - Glacier (Flexible Retrieval)
    - 長期保存用。
    - 最低保持期間が90日のため、それ以下で不要になる場合は他のクラスが選択肢となる。
    - 迅速読み取りも可能だが、数分のアクセス時間は必要。
    - 通常は、3～5時間で読み取り
    - 大容量取り出しは5～12時間で読み取り。
  - Glacier Instant Retrieval
    - より低頻度アクセスだが、取り出しはミリ秒単位(S3と同等)に必要なデータ向け。
    - 医用画像やニュースメディアなど。
  - Glacier Deep Archite
    - ～12時間で読み取り。

- ストレージクラス分析
  - アクセスパターンを分析し、適切なデータを適切なクラスに移行するタイミングを判断できます。

- 整合性
  - 2020年12月より、強い整合性モデルに変更されている。

- MFA認証
  - 誤って削除するのを防ぐ目的で、削除時にMFA認証を設定することができる。

- S3 Access Analyzer
  - AWSアカウントの外部からアクセスできるリソースに対してアクセス情報を分析する。

- 暗号化
  - 暗号化を有効にすることで、アクセスログなども自動で暗号化される。
  - バケット作成時ではなくとも、後から設定することが可能。
  - Storage GatewayやGlacierは、デフォルト設定で暗号化が有効となる。

- 暗号化のタイプとヘッダ
  - SSE-KMS/SSE-S3
    - x-amz-server-side-encryption
      - AES256で固定
  - SSE-C
    - x-amz-server-side​-encryption​-customer-algorithm
      - AES256で固定
    - x-amz-server-side​-encryption​-customer-key	
      - base64エンコードされた暗号化キー
    - x-amz-server-side​-encryption​-customer-key-MD5
      - エラーチェック用の整合性チェック用のMD5ダイジェスト
  - CSE
    - AWS SDKにより実施される。

- Vault lock (Glacier)
  - ロックにより変更禁止とすることにより、コンプライアンス管理を実施することが可能。

- S3 Select
  - オブジェクトのフィルタなども可能。
  - これにより必要なサブセットのみのオブジェクトを取得するなどが可能となる。
  - より複雑な分析の選択肢としては、AthenaやRedShift Spectrumなどがある。

- データの保護
  - オブジェクトのロックが可能。

- 静的ウェブサイト
  - URLは、`bucketname.s3-website-ap-northeast-1.amazonaws.com`となる。

- バージョニング
  - バージョニング可能なのはS3のみ。(EBSやEFSはバージョニングできない)
  - バージョニング開始時に既にあるオブジェクトは、バージョンIDがnullとなる。その後変更された時点でバージョンIDが付与され始める。

- ライフサイクル管理
  - S3は一定期間後のクラス変更や削除など様々なライフサイクルポリシーを設定可能。
    - EBSはライフサイクル設定できない(DLM定期スナップショットのみ)
    - EFSはIAに移動させる管理しか対応できない。
  - Glacierも一番最初の保存先選択した場合は、一定期間後に削除するポリシーなどを設定はできない。

* AWS CLIのページネーション
  * ページネーションの設定としていくつかオプションを利用可能。
  * デフォルトでは、個々のサービスによって決定されるページサイズを使用します。(S3の場合はページサイズ1,000) 
    * 3,500のオブジェクトがある場合、aws s3 api list-objectsでは、S3に対して4つの呼び出しを自動実行し、すべての結果を得る。
  * オプションを指定すると以下のような動作となる。
    * `--no-paginate`
      * バックグラウンドでのS3に対する呼び出しは1回となる。
      * 3,500のオブジェクトがある場合、aws s3 api list-objectsでは、S3に対して1つの呼び出しを自動実行し、1,000件の結果を得る。
    * `--page-size`
      * ページサイズ1,000単位であったものを変更できる。ただしすべての結果を得ることには変わりがない。
      * API呼び出し回数は増加するが、個々の呼び出しがタイムアウトにならず安定する可能性があります。
    * `--max-items`
      * 得られる結果を少なくするには、`--max-items`を指定する。
      * 次のセットを出力するために、応答には`NextToken`が含まれる。
      * これを指定する場合、`--page-size`を一緒に指定しないと項目の不足や重複など予期しない結果となるので注意する。
    * `--starting-token`
      * 前述の`NextToken`を設定することで、次の結果を取得できる。
  * 参考
    * [AWS CLI のページ分割オプションの使用 - AWS Command Line Interface](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-usage-pagination.html)

- 参考
  - [Amazon S3における「フォルダ」という幻想をぶち壊し、その実体を明らかにする](https://dev.classmethod.jp/articles/amazon-s3-folders/)
    - S3は単純なKey-Value型データストアであり、フォルダは実体がない。

### EBS

- EBSの種類
  - 汎用SSD
    - 通常用途。アプリケーションなどの環境用。
    - スループットについてはスループット最適化HDDより低い場合があるため注意が必要。
      - スループットは、gp3は1,000[MiB/sec]でgp2は250[MiB/sec]
      - IOPSはSSDの方が総じて良い。
  - Provisioned IOPS SSD
    - IOPSが16,000必要な高パフォーマンス用。
    - IOPSは容量に比例して最大64,000までプロビジョニング可能。(ただしNitro以外は最大32,000)
      - io1の場合、サイズ:IOPS = 1:50
      - io2の場合、サイズ:IOPS = 1:500
      - 参考
        - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html#EBSVolumeTypes_piops
    - マルチアタッチも可能。
    - io2は最大スループットが1,000MB/secである
    - io2 Block Expressは最大スループットが4,000MB/secであり、最も性能が高い。
  - スループット最適化HDD
    - 500 MiB/sec程度の高スループット。
    - IOPSはSSDよりも低い。
    - ルートボリュームには設定不可。
  - コールドHDD
    - アクセス頻度の低い用途。
    - 250 MiB/sec程度のスループット。
    - ルートボリュームには設定不可。

- IOPS向上施策
  - プロビジョンドIOPSにを使用する
  - あるいは、EBSの容量を追加することで、IOPSを向上させることもできる。

- EBSの冗長化
  - ミラーリング(RAID1)は最も、回復性が高い。
  - その他には、スナップショットやAMIの作成があるが、回復性は低い。

- EBSのAZ・リージョン移動
  - 同じAZ内のインスタンスにしかアタッチできない。
  - EBS自体を移動することはできないため、スナップショットを作成し、別AZ・別リージョンで複製する必要がある。
  - 複製したスナップショットは元のスナップショットの保持スケジュールなどの影響は受けない。（新しく設定が必要）

- マルチアタッチ
  - プロビジョンドIOPSのみマルチアタッチが可能。

- DeleteOnTermination属性
  - インスタンス削除後もルートボリュームのEBSのデータを保持したい場合は、この属性を無効化することが必要。

- デタッチ方法
  - 停止すればデタッチすることが可能（終了までしなくてもよい）。

- Amazon DLM (Data Lifecycle Manager)
  - 定期スナップショットなどの設定が可能。
  - 保存先はS3だが、ユーザーが指定することができない。

- EBSの変更
  - ボリュームサイズやボリュームタイプはデタッチすることなく変更することが可能。
  - ただしボリュームサイズを減らすことはできない。
  - https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/requesting-ebs-volume-modifications.html#elastic-volumes-limitations

- ファイルシステムの作成
  - 新規のEBSをアタッチした場合は、ファイルシステムを作成する必要がある。
  - フォーマット後、マウントが必要。
  - マウントターゲットは不要(EFSのみ)

### EFS

- 接続方法
  - AZ毎に１つのマウントターゲットが必要
  - NFSv4を使用

- ライフサイクル管理
  - 自動的なファイルストレージ管理
  - 30日アクセスされなかったファイルをEFS IAクラスに移行する。
  - データ削除などのライフサイクル管理設定はできない。

- S3との比較
  - S3と異なりインターネットからの直接アクセスは不可能
  - EFSは強い整合性やファイルのロックなどが可能であり

* マウントヘルパー
  * amazon-efs-utilsパッケージ
  * 暗号化オプションを設定する際などに使用する。

### Snowball

- Snowball edge
  - 安全なデバイスを使用し、テラバイト規模の大容量データを転送するサービス。
  - 物理的なハードウェアを用いた移転が可能。

- Snowball edge Compute Optimized
  - 42TBのHDD容量
  - 機械学習、動画分析向け。

- Snowball edge Storage Optimized
  - 100TBのHDD容量だが、利用可能な部分は80TB程度。

- Snowmobile
  - ペタバイト規模のデータを移行するサービス。

- 要する時間
  - 諸々で数週間は必要。
  - エンドツーエンドでは、1週間程度。
  - 100TBを1Gbps回線の場合は、Snoballの方が良い。

### 高機能なストレージのIOPS比較

- EBSのプロビジョンドIOPSは、最大64,000IOPSのベースラインまで。
- EFSは、500,000超のIOPSまで。
- Amazon FSx for Windowsは、数百万IOPSまで対応。
- Amazon FSx for Lustreは、スーパーコンピューター用。

### AWS Storage Gateway

- Amazon S3 File Gateway
  - NFSおよびSMBによりS3オブジェクトとしてファイルを保存できる。

- Amazon FSx File Gateway
  - SMBプロトコルを使用し、Amazon FSxにファイルを保存できる。

- AWS Storage Gateway Virtual Tape Library (VTL)
  - iSCSIベースの仮想テープライブラリに保存ができる。

- Volume Gateway
  - iSCSIを使用したブロックストレージを提供する。
  - キャッシュ型と保存型の2種類がある。
  - 保管型ボリューム
    - プライマリをローカル、AWSに非同期にバックアップ可能。
    - データは、EBSスナップショットとしてS3にバックアップされる。
  - キャッシュ型ボリューム
    - プライマリをS3として使用し、アクセスするデータをローカルに保持する。

  - 接続を攻撃から保護するために、以下が必要。
    - CHAP（Challenge Handshake Authentication Protocol）を構成。
    - iSCSIとイニシエーター接続を認証する

---
## streaming

### Kinesis Data Stream

- 特徴
  - データ欠落がなく耐久性があり、重複無し・順序維持をした伝送が可能。
  - データを送信するProducerとデータを処理するConsumerという構成となる。

- データ保持期間
  - 保持期間のデフォルトは24時間。設定によっては365日まで変更可能。

- Producer側
  - Kinesis Agent
    - データを収集して送信するスタンドアロンのJavaアプリケーション
  - Kinesis Producer Library (KPL)
    - データを送信するOSSの補助ライブラリ
  - Fluent plugin for Amazon Kinesis
    - OSSのFluentdの出力プラグイン
  - Kinesis Data Generator (KDG)
    - テストデータの送信ができる仕組み

- Consumer側
  - Kinesis Client Library (KCL)を用いてデータ処理・分析を実施する。
    - KCLを利用してKinesisアプリケーションを作成する。
    - EC2インスタンスで動かすことができ、KCL Workerが各インスタンス内の処理ユニット。
    - Record Processor Factory で Record Processorを作成
    - 1つの Record Processor は1つのシャードに対応し、複数のRecord ProcessorをKCL Workerにマッピング可能
  - KCLのステート管理には DynamoDB が使用されている。
  - またLambdaやEMRでデータを処理することが可能。
  - 後述のFirehoseおよびAnalyticsをConsumerとして設定することもできる。

- Amazon Kinesis Connector Library
  - DynamoDB, Redshift, S3, Elasticsearchに対するコネクタが利用可能。

- 参考
  - [Amazon Kinesis | AWS Black Belt Online Seminar](https://d1.awsstatic.com/webinars/jp/pdf/services/20180110_AWS-BlackBelt-Kinesis.pdf)

### Kinesis Data Firehose

- 保存がメインの用途となる機能。Kinesis Data StreamのConsumerとして指定することで使用する。
- S3やRedShift、Elasticsearch Serviceにロードできる。
  - DynamoDBを配送先に指定することができないので注意
- Lambdaと統合し、データ変換処理をしながらロードすることも可能。
  - 変換前のソースレコードをバックアップ用S3バケットに保存
  - 変換済みレコードを中間S3バケットに保存
  - 中間S3バケットからRedshiftにCOPYなども可能。

### Kinesis Data Analytics

- 標準的なSQLクエリでストリームデータをリアルタイム分析可能
- SQLクエリの前処理としてLambdaを置くことが可能。
- ストリームを入力とし、クエリ実行結果を出力ストリームとすることが可能。


### Kinesis Video Streams

- 動画データ専用のストリーミングサービス
- Producerは以下の方法でアップロードを実行する。
  - PutMedia API, Amazon Kinesis Video Streams Producer SDK(推奨)
- Consumerとしては以下が使用される
  - EC2, ECS, SageMaker, Rekognition Video

- ストリーミング方法に２種類ある。
  - メディア形式
    - 取り込み、保存、再生、取得・分析が可能
  - WebRTC
    - 双方向の低遅延通信が可能

- 参考
  - [AWS IoT 再入門ブログリレー Amazon Kinesis Video Streams編 | DevelopersIO](https://dev.classmethod.jp/articles/re-introduction-iot-2021-amazon-kinesis-video-streams/)
---
## Database

### DynamoDB

- マルチAZ構成は不可。（そもそもリージョン内の3つのAZでレプリケーションをするため）

- Auto Scalingの設定はRead/Write双方ともに対応。
  - トラフィック変化に応じたスループット向上を行うことができる。

- 登録・変更などをトリガにlambda実行などをする場合は、DynamoDB Streamを有効化する。
  - この変更情報は最大24時間保存される。
  - Streamを使わずに、LambdaとCloudWatch Eventsを連携することでも構築可能。

- DynamoDB Accelerator(DAX)
  - 最大10倍のパフォーマンス向上が可能。
  - ただし高コストであり、恒常的な対策であるため、一時的な負荷増にはAuto Scalingを活用する。

- 整合性モデルの変更可能
  - 結果整合性と強い整合性を設定で変更することができる。

* キャパシティモード
  * プロビジョンドとオンデマンドの２種類のモードがある。
  * プロビジョンドの場合、容量を超過した場合は、ProvisionedThroughputExceededExceptionが発生する。
    * プロビジョンドスループットと、コンシュームドスループットのメトリクスを確認することで、どのキャパシティが不足しているのか確認することができます。 

* Auto Scaling
  * オプションプロビジョニングモードを選択した場合、アプリケーションに必要な 1 秒あたりの読み込みと書き込みの回数を指定します。
  * 最大、最小のキャパシティユニットを設定し、トラフィックに応じた自動調整が可能です。
  * コストの予測可能性を得るため、定義されたリクエストレート以下に維持されるように DynamoDB を制御することができます。

- キャパシティユニットの計算
  - RCU
    - 1ユニットで、強い整合性の場合、最大4KBの項目を1秒あたり1回実行可能
    - 1ユニットで、結果整合性の場合、最大4KBの項目を1秒あたり2回実行可能
    - 4KBを超える場合、多くのRCUを消費する。
  - WCU
    - 1ユニットで、最大1KBの項目を1秒あたり1回実行可能

- LSI(local secondary Index)
  - 追加でソートキーを増やすイメージ
  - 1テーブルに５つ作成可能でテーブル作成時に作成
  - 検索を詳細にしたい場合などに使用。
  - パーティションキーとソートキーを組み合わせることで複合キーを作成できる。

- GSI(global secondary Index)
  - テーブル全体をスキャンして全体で何かを算出したい場合に使用する。
  - データに対して別のハッシュキーを設定できる。
  - 1テーブルに５つ作成可能、テーブル作成後に作成が可能。
  - テーブルが複数される。

- 大量レコード対応
  - 例えば週毎にテーブルを分けることで、検索性や削除が簡単にできる。

- グローバルテーブル
  - リージョン間でのレプリケートが可能となる。
  - レプリカ間の変更の伝搬は、DynamoDB Streamsを使用して行われる。
  - 参考
    - https://aws.amazon.com/jp/blogs/news/how-to-use-amazon-dynamodb-global-tables-to-power-multiregion-architectures/

- カーディナリティ
  - スループットを効率的に使用するためには、カーディナリティが高いパーティションキーを設定する。

* アクセス制御
  * アクセスを細かく制御するためにFine Grained Access Control (FGAC)を使用する。
  * FGACはIAMと組み合わせて使用される。

* Lambda連携
  * データ取得や集計をスケーラブルに実施するために、SQSとLambda関数を連携下処理で非同期実行処理を実施できる。

* DynamoDB トランザクション
  * DynamoDBテーブル内およびテーブル間の複数の項目を調整したり、変更しないといった開発設定が可能です。
  * 複数のアクションをまとめてグループ化し、1 つのオールオアナッシングの TransactWriteItems または TransactGetItems オペレーションとして送信できます。

* DynamoDB ストリーム
  * DynamoDB 項目に対する変更をキャプチャすることができます。
  * 前述のように、リージョン間でのレプリケートにも使用される。

- 参考
  - [コンセプトから学ぶAmazon DynamoDB](https://dev.classmethod.jp/referencecat/conceptual-learning-about-dynamodb/)
  - [【入門】私を苦しめたDynamoDB | フューチャー技術ブログ](https://future-architect.github.io/articles/20200818/)

### RDS

- 対応インスタンスタイプ
  - T,MおよびR,X,Z

- マルチAZ構成は可能。
  - 目的は冗長化。これによりセカンダリーDBを別AZに構築し、フェイルオーバー構成が可能。

- 暗号化は、作成時に有効化可能。

- Auto Scalingはストレージ容量のみに対応。

- RDS ProxyによるLambdaとの連携
  - Lambdaと連携する場合は、RDS Proxyによりconnection poolを使って接続する。
  - これにより、同時接続数の制限に達しないようにすることが可能。
  - ファイルオーバーに対する耐障害性もあり、スタンバイ側に再接続が可能。
  - https://blog.serverworks.co.jp/2022/01/20/093110

- リードレプリカを利用したフェイルオーバーは不可。
  - Auroraではこれが可能。
  - 手動で昇格させることは可能。あくまで自動ができない。

- リードレプリカはデータにラグが発生する可能性がある。
  - 非同期にレプリケートされる別インスタンスであるため
  - 最新のトランザクションのいくつかを表示できない可能性がある。

- IAMデータベース認証
  - パスワード認証不要で、安全に特定リソースからRDSにアクセスすることが可能。
  - 手順
    - RDS側にログイン専用のユーザーを作成し、テーブルなどへの権限を設定。
    - IAMポリシーを作成し、Resourceに上記のユーザーID等を指定
    - ポリシーをEC2にアタッチする。
  - ご参考
    - https://blog.serverworks.co.jp/rds-iamdblogin

- モニタリング
  - 拡張モニタリングの有効化により、インスタンスのメトリクスが確認できる。
  - これはCloudWatch Logsにデフォルトで30日間保存される。

- RDSのベストプラクティス
  - エンジンはInnoDBを使用する(MyISAMは使用不可)
  - 自動バックアップを有効化する
  - 大きなテーブルのパーティションは16TBを超過しないようにする。

- オンプレとの連携
  - オンプレの場合、スナップショットなどは使えないため、mysqldumpなどを使用してデータを移行する。

- RDSで実現できない構成の例
  - OracleデータベースでRAC(Real Application Clusters)を利用したい場合
  - Oracle Recovery Managerでバックアップを使用したい場合(DBへのシェルアクセスが必要)
  - DBへのシェルアクセスが必要な場合
  - Oracle DBでRMANによる復元処理を実施したい場合(RMANによるバックアップ自体は可能)

- MySQL固有
  - ログには、一般ログ、エラーログ、スロークエリログがある。
  - スロークエリログは、実行に要した時間が`long_query_time`秒を超過した場合に記録される。

- Amazon RDS on VMware
  - Point-in-Time Recovery、自動バックアップとバックアップ保持世代の設定、OSとDBエンジンへのパッチ適用をサポート

### Aurora

- 対応インスタンスタイプ
  - T,およびR,X

- 高速な回復性
  - リードレプリカ別リージョンに構成すれば、リージョン障害時でも使用することが可能。

- RDSとの比較
  - 一日のトランザクション数が10,000を超えるなどのケースはAuroraを選択する。

- マルチマスタ構成
  - Writerを複数別AZにスケーラブルに構築可能
  - どのノード、AZが落ちてもダウンタイムがゼロとなる
  - マルチマスタ構成の場合、すべてが読み書き可能なインスタンスのため、リードレプリカは利用できない。

- RDSからの移行
  - RDSのスナップショットを用いてAuroraに移行をする。

* エンドポイントの種類
  * Auroraは通常、クラスターとして扱うため、接続のためのエンドポイントが抽象化され、自動的なロードバランシングが行われます。
  * 特定のインスタンスを別用途として使用する場合などは、カスタムエンドポイントを構成することもできます。
  * エンドポイントの種類は以下の通りです。
    * クラスターエンドポイント(ライターエンドポイント)
      * DDLなどの書き込みを実行できる唯一のエンドポイントです。
      * DBクラスターの現在のプライマリインスタンスに接続します。
      * このエンドポイントでは、すべてのオペレーション(CRUD)が可能です。
      * フェイルオーバーにより新しいインスタンスに自動的に接続されます。
    * リーダーエンドポイント
      * 読み込み専用のエンドポイントです。
      * 複数のリードレプリカがクラスターにある場合、負荷分散を実施します。
      * クラスタにプライマリインスタンスのみが含まれている場合、プライマリインスタンスに接続され、すべてのオペレーション(CRUD)が可能となります。
    * カスタムエンドポイント
      * 選択したDBインスタンスのセットを表します。
      * 最大5つのカスタムエンドポイントを作成できます。
      * またAurora Serverlessでは、カスタムエンドポイントを使用できません。
      * 以下のような用途が考えられます。
        * 社内ユーザーをレポート生成やアドホック (1 回だけの) クエリ実行用の低容量インスタンスに振り向けたい
    * インスタンスエンドポイント
      * クラスター内の特定のDBインスタンスに接続します。
      * DBクラスター接続の直接制御を提供する。

### Redshift

- ノードタイプ
  - RAおよびDC
  - RAはストレージ容量がマネージドである。

- マルチAZ構成は不可。
  - マルチAZ環境とするためにはぞれぞれにRedshiftを構成し、同じS3入力ファイルセットをロードして構成する必要がある。

- スポットインスタンスは使用不可。
  - オンデマンドおよびリザーブドのみ使用可能。

- クロスリージョンスナップショット
  - 障害時、クラスタの復旧に備えるために使用。
  - S3に自動的にスナップショットが保存されるようになる。

- クロスリージョンスナップショットの暗号化
  - 元リージョンで暗号化されたクラスターのクロスリージョンスナップショットを有効にする。
  - そして、バックアップ先のリージョンでマスターキーのスナップショットコピー許可を設定する。
  - このマスターキーによりバックアップ先での暗号化が可能となります。

- 拡張VPCルーティング
  - これを有効にすると、通常のVPCと同様以下の設定が可能になります。
    - セキュリティグループ, ACL, VPCエンドポイント
  - 設定による料金は発生しません。
  - 逆に設定しない場合は、その他のAWSサービスなどへのトラフィックが、インターネット経由でルーティングされます。

- ワークロード管理 (Work Load Management: WLM)
  - ワークロードに応じてキューを設定し、スロットでCPUやメモリを割り当てる。
  - クエリに対して割り当てるRedshiftのリソースを指定することができる。
  - WLMによりクエリ処理をキューとして実行順序を定義可能。

- クエリハングの対策
  - 最大送信単位 (MTU) のサイズを小さくする。これにより転送量を抑えられる。
  - COPYコマンドなどの長いクエリを実行するとハングしているように見えるケースがある。
  - ODBC,JDBC使用時にクライアント側のメモリ不足エラーが発生する

- クエリに時間がかかりすぎる場合の対策
  - テーブル最適化
    - テーブルが最適化されていない 並列処理を最大限に活用できるようにテーブルのソートキー、分散スタイル、および圧縮エンコードを設定します。
  - ディスク書き込みの発生
    - クエリが少なくともクエリ実行の一部でディスクに書き込みを行っている可能性があります。
  - 他クエリの終了待ち処理
    - クエリキューを作成し、別の種類のクエリを適切なキューに割り当てることで、システムの全体的なパフォーマンスを改善できる可能性があります。
  - クエリ最適化
    - 説明プランを分析して、クエリを書き換えることが可能かどうか、またはデータベースを最適化することが可能かどうかを調べます。
  - メモリ不足
    - 特定のクエリにより多くのメモリが必要な場合は、wlm_query_slot_count を増やすことによって使用可能なメモリを増やすことができます。 
  - VACUUMコマンドの実行
    - 大量の行数を追加、削除、変更した場合、データをソートキー順序でロードしていなければ、VACUUM コマンドを実行します。
    - VACUUM コマンドを実行すると、データが再編成され、ソート順序が維持され、パフォーマンスが復旧されます。

### ElastiCache

* 高速データ処理が可能なNoSQL型のデータベース
* 単純なセッションデータ管理などの場合は、シンプルなMemcachedを選択する。
* 計算処理がある場合はRedisを選択する。
* レプリケーションや自動フェイルオーバー(高可用性)、データの永続性という面ではRedisを選択する。
* Redisの場合、Redisレプリケーションを有効化して、高可用クラスター構成とすることが可能。

* Redisクラスターにおけるデータのディザスターリカバリー(DR)およびフォールトトレランス
  * 自動バックアップ
  * Redis AOF(Append-Only File)を使用した手動バックアップ
  * 自動フェイルオーバーを備えたマルチAZのセットアップ

* Redisリードレプリカ
  * レプリカノードを追加することで読み取り性能をスケールさせることができます。

* Redisノードタイプ
  * ノードタイプを変更することで性能を向上させることができる。

### AWS Database Migration Service

- オンプレにあるデータベースを短期間で安全にAWSへ移行できるサービス。

- DMSコンソールを利用して、移行対象のテーブル、以降方式をタスクとしてJSONファイルにより設定できる。

- 手順は以下の通り
  - DMSコンソールで、以降に必要となるCPUなどを設定したレプリケーション用インスタンスを配置する。
  - ソースとターゲットのエンドポイントを選択する
  - 移行タイプは以下の３つから選択するが、新しく実施する場合は通常"migrate existing data and replicate ongoing changes"を選ぶと考えられる。
    - migrate existing data and replicate ongoing changes(初期転送後、差分転送開始)
    - migrate existing data(初期転送のみ)
    - replicate data changes only(差分転送のみ)

- ネットワーク接続方法
  - NATゲートウェイを介した通信, VPN, Direct Connectなどが選択肢としてある。

* AWS Schema Conversion Tool (SCT)
  * あるデータベースエンジンにおける既存のデータベーススキーマを、別のデータベースエンジンのスキーマに変換するツール
  * 手元のデスクトップPCなどにインストールして使用できる。
  * Oracle DBとPostgreSQLなど異なるデータベース間での変換も可能
---
## Data Processing

### EMR

- データ集約型のタスクに有用
  - ログ解析
  - データマイニング
  - 科学シミュレーション

- 豊富なオープンソースのアプリケーションに対応 (20種類)
  - Application
    - Hive, Pig, Spark SQL/Streaming/ML, Flink, Mahout, Sqoop
  - Batch
    - MapReduce
  - Interactive
    - Tez
  - In Memory
    - Spark
  - Streaming
    - Flink
  - その他
    - HBase, Phoenix, Presto Tensorflow, MXNetなど

- クラスターとしてEC2インスタンスの集合を扱う
  - 動的なスケーリングが可能
  - リザーブド、スポットインスタンスと組み合わせることができる。

- 低コスト化
  - コアノードとマスターノードをRIとし、タスクノードをスポットとする。

- ノードは３つ種類がある。
  - Master instance Group
  - Core instance Group
  - Task instance Group(s)
    - Task instance Groupは複数構成できる。
    - Group毎に異なるインスタンスタイプやスポット入札額を指定可能

- ストレージ
  - EMRFSを使用してS3内のデータに直接アクセスすることが可能。S3をHDFSと同じように扱える。
    - 可用性・耐久性をS3と同等にすることができる。
  - 従来通りにHDFSを直接使用することが可能。

- 他サービスとの連携
  - Kinesis Connector
    - ストリームデータにアクセス
  - Spark Streaming
    - Kinesis Client Libraryを使用した処理
  - DynamoDB connector for Hive
    - DynamoDBへのアクセス
  - Redshift spark connector
    - Redshiftへのアクセス

- 参考
  - [Amazon EMR | AWS Black Belt Online Seminar](https://d1.awsstatic.com/webinars/jp/pdf/services/20191023_AWS-Blackbelt_EMR.pdf)

### AWS Data Pipeline

- データの移動や変換の定時実行を自動化するためのサービス。
- DynamoDBなどに設定可能で、定期的なデータ取得タスクを設定可能。

### Amazon Athena

- S3内のデータを直接・簡単に分析可能な、インタラクティブなクエリサービス。
- SageMakerの機械学習モデルを呼び出し、推論なども実行可能。

---
## Network

### インターネット接続要件

- パブリックサブネットの場合、IGWがサブネットのルートテーブル設定されている。
- プライベートサブネットの場合、NATGWがサブネットのルートテーブル設定されている。
- NATGWがパブリックサブネットに設置されている。
- セキュリティグループの設定でインターネットアクセス許可がされている。(IGWもしくはNATGWに対して)
- ACL設定でインターネットが拒否されていない。
- パブリックIPアドレスが付与されている。(自動割り当てが有効化されている。)

### VPC

- VPC間接続にはVPC Peeringを使用する。
  - これは別のAWSアカウント間でも接続可能

- VPC Peeringで複雑になる場合は、Transit Gatewayを利用する。
  - これによりハブ・アンド・スポークス構成を使用できる。

- 設定可能なCIDR範囲は`/16 ～ /28`である。

- CIDRの拡張
  - 既存のVPCにセカンダリなCIDRを追加することにより拡張することができる。

- VPC内のインスタンスにDNS名を取得するためには、DNSホスト名有効化オプションが必要。

- VPC Peeringはエッジ間ルーティング負荷
  - VPC-A, VPC-BがPeeringしている。
  - VPC-AがDirect Connectでオンプレと接続されていても、VPC-Bはオンプレと双方向に通信できない。

- VPCエンドポイント
  - インターネットを介さずにAWSリソースにアクセスできる。
  - S3とDynamoDBのみ、ゲートウェイ型
  - それ以外のリソースはプライベートリンク型
  - ゲートウェイ型とプライベートリンク型の違い
    - [2つのVPCエンドポイントの違いを知る | DevelopersIO](https://dev.classmethod.jp/articles/vpc-endpoint-gateway-type/)

- Bastionホストとは
  - EC2などで構成する踏み台サーバーのこと。
  - publicサブネットに配置し、privateサブネット内のリソースアクセスをこのBastionホスト経由のみに限定する。
  - Bastionとは要塞という意味。

- セカンダリCIDR
  - IPアドレスが枯渇する場合、最大４つのセカンダリCIDRをVPCに追加できる。

- ポート
  - インバウンドはsshなどのポート番号を指定して解放する。
  - アウトバウンドも解放が必要で、1024-65536を解放する必要がある。
    - アウトバウンドはランダムに割り当たる。
    - その範囲はクライアントによって異なる。
      - Lambda, NAT-GW, ELBは1024-65536
      - 多くのLinuxは32768-65536
      - Windows Server 2003は1025-5000
      - Windows Server 2008以降は49512-65535

### IDS/IPS

- ネットワーク型とホスト型がある。
- ホスト型は、EC2にソフトウェアをインストールして構築する。
- ネットワーク型は、IDS/IPS専用のVPCを構築し、すべてのトラフィックをルーティングさせる。
- インスタンスが多い場合は、ネットワーク型を使用する。

### Amazon VPC Traffic Mirroring

- Nitro世代のインスタンスであれば、IDS/IPSの代わりにこちらを使用してモニタリングが可能 

### VPN

- サイト間VPN
  - オンプレと接続する場合、それぞれに以下が必要。
    - AWS VPC側(下記いずれか)
      - 仮想プライベートゲートウェイ(VGW)
      - Transit Gateway(TGW)
    - オンプレ側
      - カスタマーゲートウェイ(の接続点)
  - 端末などからVPNへの接続は、Client VPN Endpointから行う。
  - 設定手順
    - 仮想プライベートGWをVPCに関連付ける
    - カスタムルートテーブルを作成
    - セキュリティグループを更新

- パブリック仮想インターフェース
  - S3などのパブリックリソース(非VPCのサービス)に専用線経由でアクセスするために使用する。
  - 参考
    - [「パブリック仮想インターフェイス」と「プライベート仮想インターフェイス」の違い - Qiita](https://qiita.com/tsumita7/items/efcc2e0009a54b953dfe)

- VPNの接続方式
  - IPsec-VPNを用いる。
  - IPsec-VPNはSSL-VPNよりセキュリティが高く、決まった拠点間の通信が多い場合に使用される方式。
  - またIPsecはネットワーク層での暗号化、SSLはセッション層での暗号化となる。
  - そのためIPsecは上位プロトコルに依存せずにセキュアな通信が可能となる。
  - 参考
    - [IPsec-VPNとは？SSL-VPNとの違いもわかりやすく徹底解説！](https://it-trend.jp/vpn/article/48-0063)

- VPNの冗長化
  - VGWおよびTGWいずれを使った場合でもAWS側はデュアルトンネルとなり、2つのVPN接続先が用意される。
  - オンプレ側のカスタマーゲートウェイの冗長化は別途構築が必要。
    - ルーターに冗長化機能を持つ機器を利用し、Customer Gatewayを設定する。
    - 上記でも回線はシングル構成のためISP障害には対応できない。その場合は2つのCustomer Gatewayを使用する。
  - 下記が詳しい。
    - [[AWS] Site to Site VPN の冗長化を考える | DevelopersIO](https://dev.classmethod.jp/articles/redundancy-of-aws-site-to-site-vpn/)

- SSL VPN
  - 拠点間ではなく外出先などでインターネット経由でプライベートネットワークにアクセスするためのソリューション

### Direct Connect

- 準備には数日が必要。

- 冗長化としてIPsec対応のハードウェアVPNを使用することができる。

- Link Aggregation Group
  - 複数の接続を使用して、利用できる帯域幅を増やすことができます。

### Direct Connect Gateway

- マルチリージョンのVPCに接続する際には、DirectConnect Gatewayが必要となる。
- Direct Connect Gatewayにより、プライベート仮想インターフェースを別リージョンのプライベート仮想ゲートウェイ(VGW)に接続できる。

### Transit Gateway 

- 多数のVPCを管理することができる。
- またFirewallやIPSに接続することでセキュリティを管理することができる。
- AWS Transit Gateway network managerで、設定の変更が可能。(IPSの設定はここではできない)

### IPv6への対応

- 手順
  - IPv6 CIDRブロックをVPC, subnetに関連付ける。
  - IPv6トラフィック用のルートテーブル更新
    - public subnetは、subnetからInternet Gateway(IGC)にIPv6トラフィックをルーティングする。
    - private subnetは、subnetからEgress-only Internet Gateway(EIGW)にIPv6トラフィックをルーティングする。
  - SGをIPv6を含めるように更新する。
  - ACLで制限されている場合、ACLのルールもIPv6に対応するように更新する。
  - インスタンスタイプをIPv6対応のものに変更する。
  - IPv6アドレスをインスタンスに割り当てる。
  - インスタンスの設定がIPv6に対応していない場合、設定を変更する。

- IPv6のCIDR範囲は、/56固定でありユーザーが指定することはできません。

- インターネットへの接続
  - IPv6を利用する場合、NATゲートウェイによるアドレス変換の代わりに、Egress-Only インターネットゲートウェイを使用する必要がある。

### ACL

- アウトバンド・インバウンドの設定
  - `Egress:true`でアウト、`Egress:false`でインとなる。

- ポート設定
  - HTTPは`80`、FTPは`20`、SSHは`22`などとなる。

- 特定のIPアドレスの攻撃からサブネットを保護するFirewallとしても使用可能。

- ルールは番号の若い順(小さい)に適用される。

### NATゲートウェイ・NATインスタンス

- NATゲートウェイは送信側のIPをパブリックなIPに変換して送信することで、外部との通信を可能にする。
- またこれ以外でも、裏側に複数のインスタンスが存在する場合で、固定のIPを外部に見せたい場合には、NATゲートウェイが使用できる。
  - 使用可能なIPに制限数があるAPIなど。

- マルチAZ
  - AZ障害を高めるためには、NATゲートウェイも異なるAZに立ち上げる。
  - NATインスタンスも同様だが、適切に処理を引き継ぐためにスクリプトを設定する必要がある。

### Route53

- ルーティングの種類
  - シンプルルーティング
    - ランダムなルーティングでもこれを使用する。
  - 加重ルーティング
    - 複数エンドポイント毎の重みによりDNSクエリに応答。Blue/Greenデプロイメントに使用。
  - フェイルオーバールーティング
    - ヘルスチェックの結果に基づき、プライマリ・セカンダリを切り替える。高可用性が目的。
  - 複数値回答ルーティング
    - ランダムに選ばれた最大8つの別々のレコードを使用して複数の値を返答する。
    - ヘルスチェックを実施したり、ELBのようにDNSを使用した負荷分散が可能
  - レイテンシールーティング
    - レイテンシが小さいリージョンへルーティングする。
  - 位置情報ルーティング
    - ユーザーのIPアドレスにより位置情報を特定し、地域毎に異なるレコードを返す。
  - 地理的近接性ルーティング
    - ユーザーとリソース双方の場所に基づいて近接性ルールを作成してルーティングする。
    - AWSリソースを使用している場合はリソースのリージョン、それ以外の場合はリソースの緯度と経度に基づく。
    - 特殊なルーティングであり、トラフィックフローを利用して設定が必要。

- ALIAS - No設定
  - 複数値回答ルーティングの場合、AliasはNoに設定する必要がある。

- フェイルオーバールーティングを使用する場合、アクティブ・パッシブ構成となる。
  - アクティブ・アクティブにしたい場合はその他のルーティングで、ファイルオーバーを実現する。

- DDos攻撃対策
  - シャッフルシャーディングと anycast ルーティングにより、攻撃を受けていてもユーザーがアクセス可能な状態を維持することができる。

- DNSレコードの種類

|レコード名|説明|
|:---|:---|
|A|ホスト名からIPアドレスを関連付ける(IPv4)|
|AAAA|ホスト名からIPアドレスを関連付ける(IPv6)|
|CNAME|別名のドメインを定義するコード|

* ALIASレコード
  * CNAMEレコードと同様の動作が可能なAWS内用のレコード
  * 参考
    * [Amazon Route 53のALIASレコード利用のススメ | DevelopersIO](https://dev.classmethod.jp/articles/amazon-route-53-alias-records/)

### CloudFront

- コンテンツを高速配信するためのCDNサービス。

- オリジン設定不可なもの
  - WebサーバーなどのプライベートIPはオリジンに設定することができない。

- 画像等の取得リクエストに対して応答性を挙げるために使用。

- キャッシュ保持期間はTTL(Time To Live)で設定
  - TTLのデフォルトは1日。0秒～1年で指定可能。

- コンテンツ圧縮を有効化することで、高速化やデータ削減(コスト削減)が可能。
  - ただし、Viewer（ブラウザ等）で`Accept-Encoding: gzip`が有効である必要がある。

- 地理的ブロッキングで、特定国単位でのユーザーのアクセスを制限することが可能。
  - ただし国より小さい単位や、ファイルのサブセットにまでアクセス制限をしたい場合は、サードパーティの位置情報サービスを使用する必要がある。

- S3へのアクセス制限(IP制限等)するをすることが可能。
  - CloudFrontのOrigin Access Identify(OAI)を使い、特定のdistributionのみをS3のBucket Policyで許可
    - OAIは特別なユーザーであり、そのユーザーに限定してBucket Policyを設定
  - CloudFrontにWAF ACLを設定し、特定のIPアドレスのみを許可
  - OAIを使用したテンプレートはこちら
    - [CloudFormation で OAI を使った CloudFront + S3 の静的コンテンツ配信インフラを作る | DevelopersIO](https://dev.classmethod.jp/articles/s3-cloudfront-with-oai-by-cloudformation/)

- 署名付きURLと署名付きCookie
  - CloudFront自体へのアクセスを制限したい場合に使用する。
  - 制限には、アクセスの有効期限やソースのIPを設定できる。
  - 署名は以下のいずれかにより行われる。
    - Trusted Key Group (AWS推奨)
      - 信頼されたキーグループ
    - Trusted Signer (root作業につきAWS非推奨)
      - CloudFrontのキーペアを持つAWSアカウント
  - [CloudFront 署名付きURLと署名付きCookieをおさらいしてPythonで試してみた | DevelopersIO](https://dev.classmethod.jp/articles/cloudfront-signed-url-and-cookie-using-python/)

- Referer制限
  - 直前のリンクを元に参照を制限する機能。
  - CloudFrontそのもので、Referer制限はできないため、WAFを利用する必要がある。

- アクセスユーザーの制御
  - 署名付きURLと署名付きCookieを利用することが可能。

- キャッシュを効かせるためには、`Cache-Control`の`max-age directive`を適切に大きく設定する。

- ディストリビューション
  - フェイルオーバー設定が可能。
  - オリジングループとしてプライマリ、セカンダリを作成
  - プライマリオリジンが使用できない場合、セカンダリに切り替わる。
    - プライマリでHTTPレスポンスが特定のコードを返す場合なども設定可能。

- Lamda@Edge
  - Node.jsによるLambda関数をユーザーに近いCloudFrontで実行することができる。

- HTTPS化
  - 以下のいずれかでHTTPS対応を実施できる。
  - Viewer Protocol PolicyでHTTPS Onlyを設定
  - Viewer Protocol PolicyでRedirect HTTP to HTTPSを設定
  - Viewer Protocol PolicyでSSL/TLS証明書を利用できる設定

- クエリ文字列の転送設定
  - オリジンが一意のオブジェクトを返すクエリ文字列パラメータのみを転送するように設定することでキャッシュを改善できます。
  - CloudFrontは、デフォルトではクエリ文字列パラメータの転送とキャッシュを行わない。
  - 以下が設定のパターンとなる。
    - None (Improves Caching)
      - オリジンがクエリ文字列パラメータの値に関係なくオブジェクトの同じバージョンを返す場合、このオプションを選択します。
      - これにより、CloudFront がキャッシュからリクエストを処理できる可能性が高くなり、パフォーマンスが向上し、オリジンの負荷が低下します。
    - Forward all, cache based on whitelist
      - オリジンサーバーが 1 つ以上のクエリ文字列パラメータに基づいてオブジェクトの異なるバージョンを返す場合、このオプションを選択します。
      - 次に、キャッシュ条件として CloudFront が使用するパラメータを [クエリ文字列のホワイトリスト] フィールドで指定します。
    - Forward all, cache based on all
      - オリジンサーバーがすべてのクエリ文字列パラメータについてオブジェクトの異なるバージョンを返す場合、このオプションを選択します。
  - 参考
    - [CloudFront でクエリ文字列パラメータを転送するには](https://oji-cloud.net/2020/05/27/post-5040/)

- Origin Protocol Polocy
  - オリジンとの通信プロトコルを以下３種類で設定できる
    - HTTP Only
    - HTTPS Only
    - Match Viewer (HTTP または HTTPS)

- オンプレミス環境との連携
  - CloudFrontはオリジンサーバーをオンプレミスにすることが可能

- Time to Live (TTL)設定について
  - キャッシュ有効期限
  - オリジンで更新があった場合に最大でもこのTTL後に反映される。
  - 更新がない場合はキャッシュが機能する(TTL=0だとキャッシュされないわけではないので注意)
    - ただしRequest自体はオリジンに送信される。
  - 参考
    - [CloudFrontで素早くコンテンツを更新させたい場合にTTLを短くしInvalidationを行わないキャッシュ戦略を考える | DevelopersIO](https://dev.classmethod.jp/articles/cloudfront-update-content-quickly-using-short-ttl/)

- AWS Shieldとの関係
  - CloudFrontでは、デフォルトでAWS Shield Standardが適用されている。

### オンプレIP移行

- ROA(Route Origin Autorization)を利用し、特定のIPアドレスを移行することができる。

- 地域インターネットレジストリ(RIR: Regional Internet Registry)に登録。
- RDAP: Registry Data Access Protocolを利用して事故署名付きの X509 証明書を発行する。

- 参考
  - https://fluid-27.hatenablog.com/entry/2021/07/16/204216
  - https://www.nic.ad.jp/ja/basics/terms/roa.html

### IPフローティング

- Route53やELBを用いてインスタンスの障害に備えることが可能だが、IPフローティングでも実現できる。
- DNS情報の伝搬には少し時間が必要であるため、継続性が重要でダウンタイムを最小にするためには、この方式を選択する。
- ヘルスチェックにはスクリプトを作成する。

---
## Dev and Ops

- [AWS OpsWorks と AWS Elastic Beanstalkの違い](https://awsjp.com/AWS/hikaku/OpsWorks-Elastic_Beanstalk-chigai.html)
  - Elastic Beanstalk: アプリケーションの管理
  - OpsWorks: アプリケーションスタックの管理（DBやミドルウェアなど）
- [AWS CloudFormation と AWS OpsWorksの違い](https://awsjp.com/AWS/hikaku/CloudFormation-OpsWorks-chigai.html)
  - OpsWorks: アプリケーションスタックの管理
  - CloudFormation: VPCなどネットワークにわたるAWS全体

### Beanstalk

- 自動的にデプロイ・スケーリングを行うサービス。
  - キャパシティのプロビジョニング
  - 負荷分散
  - Auto Scaling
  - ヘルスチェック
  - パッチ配布

- ユースケースとしては以下
  - Webアプリケーション
  - ワーカー環境
    - ただしBatch処理などは対象外。
  - Amazon ECSなどのDockerにホストされたアプリケーションも対象。

- 運用や監視にも使用することができる。

- デプロイポリシー
  - デプロイポリシーの種類は以下の通り。
    - All at Once
      - すべてのインスタンスをアップデートする
      - ダウンタイムが一瞬発生するが、最も早い。ただし失敗した場合は全滅する。
    - Rolling
      - バッチ毎に新しくする。バッチ50%であれば、半分を新しくする。
      - 更新中は使用可能なインスタンス数が減る。
      - ダウンタイムは発生しないが、古いものと新しいものが混在する。
    - Rolling with additional batch
      - バッチ単位で新しいインスタンスを起動して、新しくする。
      - Rollingと違い、使用可能なインスタンス数が減らない。
      - ただし古いものと新しいものの混在する状態は変わらない。
    - Immutable
      - 新しいAutoScalingグループを作成してそこで１つの新しいインスタンスを起動して、新しいものを動かす。
      - そしてそのAutoScalingグループをELBにアタッチしてうまく動くか確認する。
      - OKであれば残りのインスタンをまた新規に立ち上げて、新しいものを動かす。
      - その後、もともとのAutoScalingグループをELBから削除する。
      - Immutableでも古いものと新しいものの混在する状態は変わらない。
  - 単一インスタンスの場合、All at OnceもしくはImmutableしか選択できない。
  - 混在を避けたい場合は、Blue/Greenデプロイを実施する。ただしこれは、Beanstalkのデプロイポリシーには含まれないため、OpsWork等が必要となる。
    - Blue/Greenデプロイでは、ELBごと環境をクローンしてAll at Onceでデプロイすればよい。
    - その後、ELBに割り当たっているDNS名をスワップする。
    - 逆にローリングデプロイは、本番サーバーを新しいものに段階的に切り替える、短時間に置き換えることを目的とした方式。
  - 以下を参考。
    - [https://dev.classmethod.jp/articles/elastic-beanstalk-deploy-policy/](https://dev.classmethod.jp/articles/elastic-beanstalk-deploy-policy/)

- データベース削除ポリシー
  - 保持を有効化することで、RDSをBeanstalkからデカップリングしてもデータが削除されない。

### OpsWorks

- ChefやPuppetが使用可能。
- 複雑なインフラストラクチャ管理や設定を行うサービス。
- スタックベースやレイヤーなどの構築の用途の場合はCloudFormationではなくこちらを使用する。

### CloudFormation

- 必須要素はResources。
- その他の要素
  - AWSTemplateFormatVersion: バージョンを記述
  - Description: コメントを記述。必ずAWSTemplateFormatVersionの後に記載する必要がある。
  - Metadata: テンプレートに関する追加情報
  - Parameters: 実行時に(スタックの作成・更新時に)テンプレートに渡す値。ResourcesおよびOutputsを参照可能。
  - Rules: Parameterを検証するルール
  - Mappings: 条件パラメータの指定に使用できるMap(辞書)
  - Conditions: 条件指定に使用。本番か開発かなど。
  - Transform: SAMを使用したり、別のテンプレートを利用するために使用。
  - Outputs: 構築後に出力させる値や、Exportフィールドにより他のテンプレートから参照させることなどが可能。

- 変更セット
  - スタックの更新をしたり、その影響度を確認することができるスタック

- ドリフト
  - テンプレートによる展開後に変更した場合に、差分をチェックする機能

- Export/Import
  - スタック間のリソース参照機能

- スタックセット
  - 救数のAWSアカウントやリージョンにリソースを展開できる。
  - クロスアカウントやクロスリージョンのシナリオを解決可能。

- DeletionPolicy
  - 停止後にデータを保持したい場合、DeletionPolicyを有効にする必要がある。
  - DeletionPolicyには以下の種類がある。
    - Snapshot
      - スナップショットを作成したうえで、リソースを削除する。
      - このポリシーはスナップショットが作成できるリソース(EC2やRDS)にのみ追加することができます。

    - Retain
      - リソースやコンテンツを削除せず保持します。
      - この削除ポリシーは、あらゆるリソースタイプに追加することができます。

    - Delete (Default)
      - スタックの削除時にリソースと (該当する場合) そのすべてのコンテンツを削除します。
      - この削除ポリシーは、あらゆるリソースタイプに追加することができます。

- CreationPolicy
  - ResourceSignalパラメータでTimeoutを設定することができる。
  - これによりタイムアウトを超えるまでは終了しないようになります。

- Lambdaの設定方法
  - Lambda関数のコードをzip化してS3にアップロードし、AWS::Lambda::Functionから参照することができる。
  - またNode.js および Python 関数の場合で依存関係がない限り、テンプレートにインラインで関数コードを指定できます。

### CodeStar

- CI/CDの環境を最も素早く構築するためのサービス。
- CI/CDはCloudFormationやOpsWorksでも可能だが、CodeStarは細かい設定をしなくても使用可能。
  - Beanstalkは、CI/CDの構築はできない。

- 開発言語やデプロイ先は限定的なので要注意
  - 開発言語：Java, JavaScript, PHP, Ruby, Pythonなど
  - デプロイ先：EC2, Beanstalk, Lambda

### CodeCommit

- DR
  - リージョン間レプリケーション機能がないため、Lambda関数を利用して別リージョンに同期する仕組みが必要。

### AWS CodeDeploy

* さまざまなコンピューティングサービスへのソフトウェアのデプロイを自動化する、フルマネージド型のサービスです。
* デプロイ対象は、Amazon EC2、AWS Fargate、AWS Lambda、オンプレミスで実行されるサーバーなどが含まれます。
* 変更を段階的に導入し、設定可能なルールに従ってアプリケーションの正常性を追跡します。
* エラーが発生した場合、アプリケーションデプロイは簡単に停止およびロールバックできます。

* デプロイ設定
  * EC2/オンプレ
    * One at a time ... 一つずつ置き換え
    * Half at a time ... 半分ずつ置き換え
    * All at Once ... すべて一気に置き換え
    * Min. healthy hostsで設定が可能。
  * Lambda/ECS
    * Linear
      * Stepずつ段階的にリリース。Intervalも設定可能。
    * Canary
      * 2段階でリリース。Stepは1段階での割合を示す。Intervalも設定可能。

* 参考
  * [20210126_BlackBelt_CodeDeploy.pdf](https://d1.awsstatic.com/webinars/jp/pdf/services/20210126_BlackBelt_CodeDeploy.pdf)

### CloudWatch

- CloudWatch Logs
  - EC2, CloudTrail, Route53などのログファイルを監視することが可能
  - エラー率が閾値を超えた場合に、管理者に通知を送るなどが可能。
  - アプリケーションのログは取れないため、X-rayのエージェントが必要。

- CloudWatch Events
  - システムイベントを監視し、ルールに一致したイベントを一つ以上の関数やストリームに振り分けられる。
  - cron式やrate式により、特定の時間にトリガしたり、スケジュールが可能。

- CloudWatch エージェント
  - EC2インスタンスやオンプレミスサーバーから、メトリクスやログを収集する機能。

- CloudWatch Logs Insights
  - ログを解析・可視化するフルマネージドサービス。

* CloudWatch Metrics
  * 以下のシンプルなAPI
    * GetMetricStatistics
    * ListMetrics
    * PutMetricData
  * Put処理はまとめて複数種類、複数時点のデータを送信することができる
    * これにより、秒間の API 実行回数の上限を回避することが可能
    * またAPIコール枚に料金が発生するためコストを抑制することも可能
  * 参考
    * [CloudWatch Metricsの細かすぎて誰にも伝わらない話 - Qiita](https://qiita.com/moomindani/items/1eacbfe5b71b200a2da9)

- 異なるリージョンからのメトリクスを単一のCloudWatchで取得可能。

- 詳細モニタリング
  - デフォルトは5分間隔だが、詳細モニタリングを有効にすることにより、1分間隔にすることが可能。
  - これによりAuto Scalingなどのスケールアウトもタイミング速く実施することができる。

### Amazon API Gateway

- LambdaやEndpoint on EC2などの前に設置し、公開されたAPIとして利用できる。
- REST APIおよびWebSocket APIを作成可能
- 一時的な高負荷対応には、スロットリング制限設定とキャッシュを有効化を実施する。
- APIコールとデータ量に応じた費用のみが発生する。

- API Gatewayの実行ロール
  - Lamda関数のARNを設定し、API GatewayがLambdaを呼び出すことを許可する権限を持つIAMロールを設定する。

- 認証(Lambda Authorizer)
  - LambdaコンソールでAPI Gateway Lambda authorizer関数を作成する。
  - Lambda Authorizerには２種類ある。
    - トークンベース
      - JSON ウェブトークン (JWT) や OAuth トークンなどのベアラートークンで発信者 ID を受け取ります。
      - これにより、AuthやSAML、CognitoなどのBearer Tokenによる認可戦略を使用できる。
    - リクエストパラメータベース
      - ヘッダー、クエリ文字列パラメータ、stageVariables、および $context 変数の組み合わせで、発信者 ID を受け取ります。 
  - またこのAuthorizer関数も、API Gatewayの実行ロールに設定する必要がある。
  - 参考
    - [API Gateway Lambda オーソライザーを使用する - Amazon API Gateway](https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html)

- プロキシ統合
  - プロキシ統合を使用することで、Lambda関数内でリクエストを生の状態で処理できる。
  - これによりマッピングを手動で定義する必要がなく簡単に利用が可能。
  - 参考
    - [[初心者向け] Lambda 非プロキシ統合で API Gateway API をビルドする をプロキシ統合にして比較してみる | DevelopersIO](https://dev.classmethod.jp/articles/for-beginner-build-apigateway-with-noproxy-and-proxy-lambda/)

- API実行状況の監視
  - CLoudWatchを使用して監視する。API GatewayからCloudWatchへデフォルト1分間隔でメトリクスデータが送信されます。
  - メトリクスの内容は以下です。
    - 4XXError: 指定期間のクライアント側のエラー数
    - 5XXError: 指定期間のサーバー側のエラー数
    - CacheHitCount: APIキャッシュが有効な場合に、指定期間にAPIキャッシュから配信されたリクエスト数
    - CacheMissCount: APIキャッシュが有効な場合に、指定期間にAPIキャッシュではなくバックエンドから配信されたリクエスト数
    - Count: 指定期間のリクエスト数
    - IntegrationLatency: API Gatewayがリクエストを中継してからバックエンドからレスポンスを受け取るまでの時間
    - Latency: API Gatewayがクライアントからリクエストを受け取ってからクライアントにレスポンスを返すまでの時間

* デプロイステージ
  * アルファ、ベータ、プロダクションなど、各 API 用の複数のリリースステージを管理できます。
  * ステージ変数を使用することで、異なるバックエンドのエンドポイントとやり取りするよう API デプロイステージを設定できます。

* マッピングテンプレート
  * リクエストとレスポンスのデータマッピングをセットアップすることができます。

* タイムアウト
  * 統合タイムアウトの範囲は、50msec～29secで設定できる。
  * Lambdaの実行時間制限等に引っかからない場合でも、この設定によりAPI Gateway側でタイムアウトする場合がある。

- エッジ最適化APIエンドポイント
  - APIリクエストが最寄りのCloudFrontエッジロケーションにルーティングされる。
  - これによりアップロード処理などの高速化が期待できる。

### AWS X-Ray

- リクエストやレスポンスの追跡・監視が行える。

### AWS Serverless Application Model (SAM)

- サーバレスアプリケーション構築のデプロイツール。
- CloudFormationのサーバレス拡張という位置づけ
  - [https://dev.classmethod.jp/articles/aws-serverless-application-model/](https://dev.classmethod.jp/articles/aws-serverless-application-model/)
- CloudFormationと連携し、SAMがSAM構文をCloudFormation構文に変換する。
- テンプレートに以下のように記述する。

```yaml
Transform: AWS::Serverless-2016-10-31
```

### AWS AppSync

- DynamoDB、Lambda、HTTP APIなどのデータを組み合わせて、リアルタイムアプリケーションのGraphQLインターフェースを提供するサービス。

---
## アクセス管理

### IAM

- ポリシーの種類
  - AWS管理ポリシー
    - AWSがあらかじめ準備しているポリシー
  - カスタマー管理ポリシー
    - ユーザー(開発者)が自身でカスタマイズしたポリシー
  - インラインポリシー
    - 1つのエンティティに埋め込まれたポリシーでIAMユーザなどに適用するのは非推奨。
    - S3バケットポリシーやIAMロールの信頼ポリシーなど、リソース固有のポリシーが設定可能な場合に使用
    - 他には、SNSのTopicポリシーやVPCエンドポイントポリシーなどが該当

- リソースベースのポリシーがあるサービス一覧
  - https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html

- 本番・開発の分離
  - 開発者には開発者用アカウントを付与する。
  - インスタンス等にタグを設定し、操作許可を限定する設定も有用。

- サポートするIdP
  - IdPはIdentify Providerのこと。
  - IdPとSP(Service Provider)の間の認証方式がSAML2.0やOpenID Connect。
  - IAMは、OpenID Connect または SAML 2.0と互換性のあるIdPをサポートしている。
  - OpenIDの場合、ウェブIDフェデレーションを利用する。

- 外部のIdPを使う場合
  - マネコンおよびCLIを使って、IdPのエンティティを作成して、SAMLメタデータドキュメントなどをuploadする。
  - その後、IAMロールを作成し、信頼ポリシーでProviderを、信頼関係を確立するPrincipalとして設定する。
  - ロールに必要な権限を設定する。
  - オンプレミス環境のユーザー、グループをIAMロールにマッピングするアサーションを定義する。

- 既存のActive DirectoryとAWSのSSO連携
  - フェデレーションプロキシまたはIDプロバイダーのセットアップを実施する。
  - その際、SAMLなどの標準化された認証情報をを使用して、セキュリティ情報を交換する。
  - 既存のオンプレADでは、ADFS(Active Directory Federation Services)をセットアップする。
  - そしてSAMLメタデータで認証情報を交換する。
  - 信頼関係確立のため、IAMロールを作成し、ADFSでAWS側のFederation Metadataを信頼するようセットアップする。

- aliasされたログインURL
  - `https://development-group.signin.aws.amazon.com/consle/`

- IAMロールを使用したリソースのアクセス権限
  - AWS STS AssumeRoleのAPI実行で使用するARNを渡す。
  - これにより、一時的な資格情報で新しいセッションが作成される。

- Web IdP
  - Amazon, Facebook, GoogleなどのOIDC互換のIdPを使う場合、Web IdPと呼ぶ。
  - モバイル認証で、Cognitoの代わりに使用されることがある。
  - 認証には、AssumeRoleWithWebIdentity APIを使用する。

- カスタムIDブローカ
  - LDAPなどのローカル認証システムを用いてAWSのリソースにアクセスするための方法

- Conditionに使われるタグについて
  - "PrincipalTag"
    - Principalにアタッチされたタグの条件を定義
    ```json
    // PrincipalTag(Principalにアタッチされたタグ)の"job-title"キーの値が"Product-Manager"ではない場合
    {
      "StringNotEquals": {
        "aws:PrincipalTag/job-title": "Product-Manager"
      }
    }
    ```
  - ResourceTag
    - 操作対象のResourceにアタッチされたタグの条件を定義
    ```json
    // ResourceTagの"Env"キーの値が"test"である場合。StringLikeはワイルドカード(*,?)が使えるマッチング
    {
      "StringLike": {
        "ec2:ResourceTag/Env": "test"
      }
    }
    ```
  - RequestTag
    - 操作時に付与するタグが満たすべき条件を定義する。
    ```json
    // 操作時に付与するタグに"Env"キーがあり、その値が"Dev", "Prod", "QA"である場合
    {
      "StringEquals": {
        "aws:RequestTag/Env": ["Dev", "Prod", "QA"]
      }
    }
    ```
  - TagKeys
    - 操作時に付与するタグのキーについての制限を定義する
      - `ForAllValues`と`ForAnyValues`は同一キーが何個もありうるような場合に使用する。
    ```json
    // 操作時に付与されるタグのキーすべてが["Env", "CostCenter"]に含まれる場合（ただしタグキーがない場合もOK）
    {
      "ForAllValues:StringEquals":{
        "aws:TagKeys": ["Env", "CostCenter"]
      }
    }
    ```
      - 上記で`ForAnyValues`の場合は、操作時に付与されるタグのキーの１つ以上が["Env", "CostCenter"]に含まれる場合
  - 参考
    - [IAM タグベース制限ポリシーを作成する](https://aws.amazon.com/jp/premiumsupport/knowledge-center/iam-tag-based-restriction-policies/)
    - [Condition Operatorに使える条件一覧](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html)
    - [複数のキーまたは値による条件の作成](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/reference_policies_multi-value-conditions.html)

- 参考
  - [IAMロール徹底理解 〜 AssumeRoleの正体](https://dev.classmethod.jp/articles/iam-role-and-assumerole/)
    - STSを使ったAssumeRoleの仕組みが良く分かる。

### AWS Organizations

- 複数のAWSアカウントを管理するサービス。

- SCPでアクセス権限のコントロールを行う。ホワイトリスト形式のポリシー。

- デフォルトでは、SCPは`FullAWSAccess`が設定されているため、制限するためにはこのポリシーのデタッチが必要。

- SCPが設定がされたOU(Organization Unit)のアカウントは以下が行える。
  - ポリシー内で許可したアクションを、IAMポリシーで権限付与が実行できる。

- AWS Resource Access Manager (AWS RAM)
  - アカウント間でリソース共有を行うためにはこちらを使用する。

- 組織からメンバーアカウントの削除
  - 請求情報へのIAMユーザアクセスが有効となっている必要がある。

- SCPの範囲
  - 特定のサービスにアタッチ済みのIAMロールには影響を与えないので注意する。

- マスターアカウントでメンバーアカウントのリソースを管理する方法
  - 新規メンバーアカウントの場合
    - メンバーアカウントをOrganizationsのコンソールで作成するとOrganizationAccountAccessRoleが自動生成される。
    - マスターアカウントに対してクロスアカウントアクセスを設定する。
  - 既存メンバーアカウントの場合
    - OrganizationAccountAccessRoleが生成されない。
    - そのためまず、メンバーアカウントをマスターアカウントに招待する。
    - そのうえで、マスターアカウントに対してOrganizationAccountAccessRoleをクロスアカウント権限で付与することが必要。

- リザーブドインスタンスの共有
  - マスターアカウントでRIの共有設定を有効化することで、アカウント間でRIの使用を共有できる。
  - 共有したくない場合は無効化するが、その分請求が高くなる可能性がある。
  - また共有できるのは、おなじAZのインスタンスのみである。

- CloudTrailとの統合
  - 組織にたいするCloudTrailの証跡を有効化することで、全アカウントでの証跡有効化をシンプルに実施できる。
  - SCPでも設定が可能だが、CloudTrailのみであれば統合機能を使う方がよりシンプルでベストな選択である。

### AD関連

- AD Connector
  - 既存のADを使って、AWS環境へのアクセスを可能にしたり、IAMによるユーザー管理する。

- Simple AD
  - ADを作成するサービス
  - 簡易にAmazon Workspaceに認証・アクセスできる。

- AWS Managed Microsoft AD
  - フル機能のMicrosoft Active DirectoryをAWSで使用できる。
  - SAMLなどのフェデレーションしたり、オンプレとのADの連携も可能。
  - 既存のADワークロードをAWSに移行する場合は、こちらを利用する。

### AWS Single Sign-On (SSO)

- 複数のAWSアカウントやビジネスアプリケーションへのSSOアクセスを簡単に一元管理できるクラウドSSOサービス。
- Organizationsすべてのアカウントの一元管理も可能
- AWS SSOで構成する資格情報、または既存の社内認証情報を使用して再インできる。

### AWS Service Catalog

- 組織としてのガバナンスが適用されたテンプレートを、AWS利用者であるユーザー部門に利用させることができるサービス。
- Service Catalogは、CloudFormationテンプレートを製品としてインポートする事が出来ます。
- CloudFormationテンプレートには、多くのAWSサービスの構成情報を記載できます。
- これにより、スタンプを押すように統一的な環境を作成する事が出来ます。
- 参考
  - https://dev.classmethod.jp/articles/serca/

### AWS Systems Manager

- Systems Manager Automation
  - メンテナンスやデプロイタスクを自動ワークフロー化できる。
  - 定義済みのワークフローを使うこともできる。
    - EC2インスタンスの再起動
    - AMIの作成、など

- Systems Managerコンソール
  - ワークフローの進行状況を確認できる。

- AWS Systems Manager エージェント(SSMエージェント)
  - System Managerがリソースを管理できるようにするためのエージェント。
  - EC2インスタンス、オンプレサーバーなどにインストールして使用する。

* AWS Systems Manager Patch Manager
  * パッチ適用のプロセスを自動化する。
  * インスタンスをパッチグループで分類して管理することができる。

* AWS Systems Manager State Manager
  * 安全でスケーラブルな設定管理サービス
  * Amazon EC2 およびハイブリッドインフラストラクチャを、定義された状態に保つプロセスを自動化します。
  * シェルスクリプトによって、午前0:00にCE2インスタンスからS3バケットにログを取得する設定が可能です。 
---
## Computing

### EC2

- インスタンスファミリー
  - 汎用: T,M,A
    - T: Turbo. バーストタイプ
    - M: Most scenarios. 標準的なやつ
    - A: Arm. ARMプロセッサタイプ(AWS Graviton)
    - Mac: Apple Mac Mini搭載
  - コンピューティング最適化: C
    - C: Compute. 計算パフォーマンスが高い。
  - メモリ最適化: R,X,Z
    - R: RAM. メモリ最適化
    - X: Extra large memory. 最大メモリ量が大きい
    - Z: Hz. 高クロックなコア搭載モデル。
  - 高速コンピューティング: P,G,F,Inf,etc
    - P: general Purpose. 汎用GPU搭載
    - G: Graphics. グラフィックス特化GPUタイプ
    - F: FPGA. FPGAモデル
    - Inf: Inference. 機械学習推論に最適化されたタイプ。AWSが開発した Inferentia チップが搭載。
    - Trn: Trainium. AWSが開発したML用チップ Trainium 搭載タイプ
    - DL: Deep Learning. Gaudiアクセラレータ搭載タイプ
    - VT: Video Transcoding. 最大4K解像度に対応したリアルタイムトランスコーディングが可能なタイプ(Xilinx U30 Acceralatorが搭載)
  - ストレージ最適化: I,D,H
    - I: IO Performance. NVMe SSD搭載でIO性能が高い
    - D: Dense storage. 最大48TBのHDD搭載
    - H: High disk thoughput. 高スループットタイプ。これもHDD。
  - 参考
    - https://otomosa.com/aws/post-1870/
    - https://aws.amazon.com/jp/ec2/instance-types/

- 購入方法
  - オンデマンド
  - リザーブド
  - スポット
  - オンデマンドのキャパシティ予約 + Savings Plans

- リザーブド・コンバーティブル
  - インスタンスファミリー・OS・テナンシー・支払いオプションを変更可能。
  - スタンダードでも、AZ・インスタンスサイズ・ネットワークタイプは変更できる。

- 物理専有型
  - ハードウェア専有インスタンス(Dedicated Instance)
    - 専用HWのVPCで実行されるEC2インスタンス。
    - VPC構成をする際にdedicatedというのを選ぶと選択することができる。
    - 他のAWSアカウントから分離したインスタンスとなるが、同じアカウント内では共有する可能性がある。
    - またハードウェアを専有できるが、どのハードウェアで起動するかは指定することができない。
  - Dedicated Host
    - 同じアカウント内でも共有しない設定が可能なインスタンス形式。
    - IAMグループなどで閉じたインスタンスにすることができる。
    - 用途としては、オンプレのライセンスサーバーなどをAWSに移行したい場合など。
    - ホストのアフィニティ設定をhostにしておくと、停止して再起動した場合でも同じハードウェアを利用できる。
  - ベアメタル(Bare Metal)
    - サーバーのProcessorやMemoryにアクセス可能なインスタンス。
    - 下層のハードウェアレベルまでアクセス可能。

- ユーザーデータ
  - 起動時に実行したいコマンドを記述することができる。

- 起動設定と起動テンプレート
  - 起動設定は、AMIが変更されると再作成が必要、バージョン管理が不可など機能が少ない。
  - 起動テンプレートはバージョン管理が可能。AMIと独立して設定ができる。
    - AMIは「起動テンプレートに含めない」という設定が可能。
  - 双方とも、Auto Scalingグループに紐づけする。
  - そのAuto ScalingグループをELBに紐づけすることが可能。S

- インスタンス間のネットワーク高速化
  - クラスタープレイスメントグループを設定する。
  - 拡張ネットワーキングをサポートするインスタンスタイプを選択
  - 拡張ネットワーキングの種類は以下の通り
    - ENA (Elastic Network Adapter)
      - 最大100Gbpsを実現するための拡張ネットワーク
    - Intel 82599 Virtual Function (VF) インターフェイス
      - 最大10Gbpsを実現するための拡張ネットワーク
  - 拡張ネットワーキングの方式のことを、シングルルート I/O 仮想化 (SR-IOV) とも呼ぶ。

- プレイスメントグループ
  - プレイスメントグループは設定後に、起動するという手順となる。
  - 異なるインスタンスタイプをグループにすることはできない。
  - インスタンスを追加する場合は、一旦プレイスメントグループを停止する必要がある。
  - 種類
    - クラスタープレイスメントグループ
      - パフォーマンス向上が目的。単一AZ内でグループ化し、複数のVPC Peeringにまたがることも可能。
      - グループ内のインスタンスは、TCP/IPトラフィックのスループット上限が高くなり、インスタンス間通信の速度が向上する。
    - パーティションプレイスメントグループ
      - 耐障害性が目的。
      - 複数パーティションに分けられ、パーティション毎にラックがあり、パーティション同士はラックを共有しない。
    - スプレッドプレイスメントグループ
      - 更なる耐障害性が目的。
      - パーティションあたり1インスタンス構成となり、異なるラックにそれぞれのインスタンスを配置できるグループ。
  - その性質上、複数のAZには構成できないため注意する。

- VM Import/Export
  - オンプレ環境の仮想マシンをAWSにインポートする機能

- store-backed / EBS-backed
  - store-backedはインスタンスストアがroot volumeのもの。
  - 停止すると、インスタンスストアのデータは自動的に削除される揮発型。

* store-backedなEC2のバックアップ
  * AMIを作成する必要がある。 ec2-bundle-volやec2-upload-bundleなどのAMIツールが必要です。
  * EBS-backedとは異なり、EC2 CLIやマネジメントコンソールでは実施できない。

- キーペアの管理
  - AMIの複製では、キーペアはコピーされないため、既存のキーを使う場合には再度インポートが必要となる。

- 複数のサーバーSSL証明書の設定
  - SSL通信は、HTTP前段階で確率され、その際にSSLサーバー証明書も使用される。
  - HTTPの前段階ではホスト名ではなくIPアドレス等を使って通信されます。
  - そのため、SSLサーバー証明書はIPアドレス毎に一つまで有効となります。
  - EC2に複数設定したい場合は、複数のENIで各ENIにEIPを設定する必要があります。
  - 参考
    - [1台のWebサーバで複数の証明書を運用する際の注意点は？ | SSLサーバ証明書のクロストラスト](https://xtrust.jp/support/faq/faq09/a008/)

- クライアント側のSSL証明書設定
  - Webサーバーとの直接的なTCP通信が必要となるので注意する。
  - そのためELBは、HTTPSではなくTCPで設定する必要がある。

* Bashスクリプトの設定
  * OSのセッティング等に使用する。

* HVM AMI
  * 完全に仮想化された一連のハードウェアを備えており、イメージのルートブロックデバイスのマスターブートレコードを実行することによって起動します。
  * ホストシステム上の基盤となるハードウェアへの高速なアクセスを可能にするハードウェア拡張を利用できます。
  * 現在はHVM AMIが推奨されており、対するものはPV AMI
  * 参考
    * [EC2の仮想化方式についてのおぼえがき - kasei_sanのブログ](https://blog.kasei-san.com/entry/2018/01/10/003933)

### EC2Rescue

* Windowsインスタンスで問題が発生している場合に使用するサービス
* 以下のようなユースケース
  * インスタンス接続できない
  * 起動に関する問題が発生していたりする場合
* 分析やトラブルシューティングのためにログの収集などを行える。
* 具体的には以下の機能があります。
  * Current Instance Option（ログインしているインスタンスに対する機能）
  * Capture Logs：ログ収集
  * Offline Instance Option（起動していないインスタンスに対する機能）
  * Diagnose and Rescue：問題を自動検出して修正することができる
  * Restore：レジストリのリストア
  * Capture Logs：ログ収集
* 参考
  * [Amazon EC2のWindows用復旧ツール『EC2Rescue』が利用可能になりました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-ec2-windows-ec2rescue/)

### ENI

- EC2インスタンスにアタッチするネットワークインターフェース。

- アタッチとして以下の種類がある。
  - コールドアタッチ
    - インスタンス起動時にアタッチする。
  - ウォームアタッチ
    - 停止中のインスタンスにアタッチする。
  - ホットアタッチ
    - runnning中のインスタンスにアタッチする。

- 複数アタッチすることで、それぞれをインターネット用、バックエンドとの通信用などに使い分けることも可能。

- フェイルオーバー
  - セカンダリENIを使うことにより、フェイルオーバー時に同一IPのインスタンスをフェイルオーバー先にすることが可能。
  - またENIにはセカンダリなプライベートIPv4アドレスも設定できるため、EIPを付け替えてことでもフェイルオーバー可能。

### ELB

- ELBのみでは、Auto Scalingは実施できないので注意する。

- スケールイン・アウトの繰り返し抑制
  - クールダウンタイマーの値を見直す。
  - デフォルト値は300秒である。
  - CloudWatchと連携して、スケールが設定されるがその際のアラーム閾値を見直す。

- スティッキーセッション
  - セッション中に同じユーザから来たリクエストを同一インスタンスで処理することが可能。

- クロスゾーン負荷分散
  - 複数のAZにまたがる分散を行うことができる。

- Connection Draining
  - 接続をオープンとしたまま、登録解除・異常なインスタンスへの送信を停止できる機能。
  - 登録解除の待ち時間として、タイムタイムアウトを設定できる(1～3600秒、デフォルト300秒)。
  - タイムアウトを過ぎると強制的に停止する。

- ステータスコードについて
  - [https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/](https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/)
  - HTTPCode_Backend_2XX, HTTPCode_Backend_4XX, HTTPCode_Backend_5XX
    - EC2インスタンスに基づくステータスコード
  - HTTPCode_ELB_4XX
    - 解釈不能なHTTPの場合、ELB時点でエラーとなる
  - HTTPCode_ELB_5XX
    - 502: 解釈不能なレスポンスがEC2インスタンスから来た場合、このエラーとなる。
    - 503: 様々な要因が考えられる。
      - ELBに登録されたインスタンスが無い場合
      - ELBに登録されたインスタンスがあるが、healthyなものがない場合
      - スケールアップ中で送信先インスタンスが切り替わり中の場合
      - 突発的な負荷増加でELBの待ち行列(surge queue)があふれた場合

- メトリクス
  - RequestCount
    - HTTPCode_Backend_XXXの合計数
  - SurgeQueueLength
    - ELB内の待ち行列にたまっているリクエスト数
    - 突発的なリクエスト増がない場合0を維持
  - SpilloverCount
    - HTTPCode_ELB_5XXが返った数

- クロスゾーン負荷分散
  - クライアントがDNSルックアップをキャッシュする環境では、クロスゾーン負荷分散が無効な場合いずれかのAZに不可が集中する可能性がある。
  - ALBでは常に有効となり無効にできない。
  - CLB, NLBは作成方法によっては無効となるので、明示的な有効化が必要になる場合がある。
    - NLBは必ず無効がデフォルトとなる。
  - 参考
    - [ELBの種類によるクロスゾーン負荷分散のデフォルト値調べ | DevelopersIO](https://dev.classmethod.jp/articles/elb_crosszone_load_balancing_default_value/)

- ソース情報の維持
  - ELBを経由すると通常ソースのIPなどの情報が失われる。
  - これを維持するためには以下を使用する。
    - X-Forwarded-For (XFF)
      - HTTPのレイヤではこれを使用する。
    - Proxy Protocol
      - TCPのレイヤではこれを使用する。
  - 参考
    - [Proxy Protocol とは？ - Qiita](https://qiita.com/miyuki_samitani/items/80353b1b22f5ee9c41a8)

- ELBとEIP
  - ELBにEIPを割り当てて使用することはできない。

- 参考
  - [ELBの挙動とCloudWatchメトリクスの読み方を徹底的に理解する](https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/)


### Lambda

- 制限
  - 一時ボリューム量(`/tmp`): 512MB
    - 2022/03/24のアップデートで、デフォルト512MB、最大10GBまでを設定可能となった(料金は必要)。
  - 同時実行数: 1000
  - 関数とレイヤーストレージ: 75GB
  - デフォルトタイムアウト: 3秒(最大実行時間は900秒(15分))

- Lambda Layer
  - Lambdaファンクション間で共通の処理をLambda Layerとして定義して参照できる。
  - 最大５つまでLaymbda Layerとすることが可能。

- ネットワーク
  - Lambdaはデフォルトではインターネット接続やAWSサービスにアクセスできる安全なVPCで関数を実行します。
  - 一方、ユーザーが指定したVPCで実行する場合は、VPCからアクセス権を付与される必要があります。
  - またこのVPCがプライベートサブネットである場合、NAT経由での返信処理が設定されていなければ、レスポンスを受け取れません。
  - 同様に、Lambdaのセキュリティグループのアウトバウンドトラフィックを設定する必要があります。

- リソースポリシーによる実行許可
  - Lambdaはリソースベースポリシーがあるため、実行の許可をこのポリシーに設定する必要がある。
  - 設定には、add-permission AWS Lambdaコマンドを使用する。
  - 参考
    - https://dev.classmethod.jp/articles/lambda-resourcebase-policy/

### Amazon ECS

- 権限付与
  - ECSにより起動するインスタンスへの権限は、ECSタスクにIAMロールを付与することにより行う。
  - 今まではEC2のIAMロールを使用する必要があった。

- 起動モード
  - EC2
    - EC2インスタンスを起動する。
  - Fargate
    - ECS・EKSで利用できる専用のコンピューティングエンジン
    - インスタンスの管理が不要(CPUやメモリなどを定義する)
    - 秒単位で数万個のコンテナ起動が可能

- トラフィック制御
  - ELBと連携して実施することができる。

- Capacity Provider Reservation
  - Auto Scalingグループを構成するために、Capacity Provider Reservationを使用する。

### Amazon EKS

- kubernetesを使用する際に使うサービス
- ECSと違う点は、kubernetesを活用した開発や管理をある程度自動化することができる部分である。

### AWS Batch

* データ分析のBashスクリプト処理をBatch実行するなどでも使用する。

### Auto Scaling

- 簡易スケーリングポリシー
  - ターゲット追跡スケーリングポリシーの通常設定
  - アラーム設定に基づき１段階のスケーリングを実施

- ステップスケーリングポリシー
  - アラーム超過サイズに基づいて、インスタンス数を動的に調整する、複数段階のスケーリングを実施
  - これにより、段階的なウォームアップ条件を設定可能

- 手動スケーリング
  - 希望容量を手動で調整する。

- スケジュールされたスケーリング
  - 実施日時を指定する。

- スケールに24時間失敗し続けると、AUto Scalingが停止する可能性がある。

- ヘルスチェック
  - ELBとEC2どちらを利用するか設定する。

- スケーリング時のメトリクス
  - CPU使用率を使う。メモリ使用率を使ったトリガーはデフォルトで設定できない。

### AWS Application Discovery Service (AWS ADS)

* 移行に際してオンプレミスサーバーに関する情報収集を行うサービス
* AWSで稼働させた場合の層所有コスト(TCO)などの見積もり、移行計画へ仕様ができます。

### AWS Application Migration Service (AWS MGN)

- オンプレの仮想マシンをAWSに移行するツール
  - VMware vSphere
  - Microsoft Hyper-V/SCVMM
  - Azure 仮想マシン

- 旧サービスのAWS Server Migration Serviceともども、仮想マシンではないものの移行はできないので注意する。

- AWS Replication Agent 
  - 移行元となるソースサーバーにインストールするエージェント
  - レプリケーション設定の表示・定義ができる。
- 旧サービスは、AWS Server Migration Service(SMS)だが、2023年3月31までで使えなくなる。

### AWS Migration Hub 

* AWSおよびパートナーの複数のソリューション間における移行の進行状況を追跡できるサービス。
* 最も適した移行ツールを選択でき、全体の移行状態の可視化が可能です。 

### VM Import/Export

- 仮想マシンをEC2にいこうするためのサービス
- 似た名前として AWS Import/Exportというものがあるが、ストレージ転送のサービスであり、現在は利用されないので注意する。

### AWS License Manager

- ベンダーが提供するライセンス管理を行うサービス。
- 契約条件に基づくルールを作成することで、ライセンス違反を防ぐことが可能。
- 違反する場合は、インスタンスの起動を停止したり、管理者に侵害を通知できる。

### 移行パターン

* Rehost
  * 最も変更の少ない移行パターン。オンプレサーバーは基本すべてEC2みたいな。
* Replatform
  * クラウドのサービスを少し使用したパターン。DBはRDSを、アプリはBeanstalkでデプロイなど。
  * まだコード等は変更しない。
* Refactor / Re-architect
  * よりクラウドサービスを使用する。必要に応じて構成を大きく変更する。
  * サーバーレスやコンテナ、ELBなどなど。
* Re-purchasing
  * 移行元のレガシーアプリケーションの一部をSaaSに置き換える。
* Retaining
  * 移行元の複雑な部分を一部オンプレミスに残す。
* Retire
  * アプリケーションを廃止する。

* 参考
  * [クラウドへの移行とは？意味や仕組みをわかりやすく解説！ | ブログ | CMC Japan株式会社](https://cmc-japan.co.jp/blog/what-is-migration-to-the-cloud-a-simple-explanation-of-what-it-means-and-how-it-works/)

---
## Security

### AWS STS

- スイッチロールなどに使用
- またモバイルアプリケーションで一時的な認証情報を使用する際にも使用可能。
- SAML2.0をサポート
  - 異なるドメイン間でユーザー認証を行うためのXMLベースの標準規格。
  - SSOなどの要件に利用される。

### AWS Key Management System (KMS)

* マスターキーとデータキーがある。
* マスターキーはデータキーを暗号化するもの。
  * 大事なもののためexportできない。
  * ユーザーには暗号化済みのデータキーと平文のデータキーがexportできる。
* データキーでユーザーは暗号化ができる。
  * 暗号化されてないデータキーを使用する。そして使用後は破棄する。
  * 暗号化済みのデータキーは保持する。
* 復号時は、暗号化済みのデータキーをKMSに処理させることで、平文のデータキーを取得する。
* マスターキーは１年毎にローテーションする設定をすることが可能。
  * この場合でも古い暗号化済みデータキーは、古いマスターキーで復号可能。

* 参考
  * [10分でわかる！Key Management Serviceの仕組み #cmdevio | DevelopersIO](https://dev.classmethod.jp/articles/10minutes-kms/)
### HSM

* Hardware Security Module
* 不正使用防止策の施されたハードウェアデバイス内での、安全なキー保管と暗号化操作が可能になります。
* これはデータ暗号化に利用される仕組みです。
* 厳しいセキュリティ要件を満たすことができ、FIPS 140-2 Level 3に準拠している。
* HSMはゼロ化してキーをロスすると、コピーを有していない場合は、新しいキーは取得不可能となる。

### AWS WAF

- Web ACLを用いてHTTPリクエストレベルでの制限・許可などを行う。
  - 特定のリクエスト以外を許可（攻撃を遮断）
  - 特定のリクエストのみを許可（アクセス制限：日本国内のみ）

* 行える許可または拒否は以下の通り
  * 送信元の制限（特定のIP、もしくはIP範囲、特定の国）
  * リクエストの特定部分が、指定文字列を含む、もしくは正規表現と一致すること。
  * 指定した長さを超過していること。
  * SQLインジェクションの可能性がある。
  * XSSの可能性がある。
  * または上記の組み合わせ、および５分間に渡り、指定数以上のリクエストを超えるリクエスト

- Referer制限
  - 直前に参照していたURLに基づいて制限を行う。

* WAFサンドウィッチ方式
  * Webとアプリの２層構造の場合、Web層とアプリ層の間にWAFを設置する。
  * AWS WAFが無かった自体の話のようにも見えるが、両方の選択肢がある場合はサンドウィッチ方式を選択する方が無難か。

- ルールの更新
  - S3にCloudFrontなどのログを保存し、ログ保存イベントでLambda関数でログを解析し、ルールを更新するなどの自動化処理を実装できる。

### Amazon Inspector

- セキュリティ評価を自動で実施するサービス
- アプリケーションに対して、脆弱性やべくとプラクティスからの逸脱がないかなどを自動で評価できます。

### AWS CloudTrail

- アカウントのガバナンス、コンプライアンス、運用監査、リスク監査を行うサービス。
- AWS Organizationsを利用中の場合、すべてのAWSアカウントのログをまとめて取得することが可能。
  - マスターアカウントの組織の証跡を有効とすることで、すべてのアカウントのCroudTrailイベントを同じS3バケット、CloudWatch Logs、CloudWatchイベントに配信できる。
- AWS Organizationsを使用しない場合は、各アカウントで組織の証跡を有効化する必要がある。
- CloudTrailは、IAMユーザーやIAMロール経由でサービスに実行されたアクションやAPI実行を記録するものであり、リソースの変更を記録する場合はAWS Configを使用する。

- CloudTrail Insights
  - CloudTrailのログの定期的な監査を行うツール。

* Step Functionsとの統合
  * Step Functionsの人の手作業のによるアクティビティの記録などには、CloudTrailが必要となる。

### AWS Certificate Manager (ACM)

- SSL証明書を集中管理するためのサービス。
- ELB、Route53、CloudFrontなどとの組み合わせとしてよく出題される。

- ACMがサポートされていないリージョンでは、IAMをCertificate Managerとして使用する必要があります。
  - 具体的には以下の手順で行います。
    1. SSL証明書をIAMにアップロードする。
    2. `get-server-certificate`コマンドにより証明書のARNを取得する。
    3. `set-load-balancer-listener-ssl-certificate`コマンドにより証明書を設定する。

- 権限の分割
  - EC2の管理者権限が開発チームにある場合、セキュリティチームのみが管理できるようELBにSSL証明書を設定する必要がある。

- IAMポリシー
  - 証明書へのアクセス権限設定は、ACMとELB(またはEC2)双方へ設定が必要。

- カスタム証明書
  - 独自ドメインを使用する場合はそのドメインに対応したカスタム証明書を使用する。

### AWS Shield

- DDoS攻撃を緩和するサービス。

- DDos攻撃の例
  - SYNフラッド
    - 送信元を偽造してTCPのSYNパケットを送り続けることで、サーバー側の接続リソースを枯渇させる方法
    - [SYNフラッド](https://www.f5.com/ja_jp/services/resources/glossary/syn-flood)
  - UDPリフレクション攻撃
    - 大量のサーバー群に対して攻撃を指示し、ある特定の送信元(攻撃対象)に偽造して、あるサーバーにUDPリクエストを大量に送りつける
    - そしてリクエストの応答を、偽造したある特定の送信元にすべて集中させることでダウンさせる方法
    - [DDoS攻撃の一種である「リフレクション攻撃」とは？被害や対策例をご紹介 - カゴヤのサーバー研究室](https://www.kagoya.jp/howto/engineer/infosecurity/reflection-ddos-attacks/)

- Standardでは、リアルタイム通知や可視化機能が提供されない。その場合はAdvancedとする必要がある。

- CloudFrontとの関係
  - CloudFrontでは、デフォルトでAWS Shield Standardが適用されている。

### AWS Secrets Manager

- セキュアな資格情報を保持するために使用するサービス。

### AWS Config

- リソースの変更管理が可能

- リソースの設定変更の継続的なモニタリングが可能でコンプライアンス評価が可能。

- APIコールの記録はCloudTrailを使用する。

- 変更のモニタリングはCloudWatch Eventsを使用する。
  - 参考
    - [特定のリソースIDの変更前と変更後をメールで通知する方法 | DevelopersIO](https://dev.classmethod.jp/articles/email-specific-resource-id/)

- WAFなどのFirewallルールの変更も追跡できる。

- AWS Organizationsにおける複数アカウントについてもコンプライアンス管理が可能。

- サードパーティのリソース管理なども含まれる。

- 参考
  - https://www.yume-tec.co.jp/column/series/aws%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E3%82%92%E6%8E%A1%E7%94%A8%E3%81%97%E3%81%9F%E3%81%84%E4%BA%BA%E4%BA%8B%E6%8B%85%E5%BD%93%E5%90%91%E3%81%91%E3%81%AEaws%E5%85%A5%E9%96%80/4621

---
## Messages

### Amazon SQS

- 制限
  - キューの保持期間はデフォルト4日間。最大で14日(2週間)。
  - 保存できるメッセージの最大数は無制限
  - メッセージのサイズは256KB。
    - 拡張クライアントライブラリを使うと2GBまで可能。

- キューの削除
  - キューは明示的に削除しない限り、残り続ける。
  - また可視性タイムアウトが設定されている場合は、有効期限が過ぎれば別のインスタンスでキューが処理される。
  - 失敗し続けた場合は、デッドキューに移動する設定を行うことができる。

- Auto Scaling
  - キューの深さに応じてEC2などのリソースをスケールアウトすることが可能。

* メッセージグループ
  * メッセージグループIDはFIFO配信を支援する機能です。
  * これによって、 同じメッセージグループに属するメッセージは、常にメッセージグループに対して厳密な順序で1つずつ処理されます。

* デッドレターキュー
  * 長時間実行されなかったキューをデッドレターキューとして隔離して、キューがたまらないようにする仕組み

* 可視性タイムアウト
  * あるコンシューマーが処理中のものは、他のコンシューマーから見えない状態にし、重複処理をさける仕組み

* 遅延キュー
  * キューへの配信う数秒延期することが可能。

### Amazon Simple Notification Service (SNS)

- push型の通知サービス
- リソース間のイベント通知、モバイルへのプッシュ通知などが用途となる。
- SNSからSQS, SES, Lambdaへの通知も行う用途で使用する。

- SQSを直接使わずにSNSを使用すると拡張性が高くなったりするというノウハウもある。
  - [【AWS】SQSキューの前には難しいこと考えずにSNSトピックを挟むと良いよ、という話](https://dev.classmethod.jp/articles/sns-topic-should-be-placed-behind-sqs-queue/)

- 特定の宛先への通知停止方法
  - 管理者側でサブスクリプションを削除する。
  - または、受信者自身で購読解除オプションから解除することが可能。
  
- イベントソース
  - アプリケーション統合
    - CloudWatch Events (Amazon EventBridge)
    - Step Functions
  - 参考
    - [Amazon SNS イベントソース - Amazon Simple Notification Service](https://docs.aws.amazon.com/ja_jp/sns/latest/dg/sns-event-sources.html)

### Amazon SES

- マネージドなメールサービス
- イベントに応じてメール配信をする際は、SNS -> SESという形で構築する。

### Amazon MQ

- 業界標準のメッセージングAPIとブローカを提供するサービス。

---
## Workflow

### AWS Step Functions

- サーバレスのオーケストレーションサービス
- Lambda関数などのAWSリソースを組み込んだり、人手によるアクションをタスクに組み込むことができる。
- JSON形式でステートマシンを定義する。
- 最長１年間実行可能。
- プロセスに親子関係がある場合は、SWFを選択する。(Step FUnctionsで対応できない)
* CloudTrailとの統合
  * Step Functionsの人の手作業のによるアクティビティの記録などには、CloudTrailが必要となる。

### Amazon SWF (Simple Workflow)

- 旧型のワークフローシステム。
- 利用が水使用されていないため、ほぼ正解の選択肢にはならない(Step Functionsがない場合は選択肢になるかも)
- プロセスに親子関係がある場合は、SWFを選択する。(Step FUnctionsで対応できない)

---
## IoT

### AWS IoT Core

- インターネット接続されたデバイスから、クラウドやその他のデバイスに簡単かつ安全に通信するためのマネージド型サービス。
- センサーデバイスを利用した車両管理アプリケーションを容易に構築することが可能。
- 数十億個のデバイスと数兆件のメッセージをサポート。

---
## ML

### Amazon Macie

- S3内の機密データを検出・分類・保護できるフルマネージド型サービス

---
## CV

### Elastic Transcoder

- 動画データを様々な形式にトランスコーディングできる(MP4、HLS: HTTP Live Streaming)

### Amazon Video Streaming

- 動画をストリーミング配信するためのサービス

### Amazon Rekognition

#### Amazon Rekognition Video

- ビデオストリーミングをリアルタイム解析可能なAIサービス。
- ストリーミングデータだけではなくS3に保存した録画データも解析することが可能。