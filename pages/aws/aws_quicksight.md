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
