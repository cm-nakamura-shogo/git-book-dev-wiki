# AWS Management Console

## アップデート

### [2023-05-10 AWS Management ConsoleへのプライベートアクセスがGA](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/aws-management-console-private-access/)

- devioでも出てる
  - [[アップデート] AWSマネジメントコンソールにVPCエンドポイント経由でアクセスできるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/aws-management-console-private-access/)
  - VPC Endpoints上に構築されており、AWS PrivateLinkを使用して、お客様のVPCとAWS Management Console間のプライベート接続を確立
  - インターネットに抜けずに閉域網からマネジメントコンソールにアクセスを実現するものではない
  - VPCもしくはオンプレミスネットワーク内からマネジメントコンソールの使用を信頼されたアカウントのみに制限する
  - ユーザーがネットワーク内から任意のAWSアカウントにサインインすることを防ぐ際に有効
- そもそもプライベートアクセスの需要はどこに？という声が多い
  - [https://twitter.com/r_karotou/status/1656629702830985216](https://twitter.com/r_karotou/status/1656629702830985216)