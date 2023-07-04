# BigQuery

## 機能

### UDF: ユーザ定義関数

JSON変換など柔軟に対応できる変換がない場合は、UDFを定義して使いまわすことが可能

- [ユーザー定義の関数  |  BigQuery  |  Google Cloud](https://cloud.google.com/bigquery/docs/reference/standard-sql/user-defined-functions?hl=ja)

### ColabとBigQueryの連携

連携するには以下の方法がある。

- Colab上で`%%bigquery`のマジックコマンドを使用
- 公式ライブラリのPython Client for Google BigQueryを使用
- BigQuery結果からシームレスにColabに連携(2022-10-05プレビュー)
  - 実際は公式ライブラリを設定する際のimportが埋め込まれたnotebookが起動されるようだ
  - 参考記事
    - [Google ColaboratoryでBigQueryのクエリ結果を扱ってみる | DevelopersIO](https://dev.classmethod.jp/articles/bq_colab/)

## 参考記事

- スプレッドシートをBigQueryから分析してみた
  - https://dev.classmethod.jp/articles/google-spreadsheet-sql-from-bigquery

- BQ内部の仕組み
  - https://storage.googleapis.com/pub-tools-public-publication-data/pdf/e55a6f8822b6528ff47797936e40faedc7d047ac.pdf

## アップデート

- [2022-10-10 マルチステートメントトランザクションがGA](https://dev.classmethod.jp/articles/bigquery-mutistatement-transaction-ga/)
  - 失敗時にロールバックしてくれるため、INSERTを同期させたいものがある場合に便利。
- 2022-10-18 Remote functionsがGA
  - クエリでCloud FunctionsやCloud Runの関数を呼び出すことができる機能
- [2022-10-19 非構造化データを使用可能な機能がプレビュー提供](https://cloud.google.com/blog/products/data-analytics/how-to-manage-and-process-unstructured-data-in-bigquery?hl=en)
- [2023-02-16 BigQueryの主キー/外部キー制約はJoin Eliminationには使われない](https://qiita.com/abe_masanori/items/c19cf240fa3eaeeff44c)
  - 実際にデータのチェックが行われるわけではない
  - データのチェックが行われないのであれば主キー/外部キー制約を付与する理由は何なのかというと、一般の DBMS ではオプティマイザが実行計画を最適化する際に利用される
  - その最適化の手法の一つに不要な結合処理をスキップする Join Elimination という手法があり、そちらに利用される
- [2023-05-03 BigQueryのテーブルクローン機能がGA (Google Cloud)](https://cloud.google.com/bigquery/docs/release-notes#May_03_2023)
- [2023-05-05 BigQueryのINSERT INTO SELECTでAmazon S3およびAzure Blobからフィルタリングしてテーブルに追加することが可能に (Google Cloud)](https://cloud.google.com/bigquery/docs/release-notes#May_05_2023)
  - まだプレビュー
- [2023-05-11 オブジェクトテーブルがGAに](https://cloud.google.com/bigquery/docs/release-notes#May_11_2023)
  - BigQuery MLとBigQueryリモート関数を使用して、画像、音声ファイル、ドキュメント、その他のファイルタイプの分析および推論を実行することが可能に
  - GAリリースには、以下の新機能および更新機能が含まれています
    - ml.decode_image：ML.decode_image：画像データをデコードし、ML.PREDICT関数で解釈することができるようにします。
    - ML.CONVERT_COLOR_SPACE: RGB色空間を持つ画像を別の色空間に変換する。
    - ML.CONVERT_IMAGE_TYPE： 画像のデータ型を変換します．画像の画素値のデータ型を変換する。
    - ml.resize_image：画像のサイズを変更する。
    - ML.DISTANCE: 2つのベクトル間の距離を計算する．
    - ML.LP_NORM：Lᵖ normを計算します．
- [2023-05-18 BigQueryでカラム名の横にあるソートメニューを使って、クエリ結果をソートできるように。プレビュー機能。](https://cloud.google.com/bigquery/docs/release-notes#May_18_2023)
  - devio
    - [BigQuery でクエリ結果の並び替えができるようになりました（Preview） | DevelopersIO](https://dev.classmethod.jp/articles/bigquery-sort-query-results/)
- [2023-05-19 BigQueryでEXTERNAL_QUERY SQL pushdownが一般提供開始](https://cloud.google.com/bigquery/docs/release-notes#May_19_2023)
  - Cloud SQLやCloud Spannerデータベースなどの外部ソースからのデータ検索を最適化
  - 列の刈り込み（SELECT句）とフィルターのプッシュダウン（WHERE句）によりり少ないデータを転送することで、実行時間とコストを削減
  - すべてのデータ型がフィルタープッシュダウンに対応していないとのこと
- [2023-05-25 BigQueryのパーティショニングとクラスタリングのレコメンダーがプレビュー](https://cloud.google.com/bigquery/docs/release-notes#May_25_2023)
  - レコメンダーはBigQueryのテーブルを分析し、コスト削減の可能性があるパーティショニングやクラスタリングの機会を特定
  - レコメンド結果を直接テーブルに適用も可能
- [2023-06-12 クエリ実行グラフの一般提供（GA）を開始](https://cloud.google.com/bigquery/docs/release-notes#June_12_2023)
  - クエリ実行グラフは、クエリパフォーマンスの問題を診断したり、クエリパフォーマンスのインサイトを受け取るために使用することができます。
- [2023-06-15 BigQueryでもML.GENERATE_TEXTによりLLMのtext-bisonが使える機能がプレビュー](https://cloud.google.com/bigquery/docs/release-notes#June_15_2023)
- [2023-06-20 BigQueryのメタデータのキャッシュが一般的に利用可能に](https://cloud.google.com/bigquery/docs/release-notes#June_20_2023)
  - BigLakeテーブルや大量のオブジェクトを参照するオブジェクト・テーブルのクエリ・パフォーマンスが向上する
- [2023-06-20 BigQueryが、オープンソースエンジンで作成されたApache Icebergテーブルのクエリをサポートするように](https://cloud.google.com/bigquery/docs/release-notes#June_20_2023)
- [2023-06-21 TRUNCATE TABLEが複数ステートメント・トランザクションでサポートされるように](https://cloud.google.com/bigquery/docs/release-notes#June_21_2023)
  - [【BigQuery アップデート情報】トランザクション内でのTRUNCATE TABLEがGAになりました | DevelopersIO](https://dev.classmethod.jp/articles/truncate-table/)
- [2023-06-26 JavaまたはScalaを使用してApache Spark用のストアドプロシージャを作成できるように](https://cloud.google.com/bigquery/docs/release-notes#June_26_2023)
- [2023-06-30 Amazon S3データを参照するBigLakeテーブルでメタデータキャッシングが利用可能に(プレビュー)](https://cloud.google.com/bigquery/docs/release-notes#June_30_2023)