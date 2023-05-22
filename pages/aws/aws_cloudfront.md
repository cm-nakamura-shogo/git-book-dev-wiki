# Cloud Front

コンテンツを高速配信するためのCDNサービス。

## アップデート

### 2023-01-04 : ポリシーで指定したレスポンスヘッダーの削除が可能に

ヘッダの削除機能が追加され、攻撃者にORIGINの情報を見えないようにするなどが可能となった。

従来は、Lambda@EdgeやCloudFront Functionsで対応しないといけなかった部分を簡略化できる可能性がある。

- [Amazon CloudFront のレスポンスヘッダーポリシーで指定したレスポンスヘッダーの削除が出来るようになりました | DevelopersIO](https://dev.classmethod.jp/articles/cloudfront-removal-response-headers/)

### [2023-05-01 [update] CloudFront FunctionsでViewer ResponseのHTTPステータスコードとレスポンスbodyが変更できるようになっていました！ | DevelopersIO](https://dev.classmethod.jp/articles/http-status-response-generation-cloudfront-functions/)
