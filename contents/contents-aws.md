# contents-aws

## はじめに

ここではチームとして重要そうなAWSサービス、使うことのあるAWSサービスを紹介していきます。

サービス一覧は以下から取得しました。

- https://aws.amazon.com/jp/architecture/icons/

## コンテンツ

- ハンズオン
  - ハンズオンは以下にまとまっています。
  - [ハンズオン資料 | AWS クラウドサービス活用資料集](https://aws.amazon.com/jp/events/aws-event-resource/hands-on/)
  - よくやるハンズオン
    - [AWS Hands-on for Beginners ハンズオンはじめの一歩: AWS アカウントの作り方 & IAM 基本のキ | AWS Webinar](https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-1st-Step-2022-reg-event.html?trk=aws_introduction_page)
    - [AWS Hands-on for Beginners AWS Managed AI/ML サービス はじめの一歩 | AWS Webinar](https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-AIML-2022-reg-event.html?trk=aws_introduction_page)
    - [AWS Hands-on for Beginners 手を動かしなら学ぶ Analytics サービス入門 | AWS Webinar](https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-Analytics-2022-reg-event.html?trk=aws_introduction_page)
- Black Belt
  - 安定のBlack Belt。
  - [サービス別資料 | AWS クラウドサービス活用資料集](https://aws.amazon.com/jp/events/aws-event-resource/archive/?cards.sort-by=item.additionalFields.SortDate&cards.sort-order=desc&awsf.tech-category=*all)
- CM内のサービス毎勉強会動画
  - [このサービスは俺に聞け動画](https://drive.google.com/drive/folders/185xJP0EITHtqra_OaP9Hmv6NKe-lGrkZ)
- その他
  - AWSJさんから提供されたトレーニング関連情報も以下にあります。
    - [AWSトレーニング一覧_20220620版.xlsx - Google スプレッドシート](https://docs.google.com/spreadsheets/d/1WxLtCoQoPxoiVFH7T-5VYWiZVhRGKymQ/edit#gid=491630880)
  - 以下も結構いいかも
    - [コードで学ぶAWS入門](https://tomomano.github.io/learn-aws-by-coding/)
- 機械学習の場合
  - [aws-samples/aws-ml-enablement-workshop: 組織横断的にチームを組成し、機械学習による成長サイクルを実現する計画を立てるワークショップ](https://github.com/aws-samples/aws-ml-enablement-workshop)
  - [GitHub - aws-samples/aws-ml-jp: SageMakerで機械学習モデルを構築、学習、デプロイする方法が学べるNotebookと教材集](https://github.com/aws-samples/aws-ml-jp)
  - [GitHub - aws-sagemaker-jp/awesome-studio-lab-jp: SageMaker Studio Labの教材を紹介するリポジトリ。](https://github.com/aws-sagemaker-jp/awesome-studio-lab-jp)
  - [AWSのML講座](https://www.youtube.com/channel/UC12LqyqTQYbXatYS9AA7Nuw/playlists)
- 書籍
  - [2021-10 AWSコンテナ設計・構築[本格]入門](https://www.amazon.co.jp/dp/4815607656)
    - ECSを本格的に使いこなすための書籍
    - 書評
      - [[書評] 「AWSコンテナ設計・構築[本格]入門」は文字通り本格的にECS/Fargateを始めるのにお勧めの一冊 | DevelopersIO](https://dev.classmethod.jp/articles/bookreview-introduction-guide-aws-container-design-and-construction/)
  - [2021-12 AWS Cookbook (オライリー)](https://www.amazon.co.jp/dp/1492092606)
    - [AWS Cookbook | Github](https://github.com/AWSCookbook)
    - 参考
      - [はじまりは神本『AWS Cookbook』との邂逅　元アンチCDKの私が「CDK、できる…」と思った理由 - ログミーTech](https://logmi.jp/tech/articles/326643)
  - [2023-01 AWSで実現するモダンアプリケーション入門](https://www.amazon.co.jp/dp/4297133261)
    - hamakoさんが書評かいてたやつ
  - [2023-03 AWSコスト最適化ガイドブック](https://www.amazon.co.jp/dp/B0BYC5H9G8)

## 共通で使うサービス

共通で使うことの多いサービスです。学習の目安にしてください。

細部まで深く知っておく必要があるわけではないですが、精通していると捗ります。

- Amazon EC2
- AWS Lambda
- Amazon ECR
- Amazon ECS
- AWS Fargate
- Amazon EventBridge
- AWS Step Functions
- AWS CLI
- Amazon CloudWatch
- AWS CloudFormation
- AWS Management Console
- AWS Systems Manager
- AWS CloudTrail
- Amazon VPC
- Amazon S3

## Analytics

DA事業本部の名の通り、Analytics系のサービスも知っておくと捗ります。

- AWS Glue
- Amazon OpenSearch Service
- Amazon Redshift
- Amazon QuickSight
- Amazon Athena

## AIML

MLチームとしては以下あたりのサービスを抑えたいです。

- Amazon Comprehend
- Amazon Forecast
- Amazon Personalize
- Amazon Rekognition
- Amazon SageMaker
- Amazon Transcribe
- Amazon Bedrock

## 知っておくと役立つサービス

それ以外に知っておくと役立つサービスは以下です。

### Compute

- AWS App Runner
- AWS Batch

### Application Integration

- Amazon SNS
- Amazon SQS
- Amazon API Gateway

### Database

- Amazon Aurora
- Amazon DynamoDB
- Amazon RDS

### Developer Tools

- AWS CodeBuild
- AWS CodeCommit
- AWS CodeDeploy
- AWS CodePipeline

### Management & Governance

- AWS Config

### Networking & Content Delivery

- Amazon Route 53
- Amazon CloudFront
- AWS Cloud Map

### Security, Identity, & Compliance

- AWS Secrets Manager