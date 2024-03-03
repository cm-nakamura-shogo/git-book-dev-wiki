# DAS-C01

# 教材

### Udemy

- [https://classmethodjp.udemy.com/course/practice-exams-aws-certified-data-analytics-specialty](https://classmethodjp.udemy.com/course/practice-exams-aws-certified-data-analytics-specialty/learn/quiz/5450714/result/1183237122#overview)
    - 演習テスト1(10問) : 済（正解 5 of 10）
    - 演習テスト2(65問)
    - ※演習テスト2は順番がランダムに変わるため一気に受けた方が良いかも

### BlackBelt

- Athena : https://d1.awsstatic.com/webinars/jp/pdf/services/20200617_BlackBelt_Amazon_Athena.pdf
- Redshift : https://d1.awsstatic.com/webinars/jp/pdf/services/20200318_AWS_BlackBelt_Redshift.pdf
- Lakeformation : https://d1.awsstatic.com/webinars/jp/pdf/services/20191001_BlackBelt_LakeFormation_A.pdf
- QuickSight : https://d1.awsstatic.com/webinars/jp/pdf/services/20200204_AWS_BlackBelt_QuickSight_Update.pdf
- EMR : https://d0.awsstatic.com/webinars/jp/pdf/services/20161026_AWS-BlackBelt-EMR.pdf
- Glue : https://d1.awsstatic.com/webinars/jp/pdf/services/20210330_AWSBlackBelt2021_AWSGlueStudio.pdf
- Kinesis : https://d1.awsstatic.com/webinars/jp/pdf/services/20180110_AWS-BlackBelt-Kinesis.pdf
- Kafka : https://d1.awsstatic.com/webinars/jp/pdf/services/20191120_AWS-BlackBelt_AmazonMSK.pdf
- DMS : https://d1.awsstatic.com/webinars/jp/pdf/services/20210216_Blackbelt_DatabaseMigrationService.pdf
- OpenSearch : https://pages.awscloud.com/rs/112-TZM-766/images/AWS-Black-Belt_2023_Amazon-OpenSearch-Service-Basic_0131_v1.pdf

### 体験記

- https://classmethod.slack.com/archives/C015C8T2JT0/p1635410937002100

# Amazon Athena

- データソース
    - デフォルトはGlue Data Catalog
    - Hive Metastoreが既存である場合はそちらをLambdaで接続して取得することも可能
- パーティショニング
    - スキャンされるデータの量を制限できるため、パフォーマンスが向上し、コストが削減
    - パーティショニングはパーティション数が限られており、カーディナリティが低い列に設定（例：日付）
    - CTASやINSERT INTOで作成できるPartition数は100という上限がある
    - 1テーブルあたりの最大パーティション数も10,000,000
    - カラム名あり(Hive形式)とカラム名なしがある
        - Hive形式はMSCK REPAIR TABLEが使用できる
- バケッティング
    - バケッティングとは複数のノードで水平分散処理を行えるよう、データファイルをキーとファイル数を指定して分割するAmazon Athenaの機能
    - バケッティングはカーディナリティが高く均一に分散した列に設定（例：ユーザID）
    - バケッティングにより個々のファイルサイズを128-512MBなどのちょうどよいサイズに制限できる
    - パーティションと同時に使用する場合は、パーティション内のファイル数がバケッティングで指定した数になる
    - INSERT INTOには対応できない
- Partition Projection
    - パーティション管理を自動化できる
    - 非常に多くのパーティションがあるテーブルに対するクエリ処理を高速化できる
        - Athena自身がPartitionの情報を持つためGlue Data Catalogに対するGetPartitionsの呼び出しをしなくて良くなるため
- フォーマット
    - parquetの他、ORCもデータの高速取得用に最適化され、AWS 分析アプリケーションで使用される列形式のストレージ形式という扱い
    - ORCはHive向きの最適化、ParquetはSpark向けと言えるらしい
    - AVRO形式は行指向フォーマット
- パフォーマンス向上
    - スキャン量の削減 : 列指向、圧縮、パーティショニング
    - スキャンするファイルを一定サイズ(ex. 128MB以上)にまとめる : バケッティング
    - ファイルを分割可能な形式とする
- 使用量制限
    - Athena では、クエリごとの制限とワークグループごとの制限という 2 種類のコスト制御を設定可能
    - ワークグループ全体のデータ使用量制御制限では、指定期間中に実行されるクエリのスキャン量を制限できる
- Federated Query
    - DynamoDB、Redshift、Audora、DocumentDB、ElasticCacheなどにSQLクエリを実行可能
    - AWS Lambdaで動作するコネクタを利用して実行する

# Amazon Redshift

- 「高いパフォーマンス」「複雑な分析クエリ」などと言われる場合はAthenaよりRedshiftが選択肢
- データ分散
    - JOINする行が他のテーブルのJOINする行とすでにノード上に配置されているような方法で分散する必要がある
    - ALL 分散スタイルを使用すれば、結合したいテーブルと併置できない場合でもパフォーマンスを向上できる
    - ALL 分散を使用すると、ストレージ容量の要件が増大し、ロード時間とメンテナンス操作が増加することには注意が必要
- Redshift Spectrum
    - S3 内の履歴データ全体をクエリ可能
    - 同時実行性も高く、任意の数のクラスターから S3 データにアクセス可能
- クロスリージョンスナップショット
    - KMSキーはリージョンに固有であるため、宛先リージョンでKMSキーを作成する必要がある
- 監査ログ
    - クラスターでのログ記録を有効にすると、Amazon S3 へのログ記録のみが有効となる
    - 現在、監査ログには Amazon S3 管理キー (SSE-S3) 暗号化 (AES-256) のみを使用可能
        - SSE-KMSは使用できない
    - 監査ログはデフォルトでは有効になっていない
- VACCUM
    - テーブルの行を削除または更新するたびに空きスペースができるがRedshift は空きスペースを自動的に再利用しない
    - VACCUM操作をすると行が再ソートされ、指定されたテーブルまたは現在のデータベース内のすべてのテーブルのスペースが再利用できる
- スライス
    - 各ノードはさらにスライスに分割され、スライスには１つ以上の専用コアがあり、均等な処理能力を持つ
    - そのため、Redshift にデータをロードするときは、各スライスが同じ量の作業を実行するようにする必要がある
    - データ ファイルを分割するときは、圧縮後のサイズがほぼ同じ (1 MB ～ 1 GB) になるようにし、ファイル数はクラスター内のスライス数の倍数である必要がある
- 一時ステージング テーブル
    - Redshift の一括 ETL を実行する場合、変換用のデータを保持するために一時ステージング テーブルを使用することが推奨
    - これにより、これらの大量のデータセットを Amazon Redshift に効率的かつ高速に転送できるように
    - これらのテーブルは、ETL セッションの完了後に自動的に削除される
- 列レベルのアクセス制御
    - GRANT文で行うのが推奨で、VIEWを作成することは非推奨とのこと

# Amazon EMR

- Apach Hiveをネイティブにサポートし、Apach Hiveクラスタを迅速かつ簡単に構成可能
- Apache Hive は、データ ウェアハウスのようなクエリ機能を提供する、オープンソースの分散型フォールト トレラント システム
- ユーザーは SQL のようなインターフェイスを使用してペタバイト規模のデータの読み取り、書き込み、管理が可能
- マスター ノード、コア ノード、およびタスク ノード
- クラスターには、最大 50 個のインスタンス グループを含めることができ、マスターインスタンスグループ、コアインスタンスグループ、48個のタスクインスタンスグループが構成できる
- メモリに応じたスケーリング
    - オートスケーリングをする場合、例えば「YARNMemoryAvailablePercentage」をメトリクスとして使用すれば、メモリ使用量に応じたスケーリングが可能
    - 「CapacityRemainingGB」は残りのHDFSディスク容量を表し、クラスタの健全性を判断できるが、スケーリングには使用できない
- S3DistCpについて
    - Amazon S3とAmazon EMRクラスタ間でデータをコピーする用途に使用
    - S3DistCpを使用すると、Amazon S3からHDFSに大量のデータを効率的にコピーすることができる
    - S3DistCpはAmazon S3バケット間、またはHDFSからAmazon S3にデータをコピーすることも可能
- AZ冗長
    - EMR クラスターは単一のアベイラビリティーゾーンにのみ存在できる
- EMRFSとHDFSの違い
    - EMRFSはクラスターが通常のファイルを Amazon EMR から Amazon S3 に直接読み書きするために使用する HDFS の実装
    - EMRFSはオブジェクトストレージであり、EMRFSはクラスターが終了した場合でもデータが保持される
    - 一方、HDFSは保持されない一時的な領域

# AWS Glue

- Glue Crawler
    - S3などのデータストアに接続し、データのスキーマを決定し、AWS Glue データカタログにメタデータテーブルを作成する昨日
    - データストアのリージョンはあまり関係ない
    - スケジュール実行による定期実行、またはS3 バケットのイベント通知によってトリガーされる Lambda を使い、Crawlerをオンデマンドで呼び出すことが可能
    - 異なるスキーマのデータが同一フォルダにある場合
        - 同一フォルダでもスキーマの一致度合が70%を下回る場合は、異なるスキーマと解釈されて別テーブルと見なされる
- Job Bookmark
    - ジョブが実行されるたびに更新される、処理されたデータを追跡する機能
    - データソースがJDBC(RDB)とS3の２種類で挙動が少し異なる
    - JDBC(RDB)
        - 同じデータソースの後続のジョブは最後のcheckpoint以降に新しく追加されたデータのみを処理する
        - ブックマーク機能が正しく動作するためには、データベースのテーブルにプライマリキーが設定されていることが必要
    - S3
        - S3 オブジェクトの最終更新日時を確認し、前回のジョブ実行以降に変更されたオブジェクトを再処理する必要があるかどうかを判断
    - 重複をさせないためには
        - 最大同時実行数を1に設定する必要がある
        - job.commitが漏れていないかの確認
    - 参考
        - [AWS Glue ジョブのブックマーク機能の基準と留意点を教えてください | DevelopersIO](https://dev.classmethod.jp/articles/tsnote-awsglue-job-bookmarks-difference-standard-and-important-point/#toc-4)
- 大規模なJDBCテーブルの移行
    - ジョブが失敗する場合は、JDBCテーブルを並行して読み取る
    - データを分割するオプションを使用し、hash fieldに値が均等に分布している列を選択する
- ワーカータイプ
    - メモリを大量に使用するジョブの場合、ワーカー タイプを標準からG.1X または G.2X に変更できる
- DPU
    - 単一のデータ処理ユニット (DPU) は、4 つの vCPU と 16 GB のメモリを提供
- データソースとAthenaからの見え方の違い
    - GlueはS3、RDSやDynamoDBなど様々なデータソースを指定できる
    - 一方AthenaはS3をデータソースとするGlueテーブルのみを表示でき、またXMLなどもGlue側からしか見れない
- Glue Studio
    - ETL ジョブの作成、実行、監視を容易にする視覚的なインターフェース
- Glue Custom Connectors
    - ネイティブにサポートされていないデータストアとの接続
    - SaaSや他クラウドのサービス（Snowflake、BigQuery）
- Glue DataBrew
    - 分析および機械学習のためのビジュアライズツール
- Glue Elastic Views
    - 複数のデータソースにまたがるマテリアライズドビューを作成

# AWS Data Pipeline

- RDSからS3のエクスポート、増分コピーなどに用いられるサービス
- S3からRedshiftなどのロードも可能

# AWS Data Migration Service (DMS)

- AWS DMSは、データベースを AWS に移行するのに役立つサービス
- SQL Server から Aurora へなど、異なるデータベース プラットフォーム間の移行もサポート
    - Source : RDB、NoSQL(MongoDB、Cassandra)、S3、Snowball、Teradata
    - Target : AUrora、DynamoDB、DocumentDB、OpenSearch Service、KDS、Kafka、KDS、Redshift
- Amazon Redshift にレプリケートする移行タスクでも使用される
- バッチ実行時の挙動
    - バッチ実行に失敗した場合でもAWS DMS はバッチを分割し、1 つずつモードに切り替えてトランザクションを適用
    - 失敗の原因となったトランザクションを検出すると、AWS DMS はそのトランザクションを Amazon Redshift ターゲットの awsdms_apply_Exceptions テーブルに記録
    - 最後に、AWS DMS は新しいバッチのバッチ適用モードに戻る
- 移行前評価
    - データベース移行タスクの指定されたコンポーネントを評価して、移行タスクが期待どおりに実行できない可能性がある問題を特定する
- DMS データ検証
    - データがソースからターゲットに正確に移行されたことを確認し、ソース レコードとターゲット レコードを比較し、不一致があればレポートする
    - さらに、CDC（Change Data Capture）が有効なタスクの場合、AWS DMS は増分変更を比較し、不一致があればレポートをすることも可能

# AWS Lake Formation

- セキュアなデータレイクを構築するサービス
- ストレージとしてはS3が使用され、データ取り込み・構造化、セキュリティコントロール、データカタログ、監視・監査などが可能
- データ取り込み・構造化
    - Lake Formation は Glue の拡張機能と言え、セキュリティ強化やブループリントによるデータ取り込みなどでより便利に Glue の機能を使えるようになっている
    - Lake Formationのデータカタログは、Hive メタストアで行うのと同じ方法で、AWS でメタデータを保存、注釈付けができる
    釈付け、共有できる
- セキュリティコントロール
    - これまでIAM、S3、Glue DataCatalogの組み合わせで実現していたものをLake Formationで管理可能に
    - S3に保存されRedshift Spectrumでアクセスする際、Lake Formationによりデータの列レベルのアクセス制御をサポートするなどが可能
    - この場合Redshiftの実行ロールは、S3のアクセス権限ではなく、Lake Formationへの権限が必要となる
    - 列レベルのアクセス制御ポリシーは、SQL Grant ステートメントによって作成および管理することも可能

# Amazon Data Firehose (旧称 : Amazon Kinesis Data Firehose)

- S3、Redshift、OpenSearch Service、その他サードパーティのHTTPエンドポイントにデータを配信できる
- CloudWatch Logsのサブスクリプションフィルターに設定可能
    - Kinesis Data  Streams、Lambda、Data Firehoseで使用でき、ログはbase64 でエンコードされgzip 形式で圧縮される
    - ログの収集などに使用可能（別アカウントのCloudWatch Logsをサブスクライブする）
- DynamoDBに直接書き込むことはできない
- Kinesis Agentからの書き込み
    - ソースにKDSが指定されている場合、PutRecordでFirehoseに書き込むことができず、KDS経由で書き込む必要がある
    - Kinesis Agent自体はKDSまたはFirehoseにデータを送信できるJavaベースのソフトウェア

# Amazon Kinesis Data Streams

- ストリーミングデータに最適化されたスケーラブルなデータ取り込みおよび変換サービス
- 数十万のソースから毎秒ギガバイトのデータを継続的にキャプチャ可能
- 収集されたデータはミリ秒単位で利用できるため、リアルタイム分析が可能
- レコードの順序付けに加えて、複数の Amazon Kinesis アプリケーションに対して同じ順序でレコードの読み取りや再生を行う機能を提供
- Lambdaとのネイティブ統合
    - ネイティブ統合を使用すると、ポーリング、チェックポイント、およびエラー処理の複雑さが抽象化
    - 処理されたデータをDynamoDBに保存するよう設定が可能
- シャード
    - シャードは、全体で 1 MB/秒の書き込みと 2 MB/秒の読み取りを提供する容量の単位
    - シャードを増加させることでピーク時のデータ転送容量を増加させることができる
    - シャード分割はパーティションキーを使うことができる
- レコードは、データプロデューサーが Amazon Kinesis データストリームに追加するデータ
- PUT ペイロード ユニットは、レコードを構成する 25 KB のペイロード「チャンク」としてカウント
- 配信先の制限
    - Lambda、EC2、KDA、EMRなどに配信できる
    - Streamsから直接Redshift等には配信できないため注意（Firehoseが必要）
- Kinesis Agent
    - Amazon Kinesis サービスにデータを簡単に収集して取り込む OSS のスタンドアロンJava アプリケーション
    - Amazon Kinesis Streams と Amazon Kinesis Firehose、どちらへも送信可能
- Kinesis Producer Library
    - Amazon Kinesis Streams にデータを送信する OSS の補助ライブラリ
- Kinesis Client Library
    - AWS Kinesis Data Stream に流れるデータ（レコード）を受信して処理を行うコンシューマアプリケーションを実装するためのライブラリ
    - DynamoDB テーブルとの関係
        - 各 KCL アプリケーションは独自の DynamoDB テーブルを使用する必要がある
        - ストリーム内のシャード ID は、チェックポイント作成中に DynamoDB テーブルの主キーとして使用される
        - ユーザーは DynamoDB を KCL のチェックポイント作成テーブルとしてのみ使用できる
        - 参考
            - [同じ DynamoDB テーブルで Amazon KCL アプリケーションを使用する | AWS re:Post](https://repost.aws/ja/knowledge-center/kinesis-kcl-apps-dynamodb-table)
- メトリクス
    - GetRecords.IteratorAgeMilliseconds : GetRecords リクエストのストリーム内の最後のレコードの経過時間をミリ秒単位で測定
    - GetRecords.Latency : GetRecords 操作にかかった時間を測定
    - PutRecords.Latency : PutRecords 操作にかかった時間を測定
    - ReadProvisionedThroughputExceeded : KDSのサービスまたはシャードの制限を超えた GetRecords 呼び出しの数を測定

# Amazon Managed Service for Apache Flink (旧称：Amazon Kinesis Data Analytics)

- ストリームデータを標準的な SQLクエリでリアルタイムに分析
- Kinesis Data Analytics (KDA) は、アプリケーションの次のストリーミング ソースのみをサポートすることに注意することが重要です。
    - Amazon Kinesis Data Streams
    - Amazon Data Firehose (KDF) 配信ストリーム
- データストリームの異常を検出するには、このRANDOM_CUT_FOREST 関数を使用できる
- RCFは、データセット内の異常なデータポイントを検出するための教師なしアルゴリズム

# Amazon Managed Streaming for Apache Kafka

- フルマネージドで可用性が高くセキュアなApache Kafka サービス
- クラスターの構築が必要でマネージドなEC2で構成されたアーキテクチャ、KDSと異なりサーバーレスではない
- Apache Kafkaをオンプレミスで使用されていた場合は移行が容易
- OSS互換な点も特徴でKafkaのエコシステムを利用できる
    - Kafka MirrorMaker、Kafka Connect、Schema Registry
- Amazon MSK の最大レコード サイズは 100 MB
    - KDSはbase64 エンコード前で1MBなのでメッセージサイズで絞り込む
- 参考
    - [AWSのストリーム処理向けメッセージングサービスKDS(Kinesis)・MSK(Kafka)・SQSの特徴 #AWS - Qiita](https://qiita.com/sigmalist/items/1a65b0b0456516e2056b)

# Amazon QuickSight

- SPICE
    - 超高速、並列、インメモリな計算エンジンで、大規模なデータセットに対してインタラクティブなクエリを実行し、迅速な応答を取得する
- エディション
    - Standard エディションと Enterprise エディションが用意
    - Standardでは25 million rowsまたは25GBが上限、Enterpriseでは500 million rowsまたは500GBがデータセットの上限（非圧縮状態で）
    - Enterprise エディションでは、保存時の暗号化と Microsoft Active Directory の統合も提供
        - SAML 2.0 (およびデフォルトの暗号化設定) を使用して ID フェデレーションを実行するように構成する
        - AD Connectorが出てくる場合は間違い
- セキュリティグループ
    - QuickSightがRedshiftに接続するためには、その AWS リージョンの Amazon QuickSight サーバーの適切な CIDR アドレスブロックからのアクセスを承認する受信ルールが、セキュリティグループに必要
- VPC統合
    - VPCと統合できるのはEnterpriseエディションのみ
    - VPCエンドポイントを使用すれば同じリージョン内のRedshift等にアクセスできる
- 対応データソース
    - Amazon RDS、Amazon Aurora、Amazon Redshift、Amazon Athena、Amazon S3 などの AWS データ ソースに接続
    - Salesforce などの SaaS アプリケーションにも対応
    - データソースをS3とする場合の注意
        - QuickSight は、Amazon S3 からデータを読み取る際にparquet形式をサポートしていない
- チャートの種類
    - ツリーマップ : 四角形はでディメンション内の 1 つの項目を表現し、長方形のサイズは、ディメンションの全体と比較した、項目が表す選択したメジャーの値の割合を表せる
    - ウォーターフォール チャート : 値が加算または減算されるときの連続的な合計を視覚化
    - ファンネル チャート : ボトルネックなどの各段階の傾向や潜在的な問題領域を表示できる
    - ヒート マップ :  2 つの次元の交差のメジャーを表示し、値が範囲内のどこに該当するかを簡単に区別できるように色分け
- 更新頻度
    - QuickSight には、日次、週次、または月次ベースでデータを更新するオプションがある
    - またEnterprise Edition の場合のみ、「時間ごと」を選択するオプションがある
    - それ以上短い感覚が必要な場合、OpenSearch(Kibana)が必要

# Amazon OpenSearch

- OpenSearch を簡単にデプロイ・管理、スケール可能なフルマネージドサービス
- ドメイン
    - OpenSearch クラスター、およびクラスターと連携する AWS サービスの総称
    - ノードはデータノード、専用マスターノード、UltraWarm ノードの 3 種類
- インデックスはシャードに分割され、シャードサイズを10～50GiBに保つのが最適

# Amazon SageMaker

- コストが主な最適化基準である場合、SageMaker インスタンスは Amazon EC2 インスタンスより 40% コストが高いと推定されているため、コスト最適では注意

# Amazon ElastiCache for Redis

- 超高速のインメモリデータストア
- キャッシュ、チャット/メッセージング、ゲーム リーダーボード、地理空間、機械学習、メディア ストリーミング、キュー、リアルタイム分析、セッション ストアなどのリアルタイムのトランザクションおよび分析処理のユースケースに最適

# Amazon DynamoDB

- DAX
    - DAX は DynamoDB と互換性のあるキャッシュ サービスであり、要求の厳しいアプリケーションで高速なメモリ内パフォーマンスの恩恵を受けることが可能
- DynamoDB Stream
    - テーブル内のデータ項目に対するすべての変更に関する情報を最大 24 時間キャプチャする
    - 最も一般的なアプローチは、AWS Lambda、または DynamoDB Streams Kinesis アダプターで Kinesis クライアント ライブラリ (KCL) を使用するスタンドアロン アプリケーションを使用

# Amazon Simple Queue Service (SQS)

- SQS は、標準キューと FIFO キューの 2 種類のメッセージ キューを提供
- FIFO キューは 1 秒あたり最大 300 のトランザクションをサポート
- SQS の場合、同じメッセージを複数のコンシューマーによって同時に消費させることはできない

# Amazon S3

- オブジェクトの一部を取得したい場合、S3 SlectのScanRangeパラメータまたはGet OjbectでRange HTTPヘッダを使用する。
- S3オブジェクトは通常、アップロードしたAWSアカウントの所有となるため、別アカウントのS3バケットにUNLOADする際には、そのアカウント上のIAMロールを引き受けて処理をする必要がある
- リクエストレート
    - 高いリクエストレートに自動的にスケール
    - バケット内のプレフィックスごとにリクエストレートがある
        - PUT/COPY/POST/DELETE： 1 秒あたり少なくとも 3,500 の リクエスト
        - GET/HEAD：5,500 の リクエストを達成
- 整合性
    - すべての GET、PUT、および LIST オペレーションに対して強い一貫性を持っている
- レプリケーション
    - 同一リージョンレプリケーション、クロスリージョンレプリケーションが可能
    - またレプリケーション先のストレージクラスをソースとは異なるものにすることも可能
- S3 Standard IA
    - アクセス頻度は低いが、必要な場合には迅速なアクセスが必要なデータ用のクラス
    - 最小保存期間料金は 30 日
- S3 One Zone-IA
    - Standard IAとほぼ同じだが、少なくとも 3 つのAZにデータを保存する他の S3 ストレージ クラスとは異なり、S3 One Zone-IA はデータを 1 つの AZ に保存
    - コストが S3 Standard-IA より 20% 低くなる
    - 最小保存期間料金は 30 日
- S3 Glacier Instant Retrieval
    - 医療画像、ニュース メディア資産、ユーザーが作成したコンテンツ アーカイブなど、即時アクセスが必要なアーカイブ データに最適
    - 最小保存期間料金は 90 日
- Amazon S3 Select
    - S3 Select は、オブジェクト全体を取得することなく、単純な SQL 式を使用してオブジェクトのコンテンツから特定のデータを簡単に取得できるようにする機能
    - S3 Glacier Select もあるが、非圧縮 CSV 形式のデータのみクエリ可能なため注意
    - Athenaより低コストであるため、そのような問題であればこちら
- S3 Glacier
    - S3 Glacier に移動すると、Athenaからのクエリはできなくなる
    - コンプライアンス制御を実行する場合は、ボールトロックポリシーを使用する

# AWS Snowball

- Snowball Edge Storage Optimized
    - 数十テラバイトからペタバイトのデータを AWS に安全かつ迅速に転送する必要がある場合に最適な選択肢
    - 最大 80 TB の使用可能な HDD ストレージ、40 個の vCPU、1 TB の SATA SSD ストレージ、および最大 40 Gb のネットワーク接続を提供
    - Snowball Edge デバイスから AWS Glacier にデータを直接コピーすることはできない
- Snowmobile
    - 非常に大量のデータを AWS に移動するために使用されるエクサバイト規模のデータ転送サービス
    - 1台につき100PBまで運ぶことができ、10PB以上のデータセットを1か所に移行するためにはこちらを推奨