# Amazon EventBridge

## Articles

- [2023-02-27 EventBridge Schedulerを使ってEC2を定期起動・停止するCloudFormationテンプレート](https://dev.classmethod.jp/articles/cloudformation-template-eventbridge-scheduler-ec2-start-stop/)
- [2023-02-28 RDSの自動定期停止をEventBridge SchedulerとCloudFormationで実装](https://dev.classmethod.jp/articles/rds-stop-with-amazon-eventbridge-scheduler-and-cloudformation/)
- [2023-04-24 Amazon EventBridge SchedulerでCloudWatchアラームを定期的に無効化・有効化するCloudFormationテンプレートを作成してみた | DevelopersIO](https://dev.classmethod.jp/articles/mazon-eventbridge-scheduler-cloudformation-template-for-enable-disable-cloudwatchalarm/)

## Updates

- [2023-07-17 AWS LambdaとAmazon EventBridge Pipesがフィルタリング機能を強化](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/aws-lambda-eventbridge-pipes-enhanced-filtering/)
  - 以下のフィルタリング機能などをサポート
    - 値の末尾の文字に対するマッチング (サフィックスフィルタリング)
    - 大文字小文字の区別を無視する (equals-ignore-case)
    - 複数のフィールドにまたがる条件が真である場合に単一のルールでマッチングする (OR マッチング) 
  - また数値の境界を従来の-1e9～1e9から-5e9～5e9に増加