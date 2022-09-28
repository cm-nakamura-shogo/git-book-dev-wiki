# サービス説明

## CLIのconfig

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
