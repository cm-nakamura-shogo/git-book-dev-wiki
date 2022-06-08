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

## PartitioningとBucketing

* Partitioning
  * スキャンする対象を限定する
* Bucketing
  * 大きいファイルの処理を水平分散する

* 参考
  * [Amazon Athena で CTAS クエリのファイルの数またはサイズを設定する](https://aws.amazon.com/jp/premiumsupport/knowledge-center/set-file-number-size-ctas-athena/)
  * [Amazon Athena のPartitioningとBucketingによるパフォーマンス戦略 | DevelopersIO](https://dev.classmethod.jp/articles/amazon-athena-partitioning-vs-bucketing/)

## 参考

* [[新機能]Amazon Athena ルールベースでパーティションプルーニングを自動化する Partition Projection の徹底解説 | DevelopersIO](https://dev.classmethod.jp/articles/20200627-amazon-athena-partition-projection/)
* [Amazon Athena Partition Projectionを用いたHiveパーティションのパーティションプルーニングの自動化 | DevelopersIO](https://dev.classmethod.jp/articles/20200727-amazon-athena-partition-projection-for-hive-partition/)