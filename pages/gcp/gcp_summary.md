# Google Cloud Summary

## 公式

- Google Cloud Japanのyoutubeチャンネル
  - https://www.youtube.com/channel/UCxl3AizmA_6YC4lpeycP8kA

- DA OnAir
  - https://cloudonair.withgoogle.com/events/solution-data-analytics
  - https://cloudonair.withgoogle.com/events/solution-data-analytics/resources

- GCP用チートシート
  - https://cloud.google.com/free/docs/aws-azure-gcp-service-comparison?hl=ja

- Google Cloud Next '22
  - [Google Cloud Next '22で発表された全 123 項目 | Google Cloud 公式ブログ](https://cloud.google.com/blog/ja/topics/google-cloud-next/google-cloud-next22-wrap-up/?hl=ja)

## アーキテクチャ

- データ分析の設計パターン
  - https://cloud.google.com/architecture/reference-patterns/overview?hl=ja

- 純正の構成図ツール
  - https://dev.classmethod.jp/articles/announcing-google-cloud-architecture-diagramming-tool/

## CLIのconfig

- gcloud configで複数の設定を持って切り替える
  - https://qiita.com/sky0621/items/597d4de7ed9ba7e31f6d

- 初回設定時のコマンド
  - `gcloud init`
- 初回以降の認証
  - `gcloud auth login`
- 複数のconfig切り替え
  - `gcloud config configurations create`

### IAM

- 定義済みロールの情報を確認
  - `gcloud iam roles describe {ROLE-ID}`
- 特定のプロジェクトで定義されているロールの一覧を確認
  - `gcloud iam roles list --project={PROJECT-ID}`

### Computing Engine

- スナップショット一覧取得
  - `gcloud compute snapshots describe`
- プロジェクトIDを調べる
  - `gcloud compute project-info desribe --project {PROJECT-ID}`
- Windows Serverのイメージリストを取得
  - `gcloud compute images list --project windows-cloud --no-standard-images`
- サービスアカウントの設定
  - `gcloud compute instances set-service-account`
- スナップショットからイメージを作成
  - `gcloud compute images create {IMAGE-NAME} --source-snapshot {SNAPSHOT-NAME}`

### Google Kubernetes Engine（GKE）

- オートスケールの設定
  - `kubectl autoscale rc my-app-rc --min=2 --max=6 --cpu-percent=80`
- マニフェストファイルからクラスターをデプロイ
  - `kubectl apply -f my-app.yaml`
- クラスタ作成
  - `gcloud container clusters create with --enable-autoscaling X --min-nodes X --max-nodes X`

### Cloud SQL

- SQLクライアントでアクセスするコマンド
  - `gcloud sql connect {INSTANCE-ID} --user=root`

### Firestore

- バックアップをバックグラウンド実行
  - `gcloud datastore export gs://my-datastore-backup --async`

### Cloud Storage

- ストレージクラスを変更する
    - `gsutil rewrite -s nearline gs://free-photos-gcp`
- オブジェクトを公開する
    - `gsutil iam ch allUsers:objectViewer gs://free-photos-on-gcp`
- オブジェクトの作成時間やコンテンツタイプなどのメタデータを取得する
    - `gsutil stat gs://BUCKET_NAME/OBJECT_NAME`

### Artifact Registry

- コンテナイメージのメタデータ一覧を見る
  - `gcloud container images list`


### BigQuery

- データセットの一覧取得
  - `bq ls`
- データセットの情報表示
  - `bq show --format=prettyjson {PROJECT-NAME}:{DATASET-NAME}`
- コスト見積もり
  - `bq query --dry-run < {SQL-FILE}`
