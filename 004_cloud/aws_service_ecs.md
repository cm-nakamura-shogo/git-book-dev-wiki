# Amazon ECS

コンテナのオーケストレーションサービス。
FargateとEC2の2タイプがあり、GPUはEC2しか使用できない。

### ECS Execとは

SSMを使用してコンテナとの接続を確立することができる。

Auto ScalingとECS Execを同時使用はできないので注意が必要
- [ECS Execの有効化が原因でECSタスクがPROVISIONING状態から遷移しなくなった話 | DevelopersIO](https://dev.classmethod.jp/articles/ecs-exec-cant-use-with-asg-capacity-provider/)