# AWS Batch

- バッチ実行用のサービス。
- 実態は、ECSを起動してタスクを実行して終了するマネージドなサービス。
- 起動時のオーバーヘッドがネックだが、それが許容される場合は選択肢。
- on EC2の場合、GPUにも対応している。
- ECSにジョブキューがついて起動終了が自動化されるイメージ

## 関連ロール

ロールがいくつかあり整理が必要

- サービスロール
  - Amazon EC2 インスタンスの作成やオートスケーリングポリシーの設定などのバックグラウンドタスクを実行するために必要な権限を持つ、IAM アクセス許可ポリシーを含むロール。
- インスタンスロール
  - EC2 インスタンスが自分自身を操作するために必要な権限を持つ IAM ロール
  - たとえば、EC2 インスタンスから別の AWS サービスにアクセスする場合、インスタンスロールがその権限を提供する
  - コンテナの文脈だと、コンテナのホスト側のロールであるため、影響範囲が広いロール
- 実行ロール
  - AWS Batchがジョブを実行する際にECSタスク実行ロールを指定するもの
  - AWS Batch がジョブの起動や EC2 インスタンスへのアクセスを実行する権限を持った IAM ロールがこの実行ロールとなる
- ジョブロール
  - ジョブロールは、ジョブの実行時に実行環境やその他の AWS サービスにアクセスするために必要な権限を持つ IAM ロール
  - たとえば、ジョブが AWS Lambda を利用する場合、ジョブロールがその権限を提供する
  - コンテナの文脈だと、コンテナインスタンス側のロールであるため、こちら側にジョブ毎に適切な権限を割り当てる

## Article

- [2023-05-03 AWS Batch で OpenMPI を使った並列ジョブの実行をやってみた | DevelopersIO](https://dev.classmethod.jp/articles/tried-aws-batch-multi-node-parallel-jobs/)

## Update

- [2023-07-14 AWS Batch on AWS FargateがCLI/SDKでLinux ARM64とWindows x86コンテナをサポートするように](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/aws-batch-fargate-linux-arm64-windows-x86-containers-cli-sdk/)
  - Gravitonが使えるためよりコスパが良い
  - [[アップデート] AWS Batch の Fargate タイプで OS ファミリと CPU アーキテクチャが指定出来るようになったので、Windows コンテナで実行してみた | DevelopersIO](https://dev.classmethod.jp/articles/batch-fargate-linux-arm64-and-windows/)
- [2023-08-02 AWS Batchがスポットインスタンスの価格キャパシティ最適化割り当て戦略をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/aws-batch-price-capacity-optimized-allocation-strategy-spot-instances/)
- [2023-08-02 AWS Batch on AWS FargateがConsoleでLinux ARM64とWindows x86コンテナをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/aws-batch-fargate-linux-arm64-windows-x86-containers-console/)