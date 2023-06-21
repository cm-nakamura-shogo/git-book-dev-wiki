# AWS Step Functions

ワークフローのサービス

## ワークフローの種類

非同期実行のみのStandard Workflowと、同期実行が可能なExpress Workflowの2種類がある。

## 可視化機能

視覚的に実行内容を可視化できる機能。

以前は、Standardのみ対応していたが、2022-10-19にExpressでも可視化機能がGAされた（別途有効化は必要）。

- 参考記事
  - [AWS Step Functions Express Workflowの実行内容を視覚化されたビューで確認できるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/you-can-now-see-what-the-aws-step-functions-express-workflow-is-running-in-a-visual-view/)

## Slackへの通知

Step Functions → EventBridge → SNS → Lambda → Slackで実現するようだ。以下が参考になる。

- [Incoming Webhookを使用してAWS Step Functionsの実行結果をSlackに通知する | DevelopersIO](https://dev.classmethod.jp/articles/slack-notify-incoming-webhook-using-lambda/)

## Distributed Map

re:Invent 2022, 2022/12にリリースされた機能。
元々並列実行は対応していたものの、より大規模なものに対応したっぽい。

- [AWS Step Functionsで大規模な並列処理を実施できるDistributed Mapを試してみた | DevelopersIO](https://dev.classmethod.jp/articles/distributed-map-which-can-perform-large-scale-parallel-processing-with-aws-step-functions/)

## 特定の時間帯のみ実行する方法

Wait タスクの TimestampPath が過去の時刻場合は即実行されるのが、味噌らしい。

- [特定の時間帯のみ AWS Step Functions のタスクを実行するための Python コードを書いてみた | DevelopersIO](https://dev.classmethod.jp/articles/aws-step-functions-execute-task-specific-time-with-python-code/)

## 参考記事

### [2020-07-07 ステート間のパラメータ受け渡し方法](https://dev.classmethod.jp/articles/stepfunctions-parameters-inter-states/)

- 平野さんの記事。とても分かりやすい。

## アップデート

### APIサポートが拡大(2023-02)

- [[アップデート] AWS Step FunctionsのAWS SDK Integrationで、35のAWSサービスと1100のAPIアクションが追加でサポートされました | DevelopersIO](https://dev.classmethod.jp/articles/aws-step-functions-new-35-services-api/)

### [2023-06-17 AWS Step Functions の AWS SDK Integration で、7つの AWS サービスと 460 以上の API アクションが追加でサポートされました | DevelopersIO](https://dev.classmethod.jp/articles/aws-step-functions-adds-integration-for-7-services/)