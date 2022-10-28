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