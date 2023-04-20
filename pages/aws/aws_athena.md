# Amazon Athena

S3のデータに対してSQLクエリできる。
課金体系は、スキャン量課金で、1TB毎に5ドル程度（BigQueryやRedshift Spectrumも同程度の額）。

## コスト最適化

主に２パターンある。
* データを列指向のparquet型などで持つ
* パーティション分割により、データのスキャン量を削減

## パーティション分割

* Hiveパーティションの場合
  * `MSCK REPAIR TABLE`でパーティションを認識させられる
    * この場合、GlueのData Catalogでパーティション状況がわかる。
  * Athenaからのパーティション射影により、DDLでパーティション認識させることができる
    * この場合、GlueのData Catalogでパーティション状況が見えなくなり、テーブルのスキーマ定義などだけが記録される。

後者の場合が設定は楽だが、他サービスはこのパーティション射影に対応してない場合があり、その場合は`MSCK REPAIR TABLE`を使う方が良い可能性がある。
他、メリットデメリットについては参考URLを参照。

* 参考
  * [[新機能]Amazon Athena ルールベースでパーティションプルーニングを自動化する Partition Projection の徹底解説 | DevelopersIO](https://dev.classmethod.jp/articles/20200627-amazon-athena-partition-projection/)
  * [Amazon Athena Partition Projectionを用いたHiveパーティションのパーティションプルーニングの自動化 | DevelopersIO](https://dev.classmethod.jp/articles/20200727-amazon-athena-partition-projection-for-hive-partition/)

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

- 参考記事
  - [Amazon Athenaでクエリ実行時に「The column ‘<column>‘ in table ‘<table>‘ is declared as type ‘double’, but partition ‘Optional[year=<year>/month=<month>/day=<date>]’ declared column ‘<column>‘ as type ‘float’.」というエラーが発生する場合の対処 | DevelopersIO](https://dev.classmethod.jp/articles/when-running-a-query-on-amazon-athena-the-column-columnin-tabletable-is-appearing-as-type-double-but-partition-optional-year-yearmonth-monthday-dat-scheduled-column-column-what-to-do-when-the-as-typ/)




## PartitioningとBucketing

* Partitioning
  * スキャンする対象を限定する
* Bucketing
  * 大きいファイルの処理を水平分散する

* 参考
  * [Amazon Athena で CTAS クエリのファイルの数またはサイズを設定する](https://aws.amazon.com/jp/premiumsupport/knowledge-center/set-file-number-size-ctas-athena/)
  * [Amazon Athena のPartitioningとBucketingによるパフォーマンス戦略 | DevelopersIO](https://dev.classmethod.jp/articles/amazon-athena-partitioning-vs-bucketing/)

## struct型でJSONデータをパース

* データが少ない場合、存在しないものがnullとなる。
* データが多すぎる場合でも値は取得できる。

* 参考
  * [Athenaのstruct型でオブジェクトの要素が増減したときの読み込みの様子を調べた | DevelopersIO](https://dev.classmethod.jp/articles/athena_struct_json_element_changes/)

## external_location

AthenaのCTASはexternal_locationで結果の保存先を変更できる

- [https://docs.aws.amazon.com/ja_jp/athena/latest/ug/considerations-ctas.html](https://docs.aws.amazon.com/ja_jp/athena/latest/ug/considerations-ctas.html)

## 参考記事

### [2019-12-09 AWS Athena で CREATE TABLE する](https://qiita.com/yoshiyama_hana/items/3d532c7ecc5f08c0d040)

- わりと各パラメータの詳しい説明がある

### [2021-02-08 【全リージョン対応】CloudTrailのログをAthenaのPartition Projectionなテーブルで作る](https://dev.classmethod.jp/articles/cloudtrail-athena-partition-projection-table/)

- CloudTrailログでPartitionどうしたらええかのヒントにもなる

### [2021-04-22 S3アクセスログをAthenaで分析](https://qiita.com/hamingcode/items/6f44bfbc8c54d974ae43)

- プロダクトにS3使うときは合った方がいい？（ログまででいいかもだが分析することがあれば）
