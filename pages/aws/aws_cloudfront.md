# Cloud Front

コンテンツを高速配信するためのCDNサービス。

## Articles

- [2023-07-19 CloudFront と S3 の階層化 TTL でシングルページアプリケーション (SPA) をホストする | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/networking-and-content-delivery-host-single-page-applications-spa-with-tiered-ttls-on-cloudfront-and-s3/)
  - TTLの細かい設定ノウハウがある

## Updates

- [2023-01-04 ポリシーで指定したレスポンスヘッダーの削除が可能に](https://dev.classmethod.jp/articles/cloudfront-removal-response-headers/)
  - ヘッダの削除機能が追加され、攻撃者にORIGINの情報を見えないようにするなどが可能となった。
  - 従来は、Lambda@EdgeやCloudFront Functionsで対応しないといけなかった部分を簡略化できる可能性がある。
- [2023-05-01 [update] CloudFront FunctionsでViewer ResponseのHTTPステータスコードとレスポンスbodyが変更できるようになっていました！ | DevelopersIO](https://dev.classmethod.jp/articles/http-status-response-generation-cloudfront-functions/)
