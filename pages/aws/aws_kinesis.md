# Amazon Kinesis

## Amazon Kinesis Data Streams

ConsumerにLambdaを使用可能。Lambdaの実行数は、ParallelizationFactorにより増加させることが可能。
ParallelizationFactorは係数となっており、シャード数が100の場合、係数を2に設定すると、合計200個のLambdaで並列処理をする。

## 参考記事

- [シャード数を増やさずに Kinesis Data Streams からトリガーされる Lambda の実行数を増やしたい時の対処方法 | DevelopersIO](https://dev.classmethod.jp/articles/tsnote-kinesis-triger-lambda-increase/)
- [2023-05-08 KinesisデータストリームをLambdaで処理する時のエラー制御方法をまとめてみた | DevelopersIO](https://dev.classmethod.jp/articles/how-to-handle-kinesis-data-stream-errors/)
- [2023-04-27 Kinesis Data FirehoseからS3に送信するオブジェクトに付くプレフィックスをJSTにするため動的パーティショニングを使ってみた | DevelopersIO](https://dev.classmethod.jp/articles/try-dinamic-partitioning-of-firehose/)
- [Kinesis Video Streams Edge AgentをRaspberry PI上のDocker（Ubuntu）へデプロイして、ローカルのIPカメラの映像を送信してみました | DevelopersIO](https://dev.classmethod.jp/articles/kinesis-video-streams-edge-agent-with-docker-ubuntu-raspberry-pi/)