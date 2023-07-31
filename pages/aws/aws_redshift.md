# Amazon Redshift

## Lambda UDF

RedshiftではLambdaで定義された関数をSQLクエリの一部として使用できる。

## Updates

- [2023-03-10 Serverless の最小ベースキャパシティが32RPUから8RPUに削減](https://dev.classmethod.jp/articles/20230310-amazon-redshift-rpu-8/)
- [2023-07-17 [アップデート]Amazon RedshiftでQUALIFY句がサポートされ、WINDOW関数を使った結果のフィルタが可能になりました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-redshift-supports-qualify-calify-clause/)
  - QUALIFY句は、WINDOW関数を使った結果をフィルタリングするSQLステートメント
  - HAVING句はSUMなどの集計関数とGROUP BY句の結果をフィルタする一方、QUALIFY句では分析によく使われるRANKなどのWINDOW関数の結果をフィルタするという違いがある
- [2023-07-20 Amazon Redshift MLがAmazon Forecastとの統合を発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-redshift-ml-integration-amazon-forecast/)
- [2023-07-25 Amazon Redshiftは、AWS Glue Data Catalogの自動マウントの一般提供を発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-redshift-automatic-mounting-aws-glue-data-catalog/?nc1=h_ls)
  - [[アップデート]RedshiftがGlue Data Catalogを自動マウントするようになったので、Redshift Serverlessでクエリを試してみました | DevelopersIO](https://dev.classmethod.jp/articles/query-glue-data-catalog-from-redshift-serverless/)