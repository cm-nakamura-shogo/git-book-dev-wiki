# Amazon Aurora

## Aurora Serverless v2

v1->v2によりVPC外からパブリックアクセスが可能となった。デバッグ時などは有用かも。

- [Aurora Serverless(v2)のPostgreSQLに外部のSQLクライアントから接続してみた | DevelopersIO](https://dev.classmethod.jp/articles/aurora-serverlessv2-postgresql-connect/)

## アップデート

### [2023-05-13 AuroraにIO Optimizedというストレージ構成が追加](https://dev.classmethod.jp/articles/aurora-io-optimized/)

- IOに追加料金が発生せず、容量に対して課金される。容量はスタンダードより割増。
- コストが予測しやすくなる（IOだと予測が難しい）
