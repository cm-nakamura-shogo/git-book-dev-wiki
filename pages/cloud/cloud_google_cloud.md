# GCP

## 公式

- Google Cloud Japanのyoutubeチャンネル
  - https://www.youtube.com/channel/UCxl3AizmA_6YC4lpeycP8kA

- DA OnAir
  - https://cloudonair.withgoogle.com/events/solution-data-analytics
  - https://cloudonair.withgoogle.com/events/solution-data-analytics/resources

- GCP用チートシート
  - https://cloud.google.com/free/docs/aws-azure-gcp-service-comparison?hl=ja

## アーキテクチャ

- データ分析の設計パターン
  - https://cloud.google.com/architecture/reference-patterns/overview?hl=ja

- 純正の構成図ツール
  - https://dev.classmethod.jp/articles/announcing-google-cloud-architecture-diagramming-tool/

## config

- gcloud configで複数の設定を持って切り替える
  - https://qiita.com/sky0621/items/597d4de7ed9ba7e31f6d

## BigQuery

- スプレッドシートをBigQueryから分析してみた
  - https://dev.classmethod.jp/articles/google-spreadsheet-sql-from-bigquery

- BQ内部の仕組み
  - https://storage.googleapis.com/pub-tools-public-publication-data/pdf/e55a6f8822b6528ff47797936e40faedc7d047ac.pdf

- Remote functionsがGA(2022-10-18)
  - クエリでCloud FunctionsやCloud Runの関数を呼び出すことができる機能

- 非構造化データを使用可能な機能がプレビュー提供(2022-10-19)
  - https://cloud.google.com/blog/products/data-analytics/how-to-manage-and-process-unstructured-data-in-bigquery?hl=en

- マルチステートメントトランザクションがGA(2022-10-10)
  - https://dev.classmethod.jp/articles/bigquery-mutistatement-transaction-ga/
  - 失敗時にロールバックしてくれるため、INSERTを同期させたいものがある場合に便利。

### ColabとBigQueryの連携

連携するには以下の方法がある。

- Colab上で`%%bigquery`のマジックコマンドを使用
- 公式ライブラリのPython Client for Google BigQueryを使用
- BigQuery結果からシームレスにColabに連携(2022-10-05プレビュー)
  - 実際は公式ライブラリを設定する際のimportが埋め込まれたnotebookが起動されるようだ
  - 参考記事
    - [Google ColaboratoryでBigQueryのクエリ結果を扱ってみる | DevelopersIO](https://dev.classmethod.jp/articles/bq_colab/)


## Vertex AI

- kubeflowベース。
- kubeflowやk8sに慣れ親しんでおいた方がよい。

- Vertex AIのラーニングパス
  - https://cloud.google.com/blog/ja/topics/developers-practitioners/new-ml-learning-path-vertex-ai

- メルカリ活用例
  - https://engineering.mercari.com/blog/entry/20220224-similar-search-using-matching-engine/

## Google Cloud Next '22

- まとめ
  - [Google Cloud Next '22で発表された全 123 項目 | Google Cloud 公式ブログ](https://cloud.google.com/blog/ja/topics/google-cloud-next/google-cloud-next22-wrap-up/?hl=ja)

## Cloud Data Fusion

- データパイプラインの構築と管理を行うための統合環境
- GUI上で完結して手軽にデータパイプランを作成することが可能
- 使用するにはインスタンスの作成が必要で、パイプラインの実行には、Dataprocクラスタを使用する。
  - ETL処理はDataprocにより実施
    - [https://zenn.dev/hssh2_bin/articles/a464ce7f498024](https://zenn.dev/hssh2_bin/articles/a464ce7f498024)
- GUIではノードを接続してパイプラインを構成する。
- 例として以下のようなノードがある。
  - GCS
  - HTTP ... あるAPIのURLにアクセスしデータを取得する。
  - CSVParser
  - Wrangler ... 文字コード変換など実施可能。(BigQueryは基本的にUTF-8にしか対応していないため。フラットデータのみISO-8859-1に対応)
  - BigQuery

- 参考記事
  - [Cloud Data Fusion の HTTPプラグイン を使って BigQuery にデータを投入してみた | DevelopersIO](https://dev.classmethod.jp/articles/cloud-data-fusion_http-to-bigquery)
  - [Cloud Data Fusion の Wrangler を使って文字コード変換してみた | DevelopersIO](https://dev.classmethod.jp/articles/cloud-data-fusion_set-charset/)
