# Amazon S3

## 手動操作した場合のライフサイクルポリシー

例えば下記のようなライフサイクル設定をしているとして、

- 60 days Standard -> Standard-IA
- 120 days Standard-IA -> Glacier (FR)

そしてcat.jpgをアップロードし、10日後に手動でStandard-IAに移行した場合、10+120日後にGlacierに移動される。
最終更新日のみが使用されるため。

## 参考

### [【AWS Tips】SSE-KMSとキーローテーションの目的・仕組み - 顧客フロントSEのIT勉強ブログ](https://frontse.hatenablog.jp/entry/2021/09/09/171150)

### [S3 オブジェクトの一覧をあまり手間をかけずに AWS CLI で取得する](https://dev.classmethod.jp/articles/s3-objects-list-aws-cli/)

以下が結論

```
aws s3 ls バケット名 --recursive | grep -v '/$' | awk '{print $4}' > result.txt
```

## アップデート

### [Amazon S3 Storage Lens に 34 個のメトリクスが追加](https://dev.classmethod.jp/articles/s3-storage-lens-34-metrics/)

Storage LensはさまざまなメトリクスでS3を分析する機能

### [[アップデート] S3 インターフェースエンドポイントでプライベート DNS 名を使用できるようになりました](https://dev.classmethod.jp/articles/amazon-s3-private-connectivity-on-premises-networks/)