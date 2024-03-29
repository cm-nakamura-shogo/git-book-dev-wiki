# Amazon EC2 Instance Connect

## 参考記事

### [[新サービス] Amazon EC2 Instance Connect Endpoint が発表されました | DevelopersIO](https://dev.classmethod.jp/articles/ec2-instance-connect-endpoint/)

### [EC2 Instance Connect Endpoint と Session Managerの違いをまとめてみた | DevelopersIO](https://dev.classmethod.jp/articles/compare-eic-endpoint-and-session-manager/)

- 「個人的には、可用性重視の場合は、セッションマネージャーを選択し、コスト重視であれば、EIC エンドポイントを選択するのがよいかと思いました。」
- SSMはVPCエンドポイントポイントの料金が必要だが、EICは無料
- EICのセッション時間は最大1時間なのもネック
- 1つのVPCに１つのEIC エンドポイントしか作成できないため、EICのエンドポイントがあるサブネットにAZ障害が起きると使えない
  - これはデフォルトクォータの話をしているので誤りかも？

### [AWS CLIの実装からEC2 Instance Connect Endpointを読み解いてみた | DevelopersIO](https://dev.classmethod.jp/articles/demystifying-ec2-instance-connect-implementation/)

### [[アップデート]パブリック IP アドレスなしで、EC2インスタンスにSSH接続できる EC2 Instance Connect Endpointがリリースしました | DevelopersIO](https://dev.classmethod.jp/articles/update-ec2-instance-connect-endpoint/)

### [EC2 Instance Connect エンドポイント登場！パブリックIPのないEC2にSSH・RDPできるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/ec2-instance-connect-endpoint-private-access/)

- 鍵交換はしておく必要がある点はSSMと変わらないかも
- EICの場合、VPC内にエンドポイントを作成すれば、そこから通信可能なリソースにたいして、EC2へSSHしたりポートフォワードしてRDPしたり、RDBにアクセスしたりできます。
  - これはエージェントとか不要なのか？平井さんの記事と少し矛盾しているので検証が必要
- 西野さんまとめ
  - EC2向けのアウトバウンドトラフィック（TCP 22）を許可するSG必要 ※インバウンドは閉じておｋ
  - サブネットを指定して作成
  - Preserve Client IP 機能あり
  - IAMベースのアクセス制御
    - https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/permissions-for-ec2-instance-connect-endpoint.html#iam-OpenTunnel
  - 接続したあとの操作はやっぱり別で考えないとダメそう
    - https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/log-ec2-instance-connect-endpoint-using-cloudtrail.html
  - CLIから使える

### [パブリック IP アドレスなしで EC2 インスタンスの Windows Server に RDP 接続できる EC2 Instance Connect (EIC) Endpoint を試しました | DevelopersIO](https://dev.classmethod.jp/articles/rdp-connection-to-windows-server-using-ec2-instance-connect-endpoint-eic/)

### [EC2 Instance Connect Endpoint経由でRDSに接続してみた | DevelopersIO](https://dev.classmethod.jp/articles/how-to-connect-rds-instance-via-eic-endpoint/)

### [EC2 Instance Connect Endpoint経由でWindows ServerにRDP接続してみた | DevelopersIO](https://dev.classmethod.jp/articles/how-to-connect-windows-server-instance-via-eic-endpoint/)

### [EC2 Instance Connect Endpointを複数アカウント間で使う際に気を付けるべきこと | DevelopersIO](https://dev.classmethod.jp/articles/precautions-when-using-eic-endpoint-between-multiple-accounts/)

### [EC2 Instance Connect EndpointをCDKで作成してみた | DevelopersIO](https://dev.classmethod.jp/articles/create-ec2-instance-connect-endpoint-using-cdk-custom-resource/)

