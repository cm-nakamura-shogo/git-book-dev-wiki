# データベース設計

## indexとは何か

- indexのメリット・デメリット
  - メリット：データの読み込み・取得が早くなる。
  - デメリット：書き込みの速度が倍かかる。

- indexがあると、検索が速くなる。
- その分、書き込むときは遅くなる。

- 参考
  - https://qiita.com/seiya1121/items/fb074d727c6f40a55f22

## ユーザー更新に競合がある場合、どのように扱うか

- ユーザビリティを考えれば、先勝ちが基本
  - https://www.codegrid.net/articles/2014-web-app-patterns-1/

- 先勝ちを実現するには、最新の更新日時を保持しておく必要がある。

## マルチテナント設計

* [マルチテナント化で知っておきたいデータベースのこと | slideshare](https://classmethod.slack.com/archives/D030NQQEAKY/p1654298980899179)

## データレイクとは

- [Snowflakeプラットフォームが支える６ワークロード(5) データレイクの過去と現在、そして未来 (1) | TECH+](https://news.mynavi.jp/techplus/kikaku/snowflake-workload-5/)
  - 甲木先生の解説
