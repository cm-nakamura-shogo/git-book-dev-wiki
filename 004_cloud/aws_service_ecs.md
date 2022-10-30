# Amazon ECS

コンテナのオーケストレーションサービス。
FargateとEC2の2タイプがあり、GPU/WindowsはEC2しか使用できない。

- 参考記事
  - [AWS Fargate - Qiita](https://qiita.com/leomaro7/items/a3edb49d9929dd42cc0d)


### ECS Execとは

SSMを使用してコンテナとの接続を確立することができる。

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
