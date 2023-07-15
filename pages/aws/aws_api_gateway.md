# Amazon API Gateway

## Lambdaとの統合方式

Lambda統合とLambda非プロキシ(カスタム)統合を選択可能。

Lamdaプロキシ統合は、Lamda上から決められた形式で返却することにより、カスタム統合で必要な統合レスポンスを省略でき、より簡単にセットアップできる仕組み。

Lambda非プロキシ(カスタム)統合は、プロキシ統合のセットアップに加えて、受信リクエストデータがどのように統合リクエストにマッピングされるか、統合レスポンスデータの結果がメソッドレスポンスにどのようにマッピングされるかを指定する方式

非プロキシの場合、Lambdaのステータスコードもうまくマッピングしなければ、すべて200がクライアントに返信されるので注意が必要。

- 参考
  - [API Gateway + REST + Lambda 非プロキシ(カスタム)統合でステータス200以外返ってこない | DevelopersIO](https://dev.classmethod.jp/articles/apigateway-rest-lambda-custom-integrations-status-only-200/)

## Articles

- [Amazon API Gatewayは「HTTP API」と「REST API」のどちらを選択すれば良いのか？ #reinvent | DevelopersIO](https://dev.classmethod.jp/articles/amazon-api-gateway-http-or-rest/)
- [2023-04-17 API Gateway に統合されたバックエンドからの JSON 形式のレスポンスを API Gateway だけで編集する | DevelopersIO](https://dev.classmethod.jp/articles/api-gateway-vtl-template-response/)
- [2023-04-27 API Gateway の Lambda オーソライザーキャッシュを使う時に問題となる実装を検証してみた | DevelopersIO](https://dev.classmethod.jp/articles/api-gateway-authorizor-cache-policy/)
- ["AWS を使って API 公開したくなったときに検討すべき６つの項目"というタイトルで DevelopersIO 2023 に登壇しました #devio2023 | DevelopersIO](https://dev.classmethod.jp/articles/developersio-2023-aws-api-publication-checklist/)