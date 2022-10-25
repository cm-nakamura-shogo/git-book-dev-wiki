# Amazon API Gateway

## Lambdaとの統合方式

Lambda統合とLambda非プロキシ(カスタム)統合を選択可能。

Lamdaプロキシ統合は、Lamda上から決められた形式で返却することにより、カスタム統合で必要な統合レスポンスを省略でき、より簡単にセットアップできる仕組み。

Lambda非プロキシ(カスタム)統合は、プロキシ統合のセットアップに加えて、受信リクエストデータがどのように統合リクエストにマッピングされるか、統合レスポンスデータの結果がメソッドレスポンスにどのようにマッピングされるかを指定する方式

非プロキシの場合、Lambdaのステータスコードもうまくマッピングしなければ、すべて200がクライアントに返信されるので注意が必要。

- 参考
  - [API Gateway + REST + Lambda 非プロキシ(カスタム)統合でステータス200以外返ってこない | DevelopersIO](https://dev.classmethod.jp/articles/apigateway-rest-lambda-custom-integrations-status-only-200/)
