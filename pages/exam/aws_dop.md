# DOP

## Management & Governance

### Amazon CloudWatch

- 概要
  - AWS上で動作するさまざまなリソースのメトリクスを収集し稼働状況を監視できるサービス

- リージョン
  - 異なるリージョンからのメトリクスを単一のCloudWatchで取得可能。

- CloudWatch Metrics
  - 以下のシンプルなAPIで構成
    - GetMetricStatistics
    - ListMetrics
    - PutMetricData
  - Put処理はまとめて複数種類、複数時点のデータを送信することができる
    - これにより、秒間の API 実行回数の上限を回避することが可能
    - またAPIコール枚に料金が発生するためコストを抑制することも可能
  - 詳細モニタリング機能
    - デフォルトは5分間隔だが、詳細モニタリングを有効にすることにより、1分間隔にすることが可能。
    - これによりAuto Scalingなどのスケールアウトもタイミング速く実施することができる。
  - 15ヶ月しか保持できないため、永続化のためにはLambda関数をトリガーしてメトリクスを抽出し、長期保持する必要がある

- CloudWatch Logs
  - EC2, CloudTrail, Route53などのログファイルを監視することが可能
  - エラー率が閾値を超えた場合に、管理者に通知を送るなどが可能。
  - アプリケーションのログは取れないため、X-rayのエージェントが必要。

- CloudWatch Logs Metric Filter
  - メトリックフィルタは、CloudWatch Logsに送信されるログデータで探すべき用語やパターンを定義
  - メトリックフィルターを使用して、ログデータをグラフ化したりアラームを設定したりできる数値的なメトリックにする

- CloudWatch Logs Insights
  - ログを解析・可視化するフルマネージドサービス。

- CloudWatch Dashboard
  - グラフでグラフィカルにサービスやログを統合的に可視化する機能

- CloudWatch Events（Amazon EventBridge）
  - システムイベントを監視し、ルールに一致したイベントを一つ以上の関数やストリームに振り分けられる。
  - cron式やrate式により、特定の時間にトリガしたり、スケジュールが可能。

- CloudWatch Alarm
  - 監視するメトリクスが特定のしきい値を超えた場合に メールを送信するなどの通知アクションを実行
  - 設定できるアクションとしては、通知、Auto Scaling、EC2アクションのみ
    - EC2インスタンスの再起動など限定的な処理しかできない

- CloudWatch エージェント
  - EC2インスタンスやオンプレミスサーバーから、メトリクスやログを収集する機能。

