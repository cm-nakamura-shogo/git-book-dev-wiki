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

### [2023-05-09 Glueのラージインスタンスタイプが一般公開](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/aws-glue-large-instance-types-generally-available/)

- 石川さんの記事
  - [[アップデート] AWS Glue 大規模インスタンスタイプG.4X および G.8Xが一般提供されました | DevelopersIO](https://dev.classmethod.jp/articles/20230510-aws-glue-g4x-and-g8x/)
- これまでの、--write-shuffle-files-to-s3や--write-shuffle-spills-to-s3 を有効にするワークアラウンドも今後も有効とのこと
- しかしより直接的な選択肢としてスケールアップできる選択肢ができた感じ
