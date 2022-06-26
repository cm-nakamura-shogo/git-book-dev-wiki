# SQL

## SQLアンチパターンまとめ

- https://qiita.com/shimamura_io/items/7ca604933f526a2cdfa9

## JOIN

- 図解
  - https://i.redd.it/dyqnzpuddxk21.png

## OVER

- SQLでデータ分析(overとか)
  - https://qiita.com/w-sato-ist/items/63600a3ab84aad38e879

## DDL,DML,DCL

- https://morizyun.github.io/database/sql-ddl-dml-dcl.html

## ONとWHEREに条件を書くことについて

- INNER JOINの時はONとWHEREどちらに記述しても同じ。
- 条件に一致しないレコードは減る。

- LEFT JOINの時は、ON条件がLEFTな性質を維持するので、違いがでる。
  - ONに記述する場合はLEFT側のテーブルのレコード数が減らない。
  - WHEREは一致しないレコードが減る。

- さもありなんという感じではある。
- 以下参考
  - [https://atsuizo.hatenadiary.jp/entry/2016/12/12/163921](https://atsuizo.hatenadiary.jp/entry/2016/12/12/163921)
  - [https://zukucode.com/2017/08/sql-join-where.html](https://zukucode.com/2017/08/sql-join-where.html)