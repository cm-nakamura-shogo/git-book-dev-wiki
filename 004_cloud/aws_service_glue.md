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