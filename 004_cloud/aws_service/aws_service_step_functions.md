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