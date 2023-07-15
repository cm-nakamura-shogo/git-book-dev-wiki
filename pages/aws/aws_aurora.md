# Amazon Aurora

## Aurora Serverless v2

v1->v2によりVPC外からパブリックアクセスが可能となった。デバッグ時などは有用かも。

- [Aurora Serverless(v2)のPostgreSQLに外部のSQLクライアントから接続してみた | DevelopersIO](https://dev.classmethod.jp/articles/aurora-serverlessv2-postgresql-connect/)

## アップデート

### [2023-05-13 AuroraにIO Optimizedというストレージ構成が追加](https://dev.classmethod.jp/articles/aurora-io-optimized/)

- IOに追加料金が発生せず、容量に対して課金される。容量はスタンダードより割増。
- コストが予測しやすくなる（IOだと予測が難しい）

### [2023-05-13 Amazon Aurora が Graviton3 搭載インスタンス(R7g)をサポートしました | DevelopersIO](https://dev.classmethod.jp/articles/aurora-graviton3-r7g/)

- 値上げ分を上回る 高性能なDBとの評価

### [2023-07-13 Aurora PostgreSQLがベクトル・ストレージと類似性検索のためにpgvectorをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-aurora-postgresql-pgvector-vector-storage-similarity-search/)

- pgvectorは、Amazon Bedrockや Amazon SageMakerなどのエンベッディングを保存し、検索することを可能にする
- Aurora Machine Learningにも言及