# Amazon ECS

コンテナのオーケストレーションサービス。
FargateとEC2の2タイプがあり、GPU/WindowsはEC2しか使用できない。

- 参考記事
  - [AWS Fargate - Qiita](https://qiita.com/leomaro7/items/a3edb49d9929dd42cc0d)


### ECS Execとは

SSMを使用してコンテナとの接続を確立することができる。

- [[アップデート] 実行中のコンテナに乗り込んでコマンドを実行できる「ECS Exec」が公開されました | DevelopersIO](https://dev.classmethod.jp/articles/ecs-exec/)

Auto ScalingとECS Execを同時使用はできないので注意が必要
- [ECS Execの有効化が原因でECSタスクがPROVISIONING状態から遷移しなくなった話 | DevelopersIO](https://dev.classmethod.jp/articles/ecs-exec-cant-use-with-asg-capacity-provider/)

### ECSに必要なVPCエンドポイント

- ECS関連

| エンドポイント                     | EC2 | Fargate |
|:---|:---|:---|
| com.amazonaws.region.ecs-agent     | 要  | 不要    |
| com.amazonaws.region.ecs-telemetry | 要  | 不要    |
| com.amazonaws.region.ecs           | 要  | 不要    |

- ECR関連

| エンドポイント                            | EC2  | Fargate Linux 1.4.0 | Fargate Linux 1.3.0以前 | Fargate Windows 1.0.0 |
|:---|:---|:---|
| com.amazonaws.region.ecr.dkr              | 必要 | 必要                | 必要                    | 必要                  |
| com.amazonaws.region.ecr.api              | 必要 | 必要                | 不要                    | 必要                  |
| com.amazonaws.region.s3（ゲートウェイ型） | 必要 | 必要                | 必要                    | 必要                  |

- その他使いそうなもの
  - CloudWatch Logs
    - com.amazonaws.region.logs
  - Secrets Manager
    - com.amazonaws.region.secretsmanager
  - Systems Manager
    - com.amazonaws.region.ssm
    - com.amazonaws.region.ssmmessages
    - com.amazonaws.region.ec2messages

- 参考
  - [ECSに必要なVPCエンドポイントまとめ（2022年版） | DevelopersIO](https://dev.classmethod.jp/articles/vpc-endpoints-for-ecs-2022/)

## ECSでDocker Hubの認証情報を扱う

Docker Hubからのpullには回数制限があり、IPガチャによってはこの影響がある。

そのため、認証情報できちんとログインした方が良いらしい。(匿名の場合IP毎に6時間で100pull、認証の場合ユーザ毎に6時間で200pull)

- [ECS on Fargate構成でDocker Hubの認証情報を扱う | DevelopersIO](https://dev.classmethod.jp/articles/authenticating-with-docker-hub-for-aws-container-services/)

CodeBuildについてはこれがさらに厳しい。

## Service Connect

re:Invent 2022で発表された。

Servie Discoveryと違ってDNSを使わず、サービス間の通信のメトリクスが見れるのが良さそう。

価格はECSタスク内で起動するService Connect agentコンテナ用に、256CPUと64MiBのメモリが必要。

- [【レポート】ECSサービス間通信をシンプルにするAmazon ECS Service Connect #reinvent #CON323 | DevelopersIO](https://dev.classmethod.jp/articles/aws-reinvent-2022-amazon-ecs-service-connect-simplified-interservice-connection/#toc-10)


## 具体例

- [FargateでWebSocertサーバーを構築する](https://dev.classmethod.jp/articles/websocket-alb-fargate/)
  - バックエンドはNode.jsでwsというモジュールを使っている。
  - きちんとALBを立てて複数のFargateサービスを使っている。

## タスクロールとタスク実行ロール

タスク実行ロールは、ECRやCloudWatchなどよりインフラよりなイメージで、要するにコンテナを起動するホスト側が意識するロール。

タスクロールは、コンテナで動作するアプリケーションに持たせたいロールで、S3にアクセスするなどはこちらに設定。

なお、ECS Execでログを表示するには、タスクロールを設定する必要があるらしい。

- [ECS Exec のログ記録はタスクロールで行われるため注意しよう | DevelopersIO](https://dev.classmethod.jp/articles/ecs-exec-use-task-role-for-logging/)

## Fargate SpotはSaving Planを使えない

- [What are Savings Plans? - Savings Plans](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html)

## Fargateのtopコマンドと設定値の矛盾

きちんと明確にプロファイルしたいならEC2を使うべき。
freeコマンドでは基盤側の情報が採取されることもある。MemoryUtilizedの算出方法は非公開。

## Articles

- [2020-08-30 ALB と docker ヘルスチェックによる ECS の挙動について | Stuck inside](https://blog.msysh.me/posts/2020/08/behavior_of_ecs_by_alb_and_docker_health_check.html)
- [2023-03-18 [小ネタ]ECSのCPUUtilizationとCPUUtilizedは同じ指標？](https://dev.classmethod.jp/articles/ecs-cpuutilized-vs-cpuutilization/)
- [2023-05-17 [小ネタ]ECSタスクのタグ付けはタグの伝播元を設定しよう | DevelopersIO](https://dev.classmethod.jp/articles/ecs-using-tags/)
- [2023-05-08 Amazon ECS Exec(aws ecs execute-command)を便利にするツール「sssh」 | DevelopersIO](https://dev.classmethod.jp/articles/sssh-ecs-exec-tool/)

## Updates

- [2023-02-27 非アクティブなタスク定義リビジョンの削除をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/02/amazon-ecs-deletion-inactive-task-definition-revisions/)
  - こちらも
  - [ついにAmazon ECSの不要なタスク定義が削除できるようになりました！](https://dev.classmethod.jp/articles/update-amazon-ecs-delete-inactive-task-definition/)
  - [Amazon ECS タスク定義のリビジョンが「削除」をサポートしました！](https://dev.classmethod.jp/articles/amazon-ecs-task-definition-deletion/)
- [2023-07-17 AWS FargateがSeekable OCIを使用してコンテナ起動の高速化を実現](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/aws-fargate-container-startup-seekable-oci/)
  - 公式ブログポストに沿えば使えるらしい
    - [AWS Fargate Enables Faster Container Startup using Seekable OCI | AWS News Blog](https://aws.amazon.com/jp/blogs/aws/aws-fargate-enables-faster-container-startup-using-seekable-oci/)
  - [[アップデート]全 AWS Fargate 利用者必見！ Seekable OCI インデックスによりコンテナの起動が大幅に高速化するようになりました | DevelopersIO](https://dev.classmethod.jp/articles/update-aws-fargate-seekable-oci/#toc-13)
- [2023-07-27 Amazon ECS コンソールでタスク定義ワークフローのサポートが強化](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-ecs-console-task-definition-workflows/)
  - 1つのページレイアウトで、タスク定義の新規作成と修正、さらにコンテナログのルーティング、ファイアレンズ、コンテナのヘルスチェックなどの機能を設定できるように
