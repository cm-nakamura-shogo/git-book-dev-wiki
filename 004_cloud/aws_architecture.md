# AWSアーキテクチャ例

## CloudFront + WAF

- ALB-EC2-RDS前提（NATゲートウェイつけてる）
- 証明書2個（ALB用とCloudFront用）
  - CloudFrontに使うACM証明書はバージニア北部で作らないとだめ
- WAFでWeb ACLを作る
  - 今回はIP setで許可するIPアドレスを指定
  - Web ACL作成時はGlobal(CloudFront)にしてないとだめ
- CloudFrontに作ったWeb ACLを指定
- オリジンドメインをドロップダウンリストからロードバランサーのDNS名を選んだら403出まくりで困った
  - ALBのドメインを指定したらなおった
- オリジン（今回はALB）に直接アクセスされたくない場合はManaged Prefix ListでCloudFrontのIPをSGに指定
  - https://dev.classmethod.jp/articles/amazon-cloudfront-managed-prefix-list/


## AWS Backup

- バックアップしたいリソースにタグ付けとく
