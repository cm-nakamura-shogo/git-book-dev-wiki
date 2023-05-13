# Cloud Data Fusion

## 機能

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