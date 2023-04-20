# Amazon Connect

## データ

保存可能なデータは以下。

- CTR ... Amazon Connectで発生するイベントや、属性、キュー、エージェントのやり取りをキャプチャしたもの
- wavファイル ... 通話録音データ

CTR保存時は、Kinesis Data StreamsまたはKinesis Data Firehoseを使って最終的にはS3に保存する。
(Streamsを使った場合の方が、複数のFirehoseに配信可能なアーキ)

wavファイルは直接S3に保存することが可能。

## 参考記事

- [[Amazon Connect]問い合わせレコードデータモデル(CTR)をS3に保存し、Athenaを使って通話録音データの格納場所を検索する | DevelopersIO](https://dev.classmethod.jp/articles/amazon-connect-ctr-s3-athena-recordinglocation)
