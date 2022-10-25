# AWS Lambda

## Lambdaレイヤー

カスタムレイヤーを使用すると、pandasやnumpyなど通常は使用できないライブラリをPythonのLambdaで使用することが可能になる。

## Paramter StoreやSSMからSDKを使わずに直接値を取得可能に (2022-10-20)

Lambda Extensionsを仕組みとして私用している。

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