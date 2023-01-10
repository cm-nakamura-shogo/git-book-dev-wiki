# CloudTrail

インフラの変更などを確認するサービス

## Athenaでログを見る方法

デフォルトでDDLを与えてくれるものの、これがパーティションが適切でないため効率が悪い。

以下に整えてやるための手順が記載されていてとても良い。

- [【全リージョン対応】CloudTrailのログをAthenaのPartition Projectionなテーブルで作る | DevelopersIO](https://dev.classmethod.jp/articles/cloudtrail-athena-partition-projection-table/)