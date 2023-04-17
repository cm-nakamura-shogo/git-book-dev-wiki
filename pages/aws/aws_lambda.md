# AWS Lambda

## Lambdaレイヤー

カスタムレイヤーを使用すると、pandasやnumpyなど通常は使用できないライブラリをPythonのLambdaで使用することが可能になる。

## Lambdaを用いたアプリケーションのDBデータ暗号化

以下の実装で作成することで問題ない。

- データを保存するとき
  - Lambdaが平文のデータを受け取る
  - LambdaがKMSを使ってデータを暗号化する
  - Lambdaが暗号文をRDSに書き込む
- データを取得するとき
  - Lambdaが暗号文のデータをRDSから取得する
  - LambdaがKMSを使ってデータを複合する
  - Lambdaが平文のデータを返す

大量に動く可能性がある場合、KMSのAPI課金、スロットル対策のため、Lambda側でKMSの鍵情報、一次キャッシュする仕組みが必要となる場合がある。
実現する場合は、AWS Encryption SDKなどが使用可能。

- [https://docs.aws.amazon.com/ja_jp/encryption-sdk/latest/developer-guide/data-key-caching.html](https://docs.aws.amazon.com/ja_jp/encryption-sdk/latest/developer-guide/data-key-caching.html)

ただし、RDBMSが備えるインデックスなどの利用も制限される事になるため、認識しておく必要がある。

逆にキャッシュしない方が良い場合は、ローテーションを必要とする場合など、古いキャッシュ利用が問題となったりするケース。
実装ミスなどあれば、間接的に秘匿情報の漏洩リスクなども高まるため、API課金、スロットルの心配が無い箇所で使うなら、キャッシュさせないほうがいい場合もある。

## Lambda Extensions

Lambdaに対する様々な拡張機能が付与可能。

リリース時はモニタリング用途、ツールのインストール、セキュリティ用途、シークレットの取得などに対応していた模様。

- 参考記事
  - [Lambda Extensionsは何が嬉しいのか | DevelopersIO](https://dev.classmethod.jp/articles/cons-of-lambda-extensions/)

## Paramter StoreやSSMからSDKを使わずに直接値を取得可能に (2022-10-20)

Lambda Extensionsを仕組みとして使用している。

キャッシュが働くため、コスト削減にもつながる様子。

- 参考
  - [[アップデート] Lambdaから直接Parameter Store/Secrets Managerから値を取得できるようになりました！ | DevelopersIO](https://dev.classmethod.jp/articles/lambda-get-paramater/)

実装自体は、Lambdaの実行環境内でHTTPサーバーのプロセスを起動し、このサーバーに対してリクエストすることで値を取得している。
(Lambda実行環境内でリバースプロキシをデプロイするExtensionのようなイメージ)

なので高速なのは自前実装でメモリ内でキャッシュを実現する方法のようだ。

- 参考
  - [AWS Parameters and Secrets Lambda Extensionのパフォーマンスへの影響を確認してみた | DevelopersIO](https://dev.classmethod.jp/articles/aws-parameters-and-secrets-lambda-extension-performance/)


さらに細かく調べた記事によれば、実装はGoでなされており、POSTやQuery-Stringが不正などの場合は400番台のエラーを返すようです。

- 参考
  - [AWS Parameters and Secrets Lambda Extensionの実装について色々確認してみた | DevelopersIO](https://dev.classmethod.jp/articles/investigation-parameters-and-secrets-lambda-extension-impl/)

## Lambda ENI Finder

ENIが削除できず、どのLambdaに紐づけられているか分からない場合にLambda ENI Finderが使えるらしい。

- [Elastic Network Interfaceが削除できなくて困った時にLambda ENI Finderを利用した話 | DevelopersIO](https://dev.classmethod.jp/articles/try-delete-lambda-eni-with-lambda-eni-finder/)

## LambdaのContextの中身

以下のような感じらしい。aws_request_idは識別子として使えるのかも。

```
function_name: hoge-dev-InvokeStateMachine
function_version: $LATEST
invoked_function_arn: arn:aws:lambda:ap-northeast-1:123456789012:function:hoge-dev-InvokeStateMachine
memory_limit_in_mb: 128
aws_request_id: 4c8443bd-f044-4c06-8ad1-7d8c351fb57f
log_group_name: /aws/lambda/hoge-dev-InvokeStateMachine
log_stream_name: 2022/08/22/[$LATEST]7dc42810d4254fc1a5bd0d5f28750f32
```

## VPC Lambda

通常はLambdaはVPC外に配置するが、プライベートなVPCで使用したい場合にはVPC Lambdaを使用する。

ちなみにVPC LambdaをpublicなVPC（IGWあり）に配置する場合、public IPをもつENIをVPC LambdaにアタッチしないとIGWと接続できないらしい。

- [VPC LambdaはIGWからインターネットに出られないわけではなかったという話 | DevelopersIO](https://dev.classmethod.jp/articles/lambda-vpc-with-global-address/)

## Lambdaのリトライ

リトライのRequest Idは同じになるらしい。

- [AWS Lambda の呼び出しタイプを軽く整理する - ダメ元エンジニアのお勉強おメモ](https://rasp.hateblo.jp/entry/2022/06/18/181511)

なのでリトライ回数に応じて処理を帰るなどの事例もある。

- [Lambdaのリトライ回数に応じて処理を変えたい](https://zenn.dev/shimo_s3/articles/c2895880138d19)

## 参考記事

### [2017-10-05 Lambda関数の呼び出しタイプとリトライ方式まとめ](https://dev.classmethod.jp/articles/lambda-idempotency/)

### [2019-03-03 今度こそ理解する！俺式Lambda入門](https://dev.classmethod.jp/articles/lambda-my-first-step/)

最初に読むのはすごく良い気がする

### [2023-02-28 特定のセキュリティグループが関連づけられているLambda関数をワンライナーで取得してみた](https://dev.classmethod.jp/articles/sg-used-by-lambda/)

### [2023-01-16 CDKでLambdaからSlack通知する方法](https://dev.classmethod.jp/articles/awscdk-costexplorer-notify-to-slack/)

## アプデ

### [2023-01-17 SQSをイベントソースとして利用する際に同時実行数が設定できるように](https://dev.classmethod.jp/articles/update-aws-lambda-event-source-amazon-sqs-concurrency/)

これまでSQSをイベントソースとする際の同時実行数は、Lambda関数の「同時実行の予約」で行っていたが、直感的に設定が可能になった。

### [2023-01-24 Lambdaで新しい「ランタイム管理設定」が追加されました](https://dev.classmethod.jp/articles/aws-lambda-supports-runtime-management-controls/)

ランタイムそのもののバージョン制御ではない（3.8 -> 3.9ではない）ので注意が必要。

関数の更新にアップデートするなどが選択できるが、自動が推奨。関数を更新する予定が無い場合は自動にすべきとのこと。

### [2023-04-07 レスポンスをストリーミングで返せるように](https://dev.classmethod.jp/articles/aws-lambda-can-streaming-response/)

APIGWでは使えないので、Lambda関数URLなどを使用する必要がある。
