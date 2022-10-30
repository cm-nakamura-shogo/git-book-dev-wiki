# Amazon Kinesis

## Amazon Kinesis Data Streams

ConsumerにLambdaを使用可能。Lambdaの実行数は、ParallelizationFactorにより増加させることが可能。
ParallelizationFactorは係数となっており、シャード数が100の場合、係数を2に設定すると、合計200個のLambdaで並列処理をする。

- 参考記事
  - [シャード数を増やさずに Kinesis Data Streams からトリガーされる Lambda の実行数を増やしたい時の対処方法 | DevelopersIO](https://dev.classmethod.jp/articles/tsnote-kinesis-triger-lambda-increase/)