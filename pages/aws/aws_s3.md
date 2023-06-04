# Amazon S3

## 手動操作した場合のライフサイクルポリシー

例えば下記のようなライフサイクル設定をしているとして、

- 60 days Standard -> Standard-IA
- 120 days Standard-IA -> Glacier (FR)

そしてcat.jpgをアップロードし、10日後に手動でStandard-IAに移行した場合、10+120日後にGlacierに移動される。
最終更新日のみが使用されるため。

## 参考

### [2021-03-31 絵で見て 3分でおさらいする Amazon S3 のバージョニングとライフサイクル | DevelopersIO](https://dev.classmethod.jp/articles/3minutes-s3-versioning-lifecycle/)

### [2021-05-20 複数のアクセス拒否設定をしたS3バケットをCloudFormationで作ってみた](https://dev.classmethod.jp/articles/multi-access-restricted-s3-cfn/)

Effect: DenyでConditionがAND条件で評価されるので、どれか一つでも合えばアクセスできる設定となる。

```
            Condition:
              StringNotLike:
                'aws:userId':
                  - "AROAxxxxxxxxxxxxxxxxx:*"
              NotIpAddress:
                'aws:SourceIp':
                  - 111.222.333.444/32
            StringNotEquals:
                'aws:SourceVpce':
                  - "vpce-1a2b3c4d"
                "aws:CalledVia":
                  - "cloudformation.amazonaws.com"
```

### [2021-09-09 【AWS Tips】SSE-KMSとキーローテーションの目的・仕組み - 顧客フロントSEのIT勉強ブログ](https://frontse.hatenablog.jp/entry/2021/09/09/171150)

### [2023-02-28 S3 オブジェクトの一覧をあまり手間をかけずに AWS CLI で取得する](https://dev.classmethod.jp/articles/s3-objects-list-aws-cli/)

以下が結論

```
aws s3 ls バケット名 --recursive | grep -v '/$' | awk '{print $4}' > result.txt
```

### [2023-04-14 大量のAmazon S3 バケットをシェルスクリプトで一撃削除](https://dev.classmethod.jp/articles/delete-versioning-s3-shell/)

- バージョニングが有効になっている場合は旧バージョンのファイル削除をするs3api delete-objectsを使用する必要があるのはポイント
- delete-objectsは1000個までしか一度に指定できないため、その場合別途対策が必要らしい

## アップデート

### [2023-01-06 Amazon S3 Storage Lens に 34 個のメトリクスが追加](https://dev.classmethod.jp/articles/s3-storage-lens-34-metrics/)

Storage LensはさまざまなメトリクスでS3を分析する機能

### [2023-03-15 S3 インターフェースエンドポイントでプライベート DNS 名を使用できるように](https://dev.classmethod.jp/articles/amazon-s3-private-connectivity-on-premises-networks/)

### [2023-04-28 すべての新しいバケットに2つのセキュリティベストプラクティスをデフォルトで適用するように](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-s3-security-best-practices-buckets-default/)

- すべての新しいS3バケットに対して以下が適用
  - S3ブロック公開アクセスを自動的に有効
  - S3アクセス制御リスト（ACL）を無効にする
- 参考
  - [今S3のIaCで「AccessControlListNotSupported: The bucket does not allow ACLs」というエラーが出たならそれは2023年4月に行われたS3の仕様変更が原因かもしれない | DevelopersIO](https://dev.classmethod.jp/articles/s3-acl-error-from-202304/)
    - ACL有効化が必要な要件は非常に限定的で、たとえば「CloudFrontディストリビューションのログを格納するバケット」などはACL設定が必要
    - 一方、「CloudFrontのオリジンにする、静的コンテンツを格納するバケット」についてはACLの設定が不要
    - いまいちど見直すべし
