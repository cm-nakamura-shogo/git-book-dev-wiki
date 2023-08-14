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

## Articles

- スプレッドシートをBigQueryから分析してみた
  - https://dev.classmethod.jp/articles/google-spreadsheet-sql-from-bigquery

- BQ内部の仕組み
  - https://storage.googleapis.com/pub-tools-public-publication-data/pdf/e55a6f8822b6528ff47797936e40faedc7d047ac.pdf

- [2023-07-07 BigQuery の正規表現関数の使いどころを自分なりに整理してみた | DevelopersIO](https://dev.classmethod.jp/articles/bigquery-regexp-usage/)
- [2023-07-22 BigQueryでJSONLのデータを読み込む外部テーブルを作ってみた | DevelopersIO](https://dev.classmethod.jp/articles/create-bigquery-jsonl-external-table/)

## Updates

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
- [2023-07-05 BigQueryアップデート](https://cloud.google.com/release-notes#July_11_2023)
  - GA : LOAD DATA SQLステートメントを使用して、Avro、CSV、改行区切りJSON、JSON、ORC、またはParquetファイルからテーブルにデータをロードする機能。
  - Preview : スロット・エスティメータが、エディション価格と過去のパフォーマンス・メトリクスに基づいて、コスト最適なコミットメントとオートスケールの推奨を提供するように。
  - GA : フェイルセーフ期間が一般的に利用可能に。フェイルセーフ期間では、タイムトラベルウィンドウの後にさらに7日間のデータストレージが提供。
  - GA : ストレージの課金に物理バイトを使用する機能がGA。データセットのストレージ課金モデルを物理バイトを使用するように設定すると、課金されるアクティブ・ストレージ・コストの合計には、タイムトラベルおよびフェイルセーフ・ストレージに使用されるバイトが含まれます。
  - GA : タイムトラベルウィンドウを構成する機能が一般的に利用可能になりました（GA）。タイムトラベルウィンドウの期間は、最小2日から最大7日まで指定できます。
  - BigQueryの容量コミットメントが以下のように変更
    - 年間コミットメントはEnterpriseまたはEnterprise Plusエディションでのみ利用可能になりました。定額制の年間コミットメントは利用できなくなりました。
    - 月額コミットメントおよびフレックスコミットメントは利用できなくなりました。
  - Preview : Analytics Hubのリストでデータの送信を制限できるように
- [2023-07-06 BigQueryアップデート](https://cloud.google.com/release-notes#July_06_2023)
  - GA : Spanner Data Boostは、プロビジョニングされたSpannerインスタンス上の既存のワークロードにほとんど影響を与えることなく、分析クエリやデータエクスポートを実行することができます。
- [2023-07-12 BigQueryアップデート](https://cloud.google.com/release-notes#July_12_2023)
  - BigQuery MLフィーチャー前処理機能が一般公開
    - TRANSFORM句を使用するモデルをTensorFlow SavedModel形式にエクスポート
    - TRANSFORM句で学習したモデルをVertex AIやローカルに配置することもできるように
  - 時系列予測のためのカスタムホリデーモデリングがプレビューに
- [2023-07-17 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#July_17_2023)
  - [【アップデート情報】 BigQueryで主キーと外部キーが正式にサポートされるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/bigquery-primary-foreign-key/)
- [2023-07-19 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#July_19_2023)
  - BigQueryは検索インデックスを使用して、等置演算子（=）、IN演算子、LIKE演算子、またはSTARTS_WITH関数を含む一部のクエリを最適化し、インデックス付きデータと文字列リテラルを比較できるように
- [2023-07-20 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#July_19_2023)
  - BigQuery MLでARIMA_PLUS_XREGモデルによる多変量時系列予測が一般に利用可能に
    - この機能を使用すると、追加の特徴列を使用して時系列予測を実行できます
  - BigQuery MLは、モデルの説明可能性を高める新しいExplainable AI機能を導入
    - ML.EXPLAIN_FORECAST関数をARIMA_PLUS_XREGモデルで使用できるようになりました。
    - 更新されたML.EXPLAIN_FORECAST関数を使用して、時系列予測モデル（ARIMA_PLUSとARIMA_PLUS_XREGの両方）の休日に対する休日効果の説明を得ることができます。
    - ML.GLOBAL_EXPLAIN関数をAutoML Tablesモデルで使用して、グローバルなモデルの説明可能性を得ることができるようになりました。
    - Boosted Tree モデルと Random Forest モデルで、approx_global_feature_contrib オプションと approx_feature_contrib オプションが使用可能に
      - approx_global_feature_contrib : モデル学習で大域的な特徴寄与計算に高速近似を使用する
      - approx_feature_contrib : モデル推論で局所的な特徴寄与計算に高速近似を使用する
  - 公式ブログ
    - [Customized holiday modeling with BigQuery ML forecasting | Google Cloud Blog](https://cloud.google.com/blog/products/data-analytics/customized-holiday-modeling-with-bigquery-ml-forecasting/?hl=en)
- [2023-07-28 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#July_28_2023)
  - クエリキューが一般的に利用可能に
  - クエリキューでは、BigQueryは利用可能なスロットに基づいてクエリの同時実行数を自動的に決定
  - 最大同時実行数に達すると、処理リソースが利用可能になるまで追加のクエリがキューに入れられる
  - クエリキューはデフォルトで有効化されており、ここ数週間でロールアウトされる
  - オプションで、予約の最大同時実行数を設定することが可能
- [2023-07-31 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#July_31_2023)
  - BigQuery Storage Write APIの多重化が一般公開（GA）されました。
  - デフォルトのストリームで多重化を使用して、共有接続で複数の宛先テーブルに書き込むことができます。
- [2023-08-03 BigQueryアップデート](https://cloud.google.com/bigquery/docs/release-notes#August_03_2023)
  - Analytics Hubを使用すると、共有データセットの使用状況メトリクスを追跡できるようになりました。この機能は一般に利用可能です（GA）。
  - 使用状況メトリクスには次のようなものがあります：
    - 共有データセットに対して実行されたジョブ
    - サブスクライバーのプロジェクトや組織による共有データセットの消費詳細。
    - ジョブが処理した行数とバイト数。
  - クラウドコンソールの更新以下の機能がプレビューで利用可能になりました：
    - [ようこそ] ページの [最近アクセスしたリソース] セクションで、最近アクセスした 10 個のリソースを表示できます。
    - クエリエディタでクエリを実行した後、[Chart] タブでクエリ結果を視覚化できます。
  - SQL 文でマテリアライズド・ビューへのアクセスを GRANT または REVOKE できるようになりました。この機能は一般に利用可能です（GA）。
- [2023-08-04 BigQueryアップデート](https://cloud.google.com/release-notes#August_04_2023)
  - BigQueryが外部テーブルのマニフェストファイルの使用をサポートするようになりました。この機能は一般公開（GA）されました。
- [2023-08-07 BigQueryアップデート](https://cloud.google.com/release-notes#August_07_2023)
  - quantitive LIKE演算子のプレビューが開始。この演算子を使うと、検索値が複数のパターンにマッチするかどうかを、これらの条件のいずれかを使ってチェックすることができます
  - いくつかのJSON関数が一般公開（GA）
  - BigQueryは、IAMパーミッションの拒否ポリシーを使用してプリンシパルへのアクセスを拒否する機能をサポートするように
- [2023-08-08 BigQueryアップデート](https://cloud.google.com/release-notes#August_08_2023)
  - クエリおよびマテリアライズド・ビューで、以下の機能が一般に利用可能になりました（GA）：
    - ANY_VALUE 関数の HAVING MAX 節と HAVING MIN 節。
    - ANY_VALUE(x HAVING MAX y)の同義語であるMAX_BY関数。
    - MIN_BY関数。ANY_VALUE(x HAVING MIN y)の同義語
- [2023-08-10 BigQueryアップデート](https://cloud.google.com/release-notes#August_10_2023)
  - カーディナリティの高い結合に関するクエリ・パフォーマンスのインサイトが表示されるようになりました。この機能は一般公開（GA）されています。
  - ユーザー定義関数を使用して、BigQueryデータをプロトコルバッファ（Protobuf）列としてエクスポートできるようになりました。この機能は一般的に利用可能です