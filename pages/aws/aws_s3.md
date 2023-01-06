# Amazon S3

## 手動操作した場合のライフサイクルポリシー

例えば下記のようなライフサイクル設定をしているとして、

- 60 days Standard -> Standard-IA
- 120 days Standard-IA -> Glacier (FR)

そしてcat.jpgをアップロードし、10日後に手動でStandard-IAに移行した場合、10+120日後にGlacierに移動される。
最終更新日のみが使用されるため。

## キーローテーションについて

- [【AWS Tips】SSE-KMSとキーローテーションの目的・仕組み - 顧客フロントSEのIT勉強ブログ](https://frontse.hatenablog.jp/entry/2021/09/09/171150)


## S3 Storage Lens

さまざまなメトリクスでS3を分析する機能

- [Amazon S3 Storage Lens に 34 個のメトリクスが追加され、より広い観点で分析が出来るようになりました | DevelopersIO](https://dev.classmethod.jp/articles/s3-storage-lens-34-metrics/)
