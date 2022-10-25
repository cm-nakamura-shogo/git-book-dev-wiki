# AWS SDK

様々なSDKライブラリがある。

## タイムアウト

Lambda -> DynamoDB間で多いようだが、以下のような事例があるらしい。

- 何らかの原因で詰まる
- タイムアウト時間までエラーとならない(例. 2分間など)
- 時間がかかるため、Lambda自体(API Gatewayかも)がタイムアウト

そのため、タイムアウト時間を短めに設定して、リトライさせるようにするケースがあるようだ。

- 参考記事
  - [【AWS】LambdaからDynamoDBを呼ぶときは、タイムアウト時間を設定変更しようの巻 - Qiita](https://qiita.com/unichiku/items/6f51782b8442aa1c02c3)
  - [Boto3のコネクションタイムアウト値について教えてください | DevelopersIO](https://dev.classmethod.jp/articles/tsnote-boto3-connect-timeout-and-max-attempts/)
  - [AWS SDK for Python (boto3) のリトライ・タイムアウト制御 - Qiita](https://qiita.com/yh1224/items/5bdf43307c4c97281e7e)