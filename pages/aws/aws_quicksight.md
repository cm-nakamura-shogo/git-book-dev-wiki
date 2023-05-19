# Amazon QuickSight

BIツール。

## ダイレクトクエリモード

Athenaなどに接続できる。
クエリ自体に変数を埋め込むことはできないが、WHEREなしでクエリを記述し分析側でフィルターすることで、動的なクエリを実現することも可能。

## UTCしか使えない

QuickSightに送信したデータは、JSTで送信してもUTCとしてしか表示できない。

そのため、送信前に9時間加算するか、表示側で9時間加算する。（おそらく見る側の都合なので、後者の方が後々分かりやすい）

- 参考記事
  - [【小ネタ】Amazon QuickSight でデータのタイムゾーンを変更できないか試してみた | DevelopersIO](https://dev.classmethod.jp/articles/change-timezone-on-quicksight/)


## Adminの切り替わりもUTC基準

月末締めで管理ユーザを変更した場合を以下で検証されている。
JSTの9時にユーザが想定通りになるが、一時的にユーザが増えている期間が存在するようになるらしい

- 参考記事
  - [QuickSight の管理者ユーザーをたくさんつくってしまったので月が変わったタイミングで整理されるか検証してみた | DevelopersIO](https://dev.classmethod.jp/articles/quicksight-admin-takusan-tukutta/)

## 参考記事

### [2022-01-30 分析を、テンプレート機能を使って別アカウントへ配布](https://dev.classmethod.jp/articles/quicksight-analysis-template/)

- 本日時点でCloudFormationやAWS CLIでQuickSightの分析をイチから作成することはできない
- その代わりに、QuickSightにはコンソール上で作成した分析をテンプレート化して配布する機能が備わっている

## アップデート

### [2023-04-13 QuickSight で API でデータセット更新スケジュールを管理出来るようになった](https://dev.classmethod.jp/articles/quicksight-api-refresh-schedule/)

- データセット（SPICE） のデータ更新をスケジュール設定がAPIから可能に
- CloudFormationでもサポートされた（4/15追記）
- 従来は取り込み部分を EventBridge や Lambda で別途スケジューリングする必要があった

### [2023-05-15 QuickSight、SPICEパフォーマンス最適化のための「Common Sub-expression Elimination」の提供を開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-quicksight-common-sub-expression-elimination/)

- CSEは、複雑な式の繰り返し使用を中間テーブルに押し込んで、合計/小計、トップ・ボトム・フィルター、条件付き書式、チャートの「その他」バケットなど、複雑なクエリを簡素化
- ダッシュボードの読み込みが速くなり、ユーザ体験の向上が可能