- 参考
  - [CloudWatch Metricsの細かすぎて誰にも伝わらない話 - Qiita](https://qiita.com/moomindani/items/1eacbfe5b71b200a2da9)
  - [Amazon CloudWatch入門、logs、events、アラームの機能や料金につい解説 | よくわかるAWS・クラウド](https://cloudnavi.nhn-techorus.com/archives/875)

### AWS CloudFormation

- 構成要素
  - Resources（必須要素）
  - AWSTemplateFormatVersion: バージョンを記述
  - Description: コメントを記述。必ずAWSTemplateFormatVersionの後に記載する必要がある。
  - Metadata: テンプレートに関する追加情報
  - Parameters: 実行時に(スタックの作成・更新時に)テンプレートに渡す値。ResourcesおよびOutputsを参照可能。
  - Rules: Parameterを検証するルール
  - Mappings: 条件パラメータの指定に使用できるMap(辞書)
  - Conditions: 条件指定に使用。本番か開発かなど。
  - Transform: SAMを使用したり、別のテンプレートを利用するために使用。
  - Outputs: 構築後に出力させる値や、Exportフィールドにより他のテンプレートから参照させることなどが可能。

- 変更セット
  - スタックの更新をしたり、その影響度を確認することができるスタック

- ドリフト
  - テンプレートによる展開後に変更した場合に、差分をチェックする機能

- Export/Import
  - スタック間のリソース参照機能
  - スタックを互いに依存関係を持つ個々の独立した論理コンポーネントに分離するのがベストプラクティス
  - そのため依存関係は、Export / Importで対応する

- スタックセット
  - 複数のAWSアカウントやリージョンにリソースを展開できる。
  - クロスアカウントやクロスリージョンのシナリオを解決可能。

- DeletionPolicy
  - 停止後にデータを保持したい場合、DeletionPolicyを有効にする必要がある。
  - DeletionPolicyには以下の種類がある。
    - Snapshot
      - スナップショットを作成したうえで、リソースを削除する。
      - このポリシーはスナップショットが作成できるリソース(EC2やRDS)にのみ追加することができます。
    - Retain
      - リソースやコンテンツを削除せず保持します。
      - この削除ポリシーは、あらゆるリソースタイプに追加することができます。
    - Delete (Default)
      - スタックの削除時にリソースと (該当する場合) そのすべてのコンテンツを削除します。
      - この削除ポリシーは、あらゆるリソースタイプに追加することができます。

- CreationPolicy
  - ResourceSignalパラメータでTimeoutを設定することができる。
  - これによりタイムアウトを超えるまでは終了しないようになります。

- UpdatePolicy
  - WIP

- Capabilities
  - スタックテンプレートに例えばIAMリソースなどが含まれる場合、`CAPABILITY_IAM`を設定しておく必要あり
  - 設定しない場合`InsufficientCapabilitiesException`となる。
  - 参考
    - [https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateStack.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateStack.html)

- Lambdaの設定方法
  - Lambda関数のコードをzip化してS3にアップロードし、AWS::Lambda::Functionから参照することが可能
  - Node.js および Python 関数の場合で依存関係がない限り、テンプレートにインラインで関数コードを指定可能
  - バージョン変更検知には、S3Bukcet, S3Key, S3ObjectVersionいずれかの変更が必要

- Coustom Resource
  - AWS::CloudFormation::CustomResourceまたはCustom::Stringリソースタイプを使用してカスタムリソースを指定可能
  - カスタムリソースは、CloudFormationテンプレートにカスタムプロビジョニングロジックを記述し、スタックの作成、更新、削除などのスタック操作時にCloudFormationがそれを実行するための方法を提供する
  - 具体例としてはS3バケット削除前にオブジェクトを削除する、など

- AutoScalingのデプロイメントポリシー
  - AutoScalingReplacingUpdate : ASGごと置き換える
  - AutoScalingRollingUpdate : 同じASGのインスタンスをローリングアップデートする

### AWS Config

- 概要
  - リソースの変更管理が可能
  - リソースの設定変更の継続的な監視ができコンプライアンス評価が可能。
  - API実行の記録はCloudTrailを使用。
  - 変更監視はCloudWatch Eventsを使用。
    - 参考例：[特定のリソースIDの変更前と変更後をメールで通知する方法 | DevelopersIO](https://dev.classmethod.jp/articles/email-specific-resource-id/)
  - 監視できるものの例
    - WAFなどのFirewallルールの変更・追跡
    - CloudTrailが有効かどうかの監視
    - Organizationsにおける複数アカウントについてもコンプライアンス管理が可能。
    - サードパーティのリソース管理なども

- SNSとの連携
  - リソース構成への変更とリソースのタグ付けはすべてSNSトピックにストリーミングすることが可能
  - ConfigのSNSトピックは、すべての通知と構成変更のストリーミングにしか使用できない
  - そのため単一のルールのアラートを分離するためには、CloudWatch Eventsを使用する必要がある

- AWS Config Aggregator
  - 各アカウントのConfigルールによる評価の結果をまとめて表示することが可能となる機能

- 参考
  - [AWS Configとは何か？できることや利点についてもあわせて解説 | ITエンジニア派遣なら夢テクノロジー](https://www.yume-tec.co.jp/column/awsengineer/4621)
  - [AWS Config Aggregator を委任してマルチアカウント&マルチリージョンの評価を集約する - サーバーワークスエンジニアブログ](https://blog.serverworks.co.jp/organizations-config-aggregator-delegated-admin)

### AWS CloudTrail

- 概要
  - アカウントのガバナンス、コンプライアンス、運用監査、リスク監査を行うサービス
  - CloudTrailは、IAMユーザーやIAMロール経由でサービスに実行されたアクションやAPI実行を記録
  - リソースの変更やルール違反を監視する場合はAWS Configを使用
  - AWS ConfigはConfigルールを通してCloudTrailが有効かどうかをチェックする

- CloudTrailログファイルの完全性検証
  - CloudTrailがログファイルを配信した後に、ログファイルが変更、削除、または変更されていないかの判断に使用可能
  - ログの完全性を検証する正しい方法は、CloudTrail の validate-logsコマンドを使用する

- CloudWatch Eventsとの紐づけ
  - CloudWatch Events のAWS API Call via CloudTrail 機能を使用しターゲットとしてSNSを設定可能
  - これにより、イベントを発行しないAWSサービスによるアクションをトリガーとするルールを作成した処理が可能

- Organizationsとの関連
  - AWS Organizationsを利用中の場合、すべてのAWSアカウントのログをまとめて取得することが可能。
  - マスターアカウントの組織の証跡を有効とすることで、すべてのアカウントのCroudTrailイベントを同じS3バケット、CloudWatch Logs、CloudWatchイベントに配信可能。
  - AWS Organizationsを使用しない場合は、各アカウントで組織の証跡を有効化する必要あり。

- CloudTrail Insights
  - CloudTrailのログの定期的な監査を行うツール。

- Step Functionsとの統合
  - Step Functionsの人の手作業のによるアクティビティの記録などには、CloudTrailが必要となる。

### AWS Service Catalog

- 概要
  - 組織としてのガバナンスが適用されたテンプレートを、AWS利用者であるユーザー部門に利用させることができるサービス。
  - Service Catalogは、CloudFormationテンプレートを製品としてインポートする事が可能
  - CloudFormationテンプレートには、多くのAWSサービスの構成情報を記載できます。
  - これにより、スタンプを押すように統一的な環境を作成する事が出来ます。
  - 参考
    - https://dev.classmethod.jp/articles/serca/

### AWS Application Auto Scaling

- 概要
  - Amazon EC2以外の個々のAWSサービスに対して、スケーラブルなリソースを自動的にスケーリングするためのサービス

- 対象サービス
  - Computing
    - AppStream 2.0 fleets
    - Amazon Elastic Container Service (ECS) services
    - Amazon Keyspaces (for Apache Cassandra) tables
    - Lambda function provisioned concurrency
    - Spot Fleet requests
  - Database
    - Aurora replicas
    - DynamoDB tables and global secondary indexes
    - ElastiCache for Redis clusters (replication groups)
    - Amazon Neptune clusters
  - Analytics
    - Amazon EMR clusters
    - Amazon Managed Streaming for Apache Kafka (MSK) broker storage
  - ML endpoints
    - Amazon Comprehend document classification and entity recognizer endpoints
    - SageMaker endpoint variants

### AWS OpsWorks

- 概要
  - ChefとPuppetのマネージドインスタンスを提供する構成管理サービス
  - 複雑なインフラストラクチャ管理や設定を行うサービス。
  - Cassandraクラスター構成などの管理が用途として出現する
  - スタックベースやレイヤーなどの構築の用途の場合はCloudFormationではなくこちらを使用。

- スタック
  - スタックは、AWS OpsWorks Stacksのトップレベルのエンティティ
  - 集合的に管理したいインスタンスのセットを表す
  - 通常はPHPなどWebアプリケーションを提供するなどの共通の目的を持つ
  - スタックは、アプリケーションやCookbookの管理など、インスタンスのグループ全体に適用されるタスクも処理

- レイヤー
  - すべてのスタックには 1 つ以上のレイヤーがある
  - 各レイヤーはLBやAppication Serverのセットなど、スタックコンポーネントを表現
  - 各レイヤーには、5つのライフサイクルイベントのセットがありレシピとして設定可能
  - レイヤーのインスタンスでイベントが発生すると、AWS OpsWorks Stacksは自動的に適切なレシピのセットを実行

- ライフサイクルフック
  - setupフック
    - インスタンスが最初に作成されるときにのみ使用
  - configureフック
    - インスタンスが起動したり終了するたびに、すべてのインスタンスで呼び出される
  - deployフック
    - アプリがインスタンスへデプロイされるときに発火（setupにはdeployが含まれている）
  - undeployフック
    - アプリがインスタンスから削除されるときに発火
  - shutdownフック
    - Stacksへインスタンスのシャットダウンを指示した後、実際にインスタンスが終了される前に発火

- Amazon CloudWatch Eventsへの通知
  - initiated_byフィールド
    - 以下のいずれかを設定可能
      - user - API または AWS Management Console のいずれかを使用して、インスタンス状態の変更を要求したユーザー
      - auto-scaling - AWS OpsWorks Stacksの自動スケーリング機能によるインスタンスの状態変化
      - auto-healing - AWS OpsWorks Stacksの自動ヒーリング機能によるインスタンスの状態変化
  - 参考
    - [How to set up AWS OpsWorks Stacks auto healing notifications in Amazon CloudWatch Events | AWS Cloud Operations & Migrations Blog](https://aws.amazon.com/jp/blogs/mt/how-to-set-up-aws-opsworks-stacks-auto-healing-notifications-in-amazon-cloudwatch-events/)

### AWS Trusted Advisor

- 概要
  - 主に５つの機能を持つ
  - コスト最適化、セキュリティ強化、可用性向上、パフォーマンスの向上、サービスウォータのチェック

- コスト最適化
  - 使用率の低い、または使用されていない状態のリソースを検出
  - ビジネスサポートまたはエンタープライズサポートに契約している場合のみ使用可能

- セキュリティ強化
  - 脆弱性を発見し通知する
  - スナップショットやS3バケットのアクセス許可、特定のポートへの無制限アクセス、IAMの使用、MFAなど

- 可用性向上
  - Auto Scaling、ヘルスチェック、マルチAZ、バックアップ、スナップショットなどの機能が関連
  - ビジネスサポートまたはエンタープライズサポートに契約している場合のみ使用可能

- パフォーマンスの向上
  - パフォーマンスを低下させる要因を発見し、より効率的な手法があれば通知
  - ビジネスサポートまたはエンタープライズサポートに契約している場合のみ使用可能

- サービスウォータのチェック
  - 制限の80％を超えると通知

### AWS Systems Manager

- 概要
  - SSMと呼ばれることが多い。
  - プライベートVPCにあるインスタンスへの接続以外にも様々な機能がある。
  - パラメータストアなども環境変数への格納で良く使用される。

- AWS Systems Manager エージェント(SSMエージェント)
  - Systems Managerがリソースを管理できるようにするためのエージェント。
  - EC2インスタンス、オンプレサーバーなどにインストールして使用する。
  - マネージにするにはこのほか、AgentからSSM APIへのアウトバウンド経路を確保し、IAMロールを付与する必要がある
  - これらの設定はクイックセットアップでも行うことが可能

- AWS SSM インベントリ
  - マネージドインスタンスからメタデータを収集し可視化
  - 管理対象インスタンスに何がインストールされているかを把握することができる

- Document Builder
  - 運用作業をSSM自動化ドキュメントとして定義

- SSM Automation
  - メンテナンスやデプロイタスクを自動ワークフロー化できる。
  - 定義済みのワークフローを使うこともできる。
    - EC2インスタンスの再起動
    - AMIの作成、など

- Systems Manager コンソール
  - ワークフローの進行状況を確認できる。

- AWS Systems Manager Patch Manager
  - パッチ適用のプロセスを自動化する。
  - インスタンスをパッチグループで分類して管理することができる。
  - Patch Managerがサポートする各オペレーティングシステムに対して、あらかじめ定義されたパッチベースラインを提供
  - 独自のカスタムパッチベースラインを作成することも可能
    - 代替のパッチソースリポジトリを指定可能
    - パッチが承認または拒否されるかをより詳細に制御することが可能
    - ベースライン自体はカスタムできないが、RunPatchBaselineのRun Commandを含めることも可能

- AWS Systems Manager State Manager
  - 安全でスケーラブルな設定管理サービス
  - Amazon EC2 およびハイブリッドインフラストラクチャを、定義された状態に保つプロセスを自動化します。
  - シェルスクリプトによって、午前0:00にCE2インスタンスからS3バケットにログを取得する設定が可能です。

- SSMセッションマネージャ
  - SSMエージェント経由でインスタンスへのアクセスが可能
  - トンネリングアクセスにより、RDPやSSHでも接続が可能

- SSM AppConfig
  - アプリケーションの設定情報を迅速に展開するための機能
  - EC2、コンテナ、Lambdaへスケーラブルかつアプリケーションの再起動なしに展開可能
  - 本番や開発などの環境毎に異なるものもデプロイ可能

- オンプレサーバーへのSSMセットアップ
  - IAMロールを作成
  - 各サーバーに固有のアクティベーションコードとアクティベーションIDを生成して登録する
  - 登録されたインスタンスは、SSMコンソールで`mi-`というprefixが付与される

- 参考
  - [Black Belt](https://d1.awsstatic.com/webinars/jp/pdf/services/20200212_AWSBlackBelt_SystemsManager_0214.pdf)

### AWS Health

- 概要
  - リソースのパフォーマンスとAWSサービスやアカウントの可用性について継続的に可視化

- AWS_RISK_CREDENTIALS_EXPOSEDイベント
  - IAMアクセスキーがGitHubで一般に公開されたときに生成されるイベント
  - こちらはパーソナルヘルスダッシュボードサービスによって公開

## Developer Tools

### AWS CodeCommit

- 概要
  - WIP
- DR対応
  - リージョン間レプリケーション機能がないため、Lambda関数を利用して別リージョンに同期する仕組みが必要。

### AWS CodeBuild

- 概要
  - フルマネージドの継続的インテグレーション(CI)サービス。
  - ソースコードをコンパイルし、テストを実行し、デプロイ可能なパッケージを生成する。

- Build spec
  - ビルドスペックは、CodeBuildがビルドを実行するために使用するビルドコマンドと関連する設定をYAML形式でまとめたもの
  - ソースコードの一部としてビルドスペックを含めることも、ビルドプロジェクトを作成する際にビルドスペックを定義することも可能
  - ブランチ名などを参照し、artifactの名前付けに利用する場合は`CODEBUILD_SOURCE_VERSION`を使用する
  - 環境変数の一覧は以下の通り
    - [Environment variables in build environments - AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html)

- ECRとの連携
  - CLIヘルパーを使用してECRの資格情報を取得し、イメージをビルドしてからECRにプッシュする。
  - ECRの認証情報の取得は、環境変数ではなく、CodeBuild上のIAMロールとCLIヘルパーを使用する必要がある。
  - 自動的なデプロイをするためにはECRへのプッシュに反応し、CodeDeployを呼び出すCloudWatch Event Ruleを作成し、そのターゲットはECSクラスタに設定する。

### AWS CodeDeploy

- 概要
  - デプロイ対象は、Amazon EC2、AWS Fargate、AWS Lambda、オンプレミスで実行されるサーバーなどが含まれます。
  - 変更を段階的に導入し、設定可能なルールに従ってアプリケーションの正常性を追跡します。
  - エラーが発生した場合、アプリケーションデプロイは簡単に停止およびロールバックできます。

- デプロイ設定
  - EC2/オンプレ
    - One at a time ... 一つずつ置き換え
    - Half at a time ... 半分ずつ置き換え
    - All at Once ... すべて一気に置き換え
    - Min. healthy hostsで設定が可能。
  - Lambda/ECS
    - Linear
      - Stepずつ段階的にリリース。Intervalも設定可能。
    - Canary
      - 2段階でリリース。Stepは1段階での割合を示す。Intervalも設定可能。

- EC2におけるCanaryリリース
  - デプロイメントグループをわけることで実現する

- CodeDeploy エージェント
  - インスタンスにインストールして設定することで、CodeDeployのデプロイメントで使用できるようにするpkg

- App spec
  - `appspec.yml`ファイルは、各デプロイメントを一連のライフサイクル イベント フックとして管理するために使用
  - ValidateServiceフック
    - デプロイが正常に完了したことを確認することができる
    - これは最後のデプロイメントのライフサイクルイベント
    - このフックが失敗した場合にロールバックするようにCodeDeployを構成することが可能
  - フック一覧
    - [AppSpec 'hooks' section - AWS CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure-hooks.html)

- Audo Scaling Groupの一時停止
  - デプロイ中にスケールアップイベントが発生した場合、新しいインスタンスは、古いアプリとなる可能性がある
  - この問題を発生後に解決するには、影響を受けるグループに新しいアプリケーションリビジョンを再展開する
  - また、この問題を回避するために、デプロイメント中は、スケールアップ処理の一時停止を推奨
    - これは、CodeDeployによるロードバランシングに使用されるcommon_functions.shスクリプトの設定によリ実施可能
    - HANDLE_PROCS=trueの場合、デプロイ処理中に以下のAmazon EC2 Auto Scalingのイベントが自動的に停止

アズレバランス

アラームノーティフィケーション

予定されたアクション（ScheduledActions

ReplaceUnhealthy（リプレイスアンヘルシー
- 参考
  - [20210126_BlackBelt_CodeDeploy.pdf](https://d1.awsstatic.com/webinars/jp/pdf/services/20210126_BlackBelt_CodeDeploy.pdf)

### AWS CodePipeline

- 概要
  - フルマネージドの継続的デリバリー(CD)サービス。
  - ソフトウェアのリリースに必要なステップをモデル化、可視化、自動化することが可能。

- アクションとプロバイダ
  - 各ステージのアクション毎にプロバイダが決まっている。
    - [CodePipeline pipeline structure reference - AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/reference-pipeline-structure.html)
  - Source : S3, ECR, CodeCommit, CodeStarSourceConnection
  - Build : CodeBuild, Custom (CloudBee, Jenkins, TeamCity)
  - Test : CodeBuild, AWS Device Farm, Custom (BlazeMeter, Jenkins), Third-Party
  - Deploy : S3, CloudFormation, CodeDeploy, ECS, ECS (Blue/Green) by CodeDeployToECS, Beanstalk, AppConfig, OpsWorks, Service Catalog, Alexa, Custom (XebiaLabs)
  - Approval : Manual
  - Invoke : Lambda, StepFunctions

- 並列実行
  - runOrderを設定することで同じ数値を設定すれば並列に実行することができる

- CloudFormationとの連携・統合
  - CloudFormationと連携し、テンプレートの変更を本番スタックに反映前に自動的にビルドしてテストが可能。
  - CodePipelineはCloudFormationとの統合が組み込まれているので、パイプライン内でスタックの作成、更新、削除などAWS CloudFormation特有のアクションを指定することが可能。

- 複数のCodePipelineの連携
  - S3のデプロイステップを使えば、別のバケットに成果物を複製可能
  - その複製に反応して別のCodePipelineを起動すればよい。

### AWS CodeStar

- 概要
  - CI/CDの環境を最も素早く構築するためのサービス。
  - CI/CDはCloudFormationやOpsWorksでも可能だが、CodeStarは細かい設定をしなくても使用可能。
    - Beanstalkは、単体でCI/CDの構築はできない。

- 開発言語やデプロイ先は限定的なので要注意
  - 開発言語：Java, JavaScript, PHP, Ruby, Pythonなど
  - デプロイ先：EC2, Beanstalk, Lambda

## Networking & Content Delivery

### Elastic Load Balancing (ELB)

- 概要
  - EC2などの前段に配置して負荷分散をするサービス
  - ASGを関連付けることでオートスケーリングを実施したり、ヘルスチェックで正常なリソースにのみリクエストを割り当てることが可能

- ヘルスチェック
  - ヘルスチェックは、対象インスタンスに呼び出すプロトコルとポート番号、パスなどを設定する
  - HTTP 200のレスポンスコードが返れば、健全なEC2インスタンスと判断する
  - 2XX以外のステータスコードやタイムアウトを返すインスタンスは不健全と判断し、トラフィックを受け取らないようにする。
  - 参考
    - [https://docs.aws.amazon.com/ja_jp/elasticloadbalancing/latest/application/target-group-health-checks.html](https://docs.aws.amazon.com/ja_jp/elasticloadbalancing/latest/application/target-group-health-checks.html)

- Auto Scaling Groupとの連携
  - ELBのみでは、Auto Scalingは実施できないので注意する。

- スケールイン・アウトの繰り返し抑制
  - クールダウンタイマーの値を見直す。
  - デフォルト値は300秒である。
  - CloudWatchと連携して、スケールが設定されるがその際のアラーム閾値を見直す。

- スティッキーセッション
  - セッション中に同じユーザから来たリクエストを同一インスタンスで処理することが可能。

- Connection Draining
  - 接続をオープンとしたまま、登録解除・異常なインスタンスへの送信を停止できる機能。
  - 登録解除の待ち時間として、タイムタイムアウトを設定できる(1～3600秒、デフォルト300秒)。
  - タイムアウトを過ぎると強制的に停止する。

- ステータスコードについて
  - [https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/](https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/)
  - HTTPCode_Backend_2XX, HTTPCode_Backend_4XX, HTTPCode_Backend_5XX
    - EC2インスタンスに基づくステータスコード
  - HTTPCode_ELB_4XX
    - 解釈不能なHTTPの場合、ELB時点でエラーとなる
  - HTTPCode_ELB_5XX
    - 502: 解釈不能なレスポンスがEC2インスタンスから来た場合、このエラーとなる。
    - 503: 様々な要因が考えられる。
      - ELBに登録されたインスタンスが無い場合
      - ELBに登録されたインスタンスがあるが、healthyなものがない場合
      - スケールアップ中で送信先インスタンスが切り替わり中の場合
      - 突発的な負荷増加でELBの待ち行列(surge queue)があふれた場合

- メトリクス
  - RequestCount
    - HTTPCode_Backend_XXXの合計数
  - SurgeQueueLength
    - ELB内の待ち行列にたまっているリクエスト数
    - 突発的なリクエスト増がない場合0を維持
  - SpilloverCount
    - HTTPCode_ELB_5XXが返った数

- クロスゾーン負荷分散
  - 複数のAZにまたがる分散を行うことができる。
  - クライアントがDNSルックアップをキャッシュする環境では、クロスゾーン負荷分散が無効な場合いずれかのAZに不可が集中する可能性がある。
  - ALBでは常に有効となり無効にできない。
  - CLB, NLBは作成方法によっては無効となるので、明示的な有効化が必要になる場合がある。
    - NLBは必ず無効がデフォルトとなる。
  - 参考
    - [ELBの種類によるクロスゾーン負荷分散のデフォルト値調べ | DevelopersIO](https://dev.classmethod.jp/articles/elb_crosszone_load_balancing_default_value/)

- ソース情報の維持
  - ELBを経由すると通常ソースのIPなどの情報が失われる。
  - これを維持するためには以下を使用する。
    - X-Forwarded-For (XFF)
      - HTTPのレイヤではこれを使用する。
    - Proxy Protocol
      - TCPのレイヤではこれを使用する。
  - 参考
    - [Proxy Protocol とは？ - Qiita](https://qiita.com/miyuki_samitani/items/80353b1b22f5ee9c41a8)

- ELBとEIP
  - ELBにEIPを割り当てて使用することはできない。

- 参考
  - [ELBの挙動とCloudWatchメトリクスの読み方を徹底的に理解する](https://dev.classmethod.jp/articles/elb-and-cloudwatch-metrics-in-depth/)

## Compute

### Amazon Elastic Compute Cloud (Amazon EC2)

- インスタンスファミリー
  - 汎用: T,M,A
    - T: Turbo. バーストタイプ
    - M: Most scenarios. 標準的なやつ
    - A: Arm. ARMプロセッサタイプ(AWS Graviton)
    - Mac: Apple Mac Mini搭載
  - コンピューティング最適化: C
    - C: Compute. 計算パフォーマンスが高い。
  - メモリ最適化: R,X,Z
    - R: RAM. メモリ最適化
    - X: Extra large memory. 最大メモリ量が大きい
    - Z: Hz. 高クロックなコア搭載モデル。
  - 高速コンピューティング: P,G,F,Inf,etc
    - P: general Purpose. 汎用GPU搭載
    - G: Graphics. グラフィックス特化GPUタイプ
    - F: FPGA. FPGAモデル
    - Inf: Inference. 機械学習推論に最適化されたタイプ。AWSが開発した Inferentia チップが搭載。
    - Trn: Trainium. AWSが開発したML用チップ Trainium 搭載タイプ
    - DL: Deep Learning. Gaudiアクセラレータ搭載タイプ
    - VT: Video Transcoding. 最大4K解像度に対応したリアルタイムトランスコーディングが可能なタイプ(Xilinx U30 Acceralatorが搭載)
  - ストレージ最適化: I,D,H
    - I: IO Performance. NVMe SSD搭載でIO性能が高い
    - D: Dense storage. 最大48TBのHDD搭載
    - H: High disk thoughput. 高スループットタイプ。これもHDD。
  - 参考
    - https://otomosa.com/aws/post-1870/
    - https://aws.amazon.com/jp/ec2/instance-types/

- 購入方法
  - オンデマンド
  - リザーブド
  - スポット
  - オンデマンドのキャパシティ予約 + Savings Plans

- リザーブド・コンバーティブル
  - インスタンスファミリー・OS・テナンシー・支払いオプションを変更可能。
  - スタンダードでも、AZ・インスタンスサイズ・ネットワークタイプは変更できる。

- 物理専有型
  - ハードウェア専有インスタンス(Dedicated Instance)
    - 専用HWのVPCで実行されるEC2インスタンス。
    - VPC構成をする際にdedicatedというのを選ぶと選択することができる。
    - 他のAWSアカウントから分離したインスタンスとなるが、同じアカウント内では共有する可能性がある。
    - またハードウェアを専有できるが、どのハードウェアで起動するかは指定することができない。
  - Dedicated Host
    - 同じアカウント内でも共有しない設定が可能なインスタンス形式。
    - IAMグループなどで閉じたインスタンスにすることができる。
    - 用途としては、オンプレのライセンスサーバーなどをAWSに移行したい場合など。
      - CPUソケット数がライセンスに効く場合など
    - ホストのアフィニティ設定をhostにしておくと、停止して再起動した場合でも同じハードウェアを利用できる。
  - ベアメタル(Bare Metal)
    - サーバーのProcessorやMemoryにアクセス可能なインスタンス。
    - 下層のハードウェアレベルまでアクセス可能。

- ユーザーデータ
  - 起動時に実行したいコマンドを記述することができる。

- 起動設定と起動テンプレート
  - 起動設定は、AMIが変更されると再作成が必要、バージョン管理が不可など機能が少ない。
  - 起動テンプレートはバージョン管理が可能。AMIと独立して設定ができる。
    - AMIは「起動テンプレートに含めない」という設定が可能。
  - 双方とも、Auto Scalingグループに紐づけする。
  - そのAuto ScalingグループをELBに紐づけすることが可能。S

- インスタンス間のネットワーク高速化
  - クラスタープレイスメントグループを設定する。
  - 拡張ネットワーキングをサポートするインスタンスタイプを選択
  - 拡張ネットワーキングの種類は以下の通り
    - ENA (Elastic Network Adapter)
      - 最大100Gbpsを実現するための拡張ネットワーク
    - Intel 82599 Virtual Function (VF) インターフェイス
      - 最大10Gbpsを実現するための拡張ネットワーク
  - 拡張ネットワーキングの方式のことを、シングルルート I/O 仮想化 (SR-IOV) とも呼ぶ。

- プレイスメントグループ
  - プレイスメントグループは設定後に、起動するという手順となる。
  - 異なるインスタンスタイプをグループにすることはできない。
  - インスタンスを追加する場合は、一旦プレイスメントグループを停止する必要がある。（停止すれば追加可能）
  - 種類
    - クラスタープレイスメントグループ
      - パフォーマンス向上が目的。単一AZ内でグループ化し、複数のVPC Peeringにまたがることも可能。
      - グループ内のインスタンスは、TCP/IPトラフィックのスループット上限が高くなり、インスタンス間通信の速度が向上する。
    - パーティションプレイスメントグループ
      - 耐障害性が目的。
      - 複数パーティションに分けられ、パーティション毎にラックがあり、パーティション同士はラックを共有しない。
    - スプレッドプレイスメントグループ
      - 更なる耐障害性が目的。
      - パーティションあたり1インスタンス構成となり、異なるラックにそれぞれのインスタンスを配置できるグループ。
  - その性質上、複数のAZには構成できないため注意する。

- VM Import/Export
  - オンプレ環境の仮想マシンをAWSにインポートする機能

- store-backed / EBS-backed
  - store-backedはインスタンスストアがroot volumeのもの。
  - 停止すると、インスタンスストアのデータは自動的に削除される揮発型。

- store-backedなEC2のバックアップ
  - AMIを作成する必要がある。 ec2-bundle-volやec2-upload-bundleなどのAMIツールが必要です。
  - EBS-backedとは異なり、EC2 CLIやマネジメントコンソールでは実施できない。

- キーペアの管理
  - AMIの複製では、キーペアはコピーされないため、既存のキーを使う場合には再度インポートが必要となる。
  - 公開鍵（Authorizedキー）は自動で内包されて複製されるが、秘密鍵（PEMキー）はユーザーの責任で移行が必要。

- 複数のサーバーSSL証明書の設定
  - SSL通信は、HTTP前段階で確率され、その際にSSLサーバー証明書も使用される。
  - HTTPの前段階ではホスト名ではなくIPアドレス等を使って通信されます。
  - そのため、SSLサーバー証明書はIPアドレス毎に一つまで有効となります。
  - EC2に複数設定したい場合は、複数のENIで各ENIにEIPを設定する必要があります。
  - 参考
    - [1台のWebサーバで複数の証明書を運用する際の注意点は？ | SSLサーバ証明書のクロストラスト](https://xtrust.jp/support/faq/faq09/a008/)

- クライアント側のSSL証明書設定
  - Webサーバーとの直接的なTCP通信が必要となるので注意する。
  - そのためELBは、HTTPSではなくTCPで設定する必要がある。

- Bashスクリプトの設定
  - OSのセッティング等に使用する。

- HVM AMI
  - 完全に仮想化された一連のハードウェアを備えており、イメージのルートブロックデバイスのマスターブートレコードを実行することによって起動します。
  - ホストシステム上の基盤となるハードウェアへの高速なアクセスを可能にするハードウェア拡張を利用できます。
  - 現在はHVM AMIが推奨されており、対するものはPV AMI
  - 参考
    - [EC2の仮想化方式についてのおぼえがき - kasei_sanのブログ](https://blog.kasei-san.com/entry/2018/01/10/003933)
### AWS Elastic Beanstalk

- 自動的にデプロイ・スケーリングを行うサービス。
  - キャパシティのプロビジョニング
  - 負荷分散
  - Auto Scaling
  - ヘルスチェック
  - パッチ配布

- ユースケースとしては以下
  - Webアプリケーション
  - ワーカー環境
    - ただしBatch処理などは対象外。
  - Amazon ECSなどのDockerにホストされたアプリケーションも対象。

- Dockerコンテナ
  - DockerコンテナからのWebアプリケーションのデプロイをサポート
  - Dockerコンテナでは、独自のランタイム環境を定義することができる
  - Dockerrun.aws.jsonファイル
    - Elastic Beanstalk固有のJSONファイル
    - Dockerコンテナ群をElastic Beanstalkアプリケーションとしてデプロイする方法を記述する

- 運用や監視にも使用することができる。

- デプロイポリシー
  - デプロイポリシーの種類は以下の通り。
    - All at Once
      - すべてのインスタンスをアップデートする
      - ダウンタイムが一瞬発生するが、最も早い。ただし失敗した場合は全滅する。
    - Rolling
      - バッチ毎に新しくする。バッチ50%であれば、半分を新しくする。
      - 更新中は使用可能なインスタンス数が減る。
      - ダウンタイムは発生しないが、古いものと新しいものが混在する。
    - Rolling with additional batch
      - バッチ単位で新しいインスタンスを起動して、新しくする。
      - Rollingと違い、使用可能なインスタンス数が減らない。
      - ただし古いものと新しいものの混在する状態は変わらない。
    - Immutable
      - 新しいAutoScalingグループを作成してそこで１つの新しいインスタンスを起動して、新しいものを動かす。
      - そしてそのAutoScalingグループをELBにアタッチしてうまく動くか確認する。
      - OKであれば残りのインスタンをまた新規に立ち上げて、新しいものを動かす。
      - その後、もともとのAutoScalingグループをELBから削除する。
      - Immutableでも古いものと新しいものの混在する状態は変わらない。
  - 単一インスタンスの場合、All at OnceもしくはImmutableしか選択できない。
  - 混在を避けたい場合は、Blue/Greenデプロイを実施する。ただしこれは、Beanstalkのデプロイポリシーには含まれないため、OpsWork等が必要となる。
    - Blue/Greenデプロイでは、ELBごと環境をクローンしてAll at Onceでデプロイすればよい。
    - その後、ELBに割り当たっているDNS名をスワップする。
    - 逆にローリングデプロイは、本番サーバーを新しいものに段階的に切り替える、短時間に置き換えることを目的とした方式。
  - 以下を参考。
    - [https://dev.classmethod.jp/articles/elastic-beanstalk-deploy-policy/](https://dev.classmethod.jp/articles/elastic-beanstalk-deploy-policy/)

- データベース削除ポリシー
  - 保持を有効化することで、RDSをBeanstalkからデカップリングしてもデータが削除されない。

- `.ebextensions/*.config`
  - プロジェクトのソースコードに上記を同梱することで使用するAWS環境をカスタマイズできる
  - configファイルは拡張子が合っていれば任意に名前を付けてよい
    - ELBの設定変更 : `elb.config`
    - DBのマイグレーション : `db-migration.config`
  - コマンド種類
    - `option_settings` : Elastic Beanstalk環境、その中のAWSリソース、およびアプリケーションを実行するソフトウェアを設定可能（ALBのリダイレクトルールなど）
    - `command` : EC2インスタンス上でコマンドを実行する。Webサーバーのセットアップよりも前に行われる。`leader_only`は設定できないため、leaderのみが良い場合は`container_command`を使用する。
    - `container_command` : アプリが動作するコンテナインスタンスから発行するコマンド。`leader_only`の場合はleaderのみが実行する。Webサーバーのセットアップ後、アプリが実行される前に行われる。
  - 参考
    - [Advanced environment customization with configuration files (.ebextensions) - AWS Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html)

## Containers

### Amazon Elastic Container Service (Amazon ECS)

- 権限付与
  - ロールが３種類あるので注意する
  - タスクロール
    - コンテナ内のアプリケーションからAWSサービスを利用する場合に設定するロール
  - タスク実行ロール
    - コンテナエージェントが必要とするロール
    - もうちょいインフラ側のイメージで、ECRやCloudWatch Logsへの権限はこちら
    - マネージドで`ecsTaskExecutionRole`というロールがある
  - EC2 起動タイプのコンテナインスタンスの IAM ロール
    - ECS タスクを動かす土台となる EC2 インスタンスに設定される IAM ロール
    - こちらもマネージドで`ecsInstanceRole`というものがあり、いじるひつようは基本ない

- 起動モード
  - EC2
    - EC2インスタンスを起動する。
  - Fargate
    - ECS・EKSで利用できる専用のコンピューティングエンジン
    - インスタンスの管理が不要(CPUやメモリなどを定義する)
    - 秒単位で数万個のコンテナ起動が可能

- トラフィック制御
  - ELBと連携して実施することができる。

- Capacity Provider Reservation
  - Auto Scalingグループを構成するために、Capacity Provider Reservationを使用する

- awslogsドライバ
  - ECSタスク定義にawslogsドライバを含めることができ、ネイティブでCloudWatch Logsに書き込むことができる
  - ログドライバへの権限を付与する必要があるのはタスク実行ロール

## Security, Identity, & Compliance

### Amazon Inspector

- 概要
  - セキュリティ評価を自動で実施するサービス
  - アプリケーションに対して、脆弱性やベストプラクティスからの逸脱がないかなどを自動で評価できます。

- AMIの検査
  - StepFunctionなどを使用し、EC2の起動、CheckVulnerabilitiesのタグ付与、Inspectorでの評価、EC2終了までを行う必要がある。
  - Inspector自身でEC2の起動などはできない。

### Amazon Macie

- 概要
  - 機械学習を使用してAWS内の機密データを自動的に検出、分類、保護するセキュリティサービス
  - S3内の機密データを検出・分類・保護することが可能

### Amazon GuardDuty

- 概要
  - アカウントとワークロードを保護するために、悪意のある活動や不正な動作を継続的に監視する脅威検出サービス

### AWS Secrets Manager

- 概要
  - セキュアな資格情報を保持するために使用するサービス。
  - RDSやAmazon Document DB, Redshiftの認証情報をネイティブにローテート可能
  - DymanoDBはサポートしていない。

- 拡張
  - Secrets Managerを拡張して使用することができる
  - EC2上でホストされているOracleデータベースの認証情報の管理など
  - OAuthリフレッシュトークンなど、他の認証情報をローテートすることも可能


## Application Integration

### Amazon API Gateway

- 概要
  - LambdaやSteep Functions、Endpoint on EC2などの前に設置し、公開されたAPIとして利用できる。
  - REST APIおよびWebSocket APIを作成可能
  - 一時的な高負荷対応には、スロットリング制限設定とキャッシュを有効化を実施する。
  - APIコールとデータ量に応じた費用のみが発生する。
  - 同時実行数は10,000

- ステージ
  - APIのスナップショットであるデプロイメントへの名前付き参照
  - ステージの設定では以下が可能
    - キャッシュの有効化
    - リクエストスロットルのカスタマイズ
    - ロギングの設定
    - ステージ変数の定義
    - テスト用のカナリアリリースのアタッチ
    - など

- API Gatewayの実行ロール
  - Lamda関数のARNを設定し、API GatewayがLambdaを呼び出すことを許可する権限を持つIAMロールを設定する。

- 認証(Lambda Authorizer)
  - LambdaコンソールでAPI Gateway Lambda authorizer関数を作成する。
  - Lambda Authorizerには２種類ある。
    - トークンベース
      - JSON ウェブトークン (JWT) や OAuth トークンなどのベアラートークンで発信者 ID を受け取ります。
      - これにより、AuthやSAML、CognitoなどのBearer Tokenによる認可戦略を使用できる。
    - リクエストパラメータベース
      - ヘッダー、クエリ文字列パラメータ、stageVariables、および $context 変数の組み合わせで、発信者 ID を受け取ります。 
  - またこのAuthorizer関数も、API Gatewayの実行ロールに設定する必要がある。
  - 参考
    - [API Gateway Lambda オーソライザーを使用する - Amazon API Gateway](https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html)

- プロキシ統合
  - プロキシ統合を使用することで、Lambda関数内でリクエストを生の状態で処理できる。
  - これによりマッピングを手動で定義する必要がなく簡単に利用が可能。
  - 参考
    - [[初心者向け] Lambda 非プロキシ統合で API Gateway API をビルドする をプロキシ統合にして比較してみる | DevelopersIO](https://dev.classmethod.jp/articles/for-beginner-build-apigateway-with-noproxy-and-proxy-lambda/)

- API実行状況の監視
  - CloudWatchを使用して監視する。API GatewayからCloudWatchへデフォルト1分間隔でメトリクスデータが送信されます。
  - メトリクスの内容は以下です。
    - 4XXError: 指定期間のクライアント側のエラー数
    - 5XXError: 指定期間のサーバー側のエラー数
    - CacheHitCount: APIキャッシュが有効な場合に、指定期間にAPIキャッシュから配信されたリクエスト数
    - CacheMissCount: APIキャッシュが有効な場合に、指定期間にAPIキャッシュではなくバックエンドから配信されたリクエスト数
    - Count: 指定期間のリクエスト数
    - IntegrationLatency: API Gatewayがリクエストを中継してからバックエンドからレスポンスを受け取るまでの時間
    - Latency: API Gatewayがクライアントからリクエストを受け取ってからクライアントにレスポンスを返すまでの時間

- デプロイステージ
  - アルファ、ベータ、プロダクションなど、各 API 用の複数のリリースステージを管理できます。
  - ステージ変数を使用することで、異なるバックエンドのエンドポイントとやり取りするよう API デプロイステージを設定できます。

- マッピングテンプレート
  - リクエストとレスポンスのデータマッピングをセットアップすることができます。
  - v1 -> v2への更新時に古い方でも動作するために、静的マッピングでデフォルト値を追加することで前方互換を保てる。

- タイムアウト
  - 統合タイムアウトの範囲は、50msec～29secで設定できる。
  - Lambdaの実行時間制限等に引っかからない場合でも、この設定によりAPI Gateway側でタイムアウトする場合がある。

- エッジ最適化APIエンドポイント
  - APIリクエストが最寄りのCloudFrontエッジロケーションにルーティングされる。
  - これによりアップロード処理などの高速化が期待できる。

- Step Functionsとの統合
  - LambdaだけでなくStep Functionsとの統合も可能
  - Lamdaの同時実行数は1,000であるため、それ以上の要件がある場合はStep Functionsが選択肢となる

## Database

### Amazon Aurora

- 対応インスタンスタイプ
  - T,およびR,X

- 高速な回復性
  - リードレプリカ別リージョンに構成すれば、リージョン障害時でも使用することが可能。

- RDSとの比較
  - 一日のトランザクション数が10,000を超えるなどのケースはAuroraを選択する。

- マルチマスタ構成
  - Writerを複数別AZにスケーラブルに構築可能
  - どのノード、AZが落ちてもダウンタイムがゼロとなる
  - マルチマスタ構成の場合、すべてが読み書き可能なインスタンスのため、リードレプリカは利用できない。

- RDSからの移行
  - RDSのスナップショットを用いてAuroraに移行をする。

- エンドポイントの種類
  - Auroraは通常、クラスターとして扱うため、エンドポイントが抽象化され、自動的なロードバランシングが可能
  - 特定のインスタンスを別用途として使用する場合などは、カスタムエンドポイントを構成することも可能
  - エンドポイントの種類は以下の通りです。
    - クラスターエンドポイント(ライターエンドポイント)
      - DDLなどの書き込みを実行できる唯一のエンドポイントです。
      - DBクラスターの現在のプライマリインスタンスに接続します。
      - このエンドポイントでは、すべてのオペレーション(CRUD)が可能です。
      - フェイルオーバーにより新しいインスタンスに自動的に接続されます。
    - リーダーエンドポイント
      - 読み込み専用のエンドポイントです。
      - 複数のリードレプリカがクラスターにある場合、負荷分散を実施します。
      - クラスタにプライマリインスタンスのみが含まれている場合、プライマリインスタンスに接続され、すべてのオペレーション(CRUD)が可能となります。
    - カスタムエンドポイント
      - 選択したDBインスタンスのセットを表します。
      - 最大5つのカスタムエンドポイントを作成できます。
      - またAurora Serverlessでは、カスタムエンドポイントを使用できません。
      - 以下のような用途が考えられます。
        - 社内ユーザーをレポート生成やアドホック (1 回だけの) クエリ実行用の低容量インスタンスに振り向けたい
    - インスタンスエンドポイント
      - クラスター内の特定のDBインスタンスに接続します。
      - DBクラスター接続の直接制御を提供する。

- Global Database
  - グローバルに分散したアプリケーション向けに設計されている
  - 1つのAmazon Auroraデータベースが複数のAWSリージョンにまたがることを可能に

### Amazon DynamoDB

- 概要
  - フルマネージド、サーバーレスの key-value NoSQL データベース

- マルチAZ構成は不可。（そもそもリージョン内の3つのAZでレプリケーションをするため）

- Auto Scalingの設定はRead/Write双方ともに対応。
  - トラフィック変化に応じたスループット向上を行うことができる。

- 登録・変更などをトリガにlambda実行などをする場合は、DynamoDB Streamを有効化する。
  - この変更情報は最大24時間保存される。
  - Streamを使わずに、LambdaとCloudWatch Eventsを連携することでも構築可能。

- DynamoDB Accelerator (DAX)
  - Amazon DynamoDB用のフルマネージド、高可用性、インメモリキャッシュ。
  - 最大10倍のパフォーマンス向上が可能。
  - ただし高コストであり、恒常的な対策であるため、一時的な負荷増にはAuto Scalingを活用する。

- 整合性モデルの変更可能
  - 結果整合性と強い整合性を設定で変更することができる。

- キャパシティモード
  - プロビジョンドとオンデマンドの２種類のモードがある。
  - プロビジョンドの場合、容量を超過した場合は、ProvisionedThroughputExceededExceptionが発生する。
    - プロビジョンドスループットと、コンシュームドスループットのメトリクスを確認することで、どのキャパシティが不足しているのか確認することができます。 

- Auto Scaling
  - オプションプロビジョニングモードを選択した場合、アプリケーションに必要な 1 秒あたりの読み込みと書き込みの回数を指定します。
  - 最大、最小のキャパシティユニットを設定し、トラフィックに応じた自動調整が可能です。
  - コストの予測可能性を得るため、定義されたリクエストレート以下に維持されるように DynamoDB を制御することができます。

- キャパシティユニットの計算
  - RCU
    - 1ユニットで、強い整合性の場合、最大4KBの項目を1秒あたり1回実行可能
    - 1ユニットで、結果整合性の場合、最大4KBの項目を1秒あたり2回実行可能
    - 4KBを超える場合、多くのRCUを消費する。
  - WCU
    - 1ユニットで、最大1KBの項目を1秒あたり1回実行可能

- LSI(local secondary Index)
  - 追加でソートキーを増やすイメージ
  - 1テーブルに５つ作成可能でテーブル作成時に作成
  - 検索を詳細にしたい場合などに使用。
  - パーティションキーとソートキーを組み合わせることで複合キーを作成できる。

- GSI(global secondary Index)
  - テーブル全体をスキャンして全体で何かを算出したい場合に使用する。
  - データに対して別のハッシュキーを設定できる。
  - 1テーブルに５つ作成可能、テーブル作成後に作成が可能。
  - テーブルが複数される。

- 大量レコード対応
  - 例えば週毎にテーブルを分けることで、検索性や削除が簡単にできる。

- グローバルテーブル
  - リージョン間でのレプリケートが可能となる。
  - レプリカ間の変更の伝搬は、DynamoDB Streamsを使用して行われる。（そのため、Streamsは有効となる）
  - 参考
    - https://aws.amazon.com/jp/blogs/news/how-to-use-amazon-dynamodb-global-tables-to-power-multiregion-architectures/

- カーディナリティ
  - スループットを効率的に使用するためには、カーディナリティが高いパーティションキーを設定する。

- アクセス制御
  - アクセスを細かく制御するためにFine Grained Access Control (FGAC)を使用する。
  - FGACはIAMと組み合わせて使用される。

- Lambda連携
  - データ取得や集計をスケーラブルに実施するために、SQSとLambda関数を連携下処理で非同期実行処理を実施できる。

- DynamoDB トランザクション
  - DynamoDBテーブル内およびテーブル間の複数の項目を調整したり、変更しないといった開発設定が可能です。
  - 複数のアクションをまとめてグループ化し、1 つのオールオアナッシングの TransactWriteItems または TransactGetItems オペレーションとして送信できます。

- DynamoDB Stream
  - DynamoDB 項目に対する変更をキャプチャすることができます。
  - 前述のように、リージョン間でのレプリケートにも使用される。
  - ２つを超えるプロセス（例えば３つのLambdaなど）を紐づけるとスロットリングが発生する
  - その場合はSNS等を使ったファンアウト構成が必要。

- 参考
  - [コンセプトから学ぶAmazon DynamoDB](https://dev.classmethod.jp/referencecat/conceptual-learning-about-dynamodb/)
  - [【入門】私を苦しめたDynamoDB | フューチャー技術ブログ](https://future-architect.github.io/articles/20200818/)

### Amazon ElastiCache

- 概要
  - 高速データ処理が可能なNoSQL型のデータベース

- ElastiCache for Memcached
  - 単純なセッションデータ管理などの場合は、シンプルなMemcachedを選択

- ElastiCache for Redis
  - 計算処理がある場合はRedisを選択する。
  - リアルタイムトランザクションおよび分析処理のユースケースに最適な選択肢
  - レプリケーションや自動フェイルオーバー(高可用性)、データの永続性という面ではRedisが有用
  - Redisの場合、Redisレプリケーションを有効化して、高可用クラスター構成とすることが可能。

- Redisクラスターにおけるデータのディザスターリカバリー(DR)およびフォールトトレランス
  - 自動バックアップ
  - Redis AOF(Append-Only File)を使用した手動バックアップ
  - 自動フェイルオーバーを備えたマルチAZのセットアップ

- Redisリードレプリカ
  - レプリカノードを追加することで読み取り性能をスケールさせることができます。

- Redisノードタイプ
  - ノードタイプを変更することで性能を向上させることができる。

## Analytics

### Amazon Kinesis Data Firehose

- 概要
  - 保存がメインの用途となる機能。
  - Kinesis Data StreamのConsumerとして指定することで使用する。

- ロード先
  - S3やRedShift、Elasticsearch Serviceにロードできる。
  - DynamoDBはロード先指定することができないので注意

- Lambda統合
  - Lambdaと統合し、データ変換処理をしながらロードすることも可能。
  - 構成例
    - 変換前のソースレコードをバックアップ用S3バケットに保存
    - 変換済みレコードを中間S3バケットに保存
    - 中間S3バケットからRedshiftにCOPYなども可能。

### Amazon Kinesis Data Stream

- 概要
  - データ欠落がなく耐久性があり、重複無し・順序維持をした伝送が可能。
  - データを送信するProducerとデータを処理するConsumerという構成となる。

- データ保持期間
  - 保持期間のデフォルトは24時間。設定によっては365日まで変更可能。

- Producer側
  - Kinesis Agent
    - データを収集して送信するスタンドアロンのJavaアプリケーション
  - Kinesis Producer Library (KPL)
    - データを送信するOSSの補助ライブラリ
  - Fluent plugin for Amazon Kinesis
    - OSSのFluentdの出力プラグイン
  - Kinesis Data Generator (KDG)
    - テストデータの送信ができる仕組み

- Consumer側
  - Kinesis Client Library (KCL)を用いてデータ処理・分析を実施する。
    - KCLを利用してKinesisアプリケーションを作成する。
    - EC2インスタンスで動かすことができ、KCL Workerが各インスタンス内の処理ユニット。
    - Record Processor Factory で Record Processorを作成
    - 1つの Record Processor は1つのシャードに対応し、複数のRecord ProcessorをKCL Workerにマッピング可能
  - KCLのステート管理には DynamoDB が使用されている。
  - またLambdaやEMRでデータを処理することが可能。
  - 後述のFirehoseおよびAnalyticsをConsumerとして設定することもできる。

- シャード数
  - スループットを増減させるためにはシャード数を調整する

- MillisBehindLatestメトリック
  - シャード内の最新のレコード（チップ）から現在のイテレータが遅れている時間を表すメトリック
  - メトリクスはKCLが動くインスタンスをAuto Scalingする際に使用することが可能

- Amazon Kinesis Connector Library
  - DynamoDB, Redshift, S3, Elasticsearchに対するコネクタが利用可能。

- 参考
  - [Amazon Kinesis | AWS Black Belt Online Seminar](https://d1.awsstatic.com/webinars/jp/pdf/services/20180110_AWS-BlackBelt-Kinesis.pdf)

## Storage

### Amazon Elastic File System (Amazon EFS)

- 接続方法
  - AZ毎に１つのマウントターゲットが必要
  - NFSv4を使用

- リージョン間レプリケーション
  - RPOとRTOの低いレプリケーションをするには双方のリージョンにASGを構成したクラスタを使用
  - S3経由で変更の書き出しとロードを行うため高コストとなる
  - よりネイティブにするには AWS DataSync を使用する

- ライフサイクル管理
  - 自動的なファイルストレージ管理
  - 30日アクセスされなかったファイルをEFS IAクラスに移行する。
  - データ削除などのライフサイクル管理設定はできない。

- S3との比較
  - S3と異なりインターネットからの直接アクセスは不可能
  - EFSは強い整合性やファイルのロックなどが可能であり

- マウントヘルパー
  - amazon-efs-utilsパッケージ
  - 暗号化オプションを設定する際などに使用する。

- Windows対応
  - SMB形式をサポートしておらず、またWindows OSのEC2インスタンスもサポートされていない。