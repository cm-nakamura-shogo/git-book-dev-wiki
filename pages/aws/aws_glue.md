# AWS Glue

ETLを行うサービス

## 概要

Glueジョブが以下のサービス構成です。

- Glueジョブ
- Glue Python Shellジョブ
- Glue Sparkジョブ
- Glue Rayジョブ　←これはどの階層なのか分からなかった
- Glue DataBrew

基本的にGlueジョブというと分散処理エンジンのSparkを積み込んだGlue Sparkジョブで、これを使わないとあんまGlueを使う意味もないと思うのですが、
Python Shellジョブが非常に使い勝手がよく、市民権を得ている感じになっています。（個人の感想）

Glue RayはSparkが使えない人向けに去年新しくでたやつらしいです。

DataBrewは、GUI操作でETLを作れるみたいなのがちょっと前に流行って出てきた感じのやつです。Glue Stuioとはちょっと違って、データを見ながら処理を作っていく感じです

ワークフロー機能は昔からある機能で、簡易的にGlueジョブの処理順だったり起動タイマーを設定できるんですが、普通にStep Functionsでいいかなぁと思っています。

ブループリントはGlueワークフローを一発でデプロイできるやつだったはずですが、あんま使ったことはないですね。
良さそうだったら掘ってもらってもいいと思うのですが、どうせならCodeCatalystのAWS Glue ETLブループリントの方からやった方がナウでヤングな感じがします。

Glue Studioはビジュアルエディタでぽちぽちするやつですね。

Materialied VIewと普通のviewの違いは、Glue Elastic Viewsという機能があってMaterialied VIewを提供しているはずなのですが、一生プレビューなのでviewしかないと思っていてよいと思います。

LakeFormationとGlueの関係性は、LFはタグベースでアクセスコントロールするので、Glueジョブに付けるIAMロールに対してタグをつけることでテーブルへのアクセス制御をすることになると思います。

## Git統合

- 2022-10-13にアップデートされた機能
  - [https://aws.amazon.com/jp/about-aws/whats-new/2022/10/aws-glue-git-integration/](https://aws.amazon.com/jp/about-aws/whats-new/2022/10/aws-glue-git-integration/)
  - [https://dev.classmethod.jp/articles/aws-glue-git-integration/](https://dev.classmethod.jp/articles/aws-glue-git-integration/)
- CodeCommitおよびGitHubと連携してジョブをバージョン管理可能。
- 1つのレポジトリで複数ジョブに対応させられる。
  - ジョブ毎にフォルダが分かれる。
- pushした際のコンフリクトは強制上書きされるため注意が必要。
  - ベストプラクティスとして、ブランチをユーザ毎に分けるなどをした方が良い。

## 参考記事

### [2023-04-24 [Step Functions + Glue] Glueジョブ終了時の出力を次のステートに流す。エラーハンドリングもできるよ！ | DevelopersIO](https://dev.classmethod.jp/articles/step-functions-glue-sync-output/)


## アップデート

### [2023-04-17 リソース使用状況を監視する新機能を発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-glue-monitor-usage-resources/)

- Cloudwatchで特定のGlueリソースの利用状況を監視し、適切なCloudWatchアラームを設定することが可能に

### [2023-04-24 CrawlersがPartition Indexの作成に対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-glue-crawlers-creating-partition-indexes/)

Glue CrawlerはS3からデータスキーマとパーティションを抽出し、AWS Glue Data Catalogに入力することでメタデータを最新の状態に保つ機能

本リリースでは、AWS Glue Crawlerが新しいAWS Glue Data Catalogテーブルを作成する際に、手動で作成する必要がなく、デフォルトでパーティションインデックスも作成される

これにより、数百万のパーティションを持つテーブルのパーティションメタデータの取得とフィルタリングに要する時間を短縮

### [2023-05-09 Glueのラージインスタンスタイプが一般公開](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/aws-glue-large-instance-types-generally-available/)

- 石川さんの記事
  - [[アップデート] AWS Glue 大規模インスタンスタイプG.4X および G.8Xが一般提供されました | DevelopersIO](https://dev.classmethod.jp/articles/20230510-aws-glue-g4x-and-g8x/)
- これまでの、--write-shuffle-files-to-s3や--write-shuffle-spills-to-s3 を有効にするワークアラウンドも今後も有効とのこと
- しかしより直接的な選択肢としてスケールアップできる選択肢ができた感じ

### [2023-05-03 [新機能] AWS Glue Visual ETL がネイティブ Amazon Redshift 機能をサポートしたので試してみました！ | DevelopersIO](https://dev.classmethod.jp/articles/aws-glue-amazon-redshift-integration-for-apache-spark/)

