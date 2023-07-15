# AWS Cognito

## Articles

- [2021-05-30 Next.js アプリに Cognito の認証を良い感じに設定する](https://zenn.dev/tatsurom/articles/next-auth-cognito)
- [2022-01-21 Amazon CognitoでSingle Sign Onを実現してみた](https://kakehashi-dev.hatenablog.com/entry/2022/01/21/080000)
- [2022-05-12 Pulumiを使ってCognitoのユーザプールを作成する例](https://dev.classmethod.jp/articles/tried-make-cognito-userpool-using-pulumi)
  - Cognito設定の参考になりそう
- [2023-05-09 ALB + EC2の構成に、Amazon CognitoのHosted UIを利用し、多要素認証（MFA）を実装してみた | DevelopersIO](https://dev.classmethod.jp/articles/alb-ec2-cognito-hosted-ui-2023/)
- [2023-07-14 【セッション資料・動画】CognitoでWebアプリケーション（not SPA）に ログインさせたい時、何を作らなくてはならないのか？ #devio2023 | DevelopersIO](https://dev.classmethod.jp/articles/what-do-i-create-when-i-want-to-log-in-to-a-web-application-with-amazon-cognito/)
  - 実装パターンやメリット、デメリットが整理されており助かる

## Updates

- [2022-08-12 AWS WAFが利用可能に](https://dev.classmethod.jp/articles/update-amazon-cognito-enables-native-support-for-aws-waf/)
  - AWS WAFのweb ACLにCognitoユーザープールを関連付けできるようになった。
  - AWS WAFを利用することでCognitoのユーザープールをWebベースの攻撃や不要なボットから保護することができるように。
