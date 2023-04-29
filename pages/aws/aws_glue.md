# AWS Glue

ETLを行うサービス

## Git統合

- 2022-10-13にアップデートされた機能
  - [https://aws.amazon.com/jp/about-aws/whats-new/2022/10/aws-glue-git-integration/](https://aws.amazon.com/jp/about-aws/whats-new/2022/10/aws-glue-git-integration/)
  - [https://dev.classmethod.jp/articles/aws-glue-git-integration/](https://dev.classmethod.jp/articles/aws-glue-git-integration/)
- CodeCommitおよびGitHubと連携してジョブをバージョン管理可能。
- 1つのレポジトリで複数ジョブに対応させられる。
  - ジョブ毎にフォルダが分かれる。
- pushした際のコンフリクトは強制上書きされるため注意が必要。
  - ベストプラクティスとして、ブランチをユーザ毎に分けるなどをした方が良い。

## アップデート

### [2023-04-17 リソース使用状況を監視する新機能を発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-glue-monitor-usage-resources/)

- Cloudwatchで特定のGlueリソースの利用状況を監視し、適切なCloudWatchアラームを設定することが可能に

### [2023-04-24 CrawlersがPartition Indexの作成に対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-glue-crawlers-creating-partition-indexes/)

Glue CrawlerはS3からデータスキーマとパーティションを抽出し、AWS Glue Data Catalogに入力することでメタデータを最新の状態に保つ機能

本リリースでは、AWS Glue Crawlerが新しいAWS Glue Data Catalogテーブルを作成する際に、手動で作成する必要がなく、デフォルトでパーティションインデックスも作成される

これにより、数百万のパーティションを持つテーブルのパーティションメタデータの取得とフィルタリングに要する時間を短縮