# Amazon Athena

S3のデータに対してSQLクエリできる。
課金体系は、スキャン量課金で、1TB毎に5ドル程度（BigQueryやRedshift Spectrumも同程度の額）。

## コスト最適化

主に２パターンある。

- データを列指向のparquet型などで持つ
- パーティション分割により、データのスキャン量を削減

## パーティション分割

- Hiveパーティションの場合
  - `MSCK REPAIR TABLE`でパーティションを認識させられる
    - この場合、GlueのData Catalogでパーティション状況がわかる。
  - Athenaからのパーティション射影により、DDLでパーティション認識させることができる
    - この場合、GlueのData Catalogでパーティション状況が見えなくなり、テーブルのスキーマ定義などだけが記録される。

後者の場合が設定は楽だが、他サービスはこのパーティション射影に対応してない場合があり、その場合は`MSCK REPAIR TABLE`を使う方が良い可能性がある。
他、メリットデメリットについては参考URLを参照。

参考

- [[新機能]Amazon Athena ルールベースでパーティションプルーニングを自動化する Partition Projection の徹底解説 | DevelopersIO](https://dev.classmethod.jp/articles/20200627-amazon-athena-partition-projection/)
- [Amazon Athena Partition Projectionを用いたHiveパーティションのパーティションプルーニングの自動化 | DevelopersIO](https://dev.classmethod.jp/articles/20200727-amazon-athena-partition-projection-for-hive-partition/)

## カラム更新時のPARTITION再設定

カラムを変更(float->double)などに変更した場合、作成済みのPARTITIONについては再度作成が必要となる。
(データをINSERT INTOなどで挿入しようとすると、エラーとなる。)

エラーとなったパーティションについてGlueで型の定義を確認することが可能。

以下のクエリでエラーとなったパーティションを再作成して上書きすることも可能。

```sql
ALTER TABLE default.device_table ADD
PARTITION (year = '2022', month = '10', day = '25')
```

ただしAthenaの場合、通常は一回DROPするか、MSCK REPAIR TALBEする方が良いと考えられる。

なおパーティション射影の場合は、これは発生しない？と思われる。

参考記事

- [Amazon Athenaでクエリ実行時に「The column ‘<column>‘ in table ‘<table>‘ is declared as type ‘double’, but partition ‘Optional[year=<year>/month=<month>/day=<date>]’ declared column ‘<column>‘ as type ‘float’.」というエラーが発生する場合の対処 | DevelopersIO](https://dev.classmethod.jp/articles/when-running-a-query-on-amazon-athena-the-column-columnin-tabletable-is-appearing-as-type-double-but-partition-optional-year-yearmonth-monthday-dat-scheduled-column-column-what-to-do-when-the-as-typ/)

## PartitioningとBucketing

- Partitioning
  - スキャンする対象を限定する
- Bucketing
  - 大きいファイルの処理を水平分散する

参考

- [Amazon Athena で CTAS クエリのファイルの数またはサイズを設定する](https://aws.amazon.com/jp/premiumsupport/knowledge-center/set-file-number-size-ctas-athena/)
- [Amazon Athena のPartitioningとBucketingによるパフォーマンス戦略 | DevelopersIO](https://dev.classmethod.jp/articles/amazon-athena-partitioning-vs-bucketing/)

## struct型でJSONデータをパース

- データが少ない場合、存在しないものがnullとなる。
- データが多すぎる場合でも値は取得できる。

参考

- [Athenaのstruct型でオブジェクトの要素が増減したときの読み込みの様子を調べた | DevelopersIO](https://dev.classmethod.jp/articles/athena_struct_json_element_changes/)

## external_location

AthenaのCTASはexternal_locationで結果の保存先を変更できる

- [https://docs.aws.amazon.com/ja_jp/athena/latest/ug/considerations-ctas.html](https://docs.aws.amazon.com/ja_jp/athena/latest/ug/considerations-ctas.html)


## Articles

- [2018-05-22 S3にフラットに配置してしまったログも大丈夫！シンボリックリンクを利用してスキャン範囲を絞ってAthenaからクエリする | DevelopersIO](https://dev.classmethod.jp/articles/create-athena-table-with-symboliclink/)
  - Apache Hive互換のマニフェストファイル(symlink.txt)を作る方法
  - これはすごい
- [2019-12-09 AWS Athena で CREATE TABLE する](https://qiita.com/yoshiyama_hana/items/3d532c7ecc5f08c0d040)
  - わりと各パラメータの詳しい説明がある
- [2021-02-08 【全リージョン対応】CloudTrailのログをAthenaのPartition Projectionなテーブルで作る](https://dev.classmethod.jp/articles/cloudtrail-athena-partition-projection-table/)
  - CloudTrailログでPartitionどうしたらええかのヒントにもなる
- [2021-04-22 S3アクセスログをAthenaで分析](https://qiita.com/hamingcode/items/6f44bfbc8c54d974ae43)
  - プロダクトにS3使うときは合った方がいい？（ログまででいいかもだが分析することがあれば）
- [2023-07-20 「Amazon Athena for Apache Sparkを使ってデータ分析をしよう！」というタイトルで DevelopersIO 2023 に登壇しました！ #devio2023 | DevelopersIO](https://dev.classmethod.jp/articles/devio2023-osaka-data-analytics-with-amazon-athena-for-apache-spark/)
  - サクッとデータレイクから大規模分析際に良い
  - ジョブ化するにはGlueを使う様子

## Updates

- [2023-04-28 AthenaがProvisioned Capacityを発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-athena-provisioned-capacity/)
  - 固定価格で長期的なコミットメントなしに、完全に管理されたコンピュート容量でSQLクエリを実行できるようにする
  - ミッションクリティカルなクエリに専用コンピートを割り当て、クエリの同時実行数やコストなどのワークロード性能特性を制御することが可能
  - 容量はいつでも追加可能で、指定した容量とアカウントで有効な時間に対してのみ支払いが発生
  - 石川さんのブログが出ている
    - [Amazon Athena キャパシティ予約ができるProvisioned Capacityについて徹底解説！ | DevelopersIO](https://dev.classmethod.jp/articles/20230429-amazon-athena-provisioned-capacity/)
    - 1つのDPUは、4つのvCPUと16GB RAMに相当
    - プロビジョニングできる最小キャパシティは、24DPU、8時間
    - 最小でも82.56USDの料金が発生してしまう
    - Provisioned Capacityが最も適しているユースケースは、Athenaに毎月100ドル以上利用する場合
    - RI（Reserved Instance）に例えるなら、8時間以上の前払いなしのRIを動的に購入して適用するのに近い
- [2023-05-09 AthenaがApache Hudi 0.12.2をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-athena-apache-hudi/)
  - Hudi 0.12.2のテーブルをAthenaでクエリすることが可能に
  - Hudiは、Amazon EMR、Apache Spark、Apache Hiveまたはその他の互換性のあるサービスを介して管理されるデータ管理フレームワーク
- [2022-11-09 Amazon AthenaでQuery Result Reuse（クエリ結果の再利用）が使えるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/query-result-reuse-is-now-available-on-amazon-athena/)