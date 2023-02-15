# DOP

## AWS CloudTrail

### 概要

- アカウントのガバナンス、コンプライアンス、運用監査、リスク監査を行うサービス
- CloudTrailは、IAMユーザーやIAMロール経由でサービスに実行されたアクションやAPI実行を記録
- リソースの変更やルール違反を監視する場合はAWS Configを使用
- AWS ConfigはConfigルールを通してCloudTrailが有効かどうかをチェックする

### Organizationsとの関連

- AWS Organizationsを利用中の場合、すべてのAWSアカウントのログをまとめて取得することが可能。
- マスターアカウントの組織の証跡を有効とすることで、すべてのアカウントのCroudTrailイベントを同じS3バケット、CloudWatch Logs、CloudWatchイベントに配信可能。
- AWS Organizationsを使用しない場合は、各アカウントで組織の証跡を有効化する必要あり。

### CloudTrail Insights

- CloudTrailのログの定期的な監査を行うツール。

### Step Functionsとの統合

- Step Functionsの人の手作業のによるアクティビティの記録などには、CloudTrailが必要となる。

## AWS Config

### 概要

- リソースの変更管理が可能
- リソースの設定変更の継続的な監視ができコンプライアンス評価が可能。
- API実行の記録はCloudTrailを使用。
- 変更監視はCloudWatch Eventsを使用。
  - 参考例：[特定のリソースIDの変更前と変更後をメールで通知する方法 | DevelopersIO](https://dev.classmethod.jp/articles/email-specific-resource-id/)
- 監視できるものの例
  - WAFなどのFirewallルールの変更・追跡
  - CloudTrailが有効かどうかの監視
  - Organizationsにおける複数アカウントについてもコンプライアンス管理が可能。
  - サードパーティのリソース管理なども

### AWS Config Aggregator

- 各アカウントのConfigルールによる評価の結果をまとめて表示することが可能となる機能

### 参考

- [AWS Configとは何か？できることや利点についてもあわせて解説 | ITエンジニア派遣なら夢テクノロジー](https://www.yume-tec.co.jp/column/awsengineer/4621)
- [AWS Config Aggregator を委任してマルチアカウント&マルチリージョンの評価を集約する - サーバーワークスエンジニアブログ](https://blog.serverworks.co.jp/organizations-config-aggregator-delegated-admin)