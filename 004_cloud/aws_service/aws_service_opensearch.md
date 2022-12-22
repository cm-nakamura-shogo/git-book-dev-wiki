# Amazon OpenSearch Service

基本はOpenSearchが動作するEC2サーバーが建つイメージ。

APIなどは、OpenSearchの方を参考に扱う。

## 用途

ログ分析、ストリーム分析、アプリケーションのモニタリングなど。

可視化などのダッシュボード機能も備えている。

Kinesis Data Firehoseの送信先として設定することが可能。

## ML Common API

機械学習のAPIがある。公式ドキュメントは以下。

- [API - OpenSearch documentation](https://opensearch.org/docs/latest/ml-commons-plugin/api/#example-load-into-all-available-ml-nodes)


## サンプル

### ApacheログをOpenSearchで分析

EC2(Apache) -> Firehose -> OpenSearchという流れ。

FirehoseでLambdaを使って、Lambdaのblueprintで「Apache Log to JSON」を選択して変換する。