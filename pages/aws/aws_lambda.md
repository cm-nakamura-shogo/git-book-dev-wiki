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