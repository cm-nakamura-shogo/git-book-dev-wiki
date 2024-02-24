# notes-analytics

## データモデリング

- [モデリングはキラキラ技術より地味だが役に立つ / modeling-over-shiny-tech - Speaker Deck](https://speakerdeck.com/pei0804/modeling-over-shiny-tech)
  - 便利なサービスを使ったとしてもモデリングは良い感じにならない
  - ログ設計から見直す、発生タイミング事に作る
  - ファクトとディメンジョンを分ければ、ファクトをUNION ALLしてディメンジョンとJOINするだけで良いはず
    - dbt_utilsでunion_relationsができる
  - ツールを使ってもクエリがつらいならばモデリングが悪い
  - [ディメンショナル・モデリング](https://zenn.dev/pei0804/articles/dimensional-modeling)
  - [スタースキーマ(基礎)](https://zenn.dev/pei0804/articles/star-schema-design)
    - ナチュラルキーとサロゲートキーを使う
    - 第三正規化まで行わない
      - ディメンジョンの属性をID化せずに実体で保持するという意味
    - 数値イコールファクトとは限らない
      - 会員番号など
      - もっと難しい例は100円が集約された場合なファクトだが、集約するためのものである場合はディメンションとなる
    - Junkディメンションという設計パターンの紹介
      - フラグをまとめたものをディメンションテーブルとする方法
    - これらのテーブル設計は冗長だが、これに場合によっては正規化を適用するのが有効なケースもある
    - これがスノーフレークスキーマだが、正規化の原則を適用することは例外的
      - [スノーフレークスキーマ](https://zenn.dev/pei0804/articles/snowflake-schema)
    - ファクトテーブルの設計は、他のカラムから計算すれば得られる値でも計算済みのカラムを持つことで使用するツールに関係なく一貫した値を得られる
    - ファクトテーブルの粒度はできるだけ詳細にする
      - 集約すると潜在的に有用な情報を失う
      - 今のビジネス要件では詳細なデータを必要としない場合でも、要件は変化する
  - [スロー・チェンジ・ディメンション(Slowly Changing Dimensions)](https://zenn.dev/pei0804/articles/slowly-changing-dimensions)
    - ナチュラルキーとサロゲートキーがあるType2のメリットが分かりやすい
    - Type1だとディメンジョンの変更履歴が追いにくく、ファクトテーブルの過去の意味が変わってしまう
    - ディメンジョンにタイムスタンプを持たせることも必要（じゃないといつから変わったかファクトテーブルから逆引きしないといけない）
    - Type3以降はあまり一般的ではないみたい

- [2022/09/24 Data Vault 2.0 輪読会に参加しました - /home/by-natures/dev*](https://bynatures.hatenadiary.jp/entry/2022/09/24/175202)
  - Data Vaultの参考として

## さがらさんのまとめ

ディメンショナルモデリング勉強手順

- 以下の記事をざっと読み、設計と実装の流れのイメージを掴む
  - DeNA社の具体的な事例
    - [ディメンショナルモデルの実導入と実装について | ドクセル](https://www.docswell.com/slide/5LLL67/embed?mode=twitter#s1)
  - 海外の方の、dbtを用いたディメンショナルモデリングのサンプル
    - [Build a Data Warehouse with dbt using Kimball’s dimensional modeling | by Haq Nawaz | Dev Genius](https://blog.devgenius.io/build-a-data-warehouse-with-dbt-using-kimballs-dimensional-modeling-59ea9bfae59f)
  - ぺいさんによる「ディメンショナルモデリング入門」スライド
    - [ディメンショナル モデリング入門 / introduction-to-dimensional-modeling - Speaker Deck](https://speakerdeck.com/pei0804/introduction-to-dimensional-modeling)
- 以下の情報をざっと読み、ディメンショナルモデリングに関する知識を得る
  - dbt公式Docのディメンショナルモデリング解説記事
    - [Dimensional modeling: An essential concept in data modeling](https://docs.getdbt.com/terms/dimensional-modeling)
  - 石川さんの神動画
    - [データ分析を支える技術 データモデリング再入門 #devio2022 - YouTube](https://www.youtube.com/watch?v=xIHbDgVyeSI)
  - ぺいさんの記事たち
    - ディメンショナルモデリングの概要
      - [ディメンショナル・モデリング](https://zenn.dev/pei0804/articles/dimensional-modeling)
    - スタースキーマ
      - [スタースキーマ(基礎)](https://zenn.dev/pei0804/articles/star-schema-design#discuss)
    - 複数のスタースキーマの取り扱い
      - [複数スタースキーマ](https://zenn.dev/pei0804/articles/multiple-star-schema)
    - コンフォームド・ディメンション
      - [コンフォームド・ディメンション(Conformed Dimensions)](https://zenn.dev/pei0804/articles/conformed-dimensions)
    - スノーフレークスキーマ
      - [スノーフレークスキーマ](https://zenn.dev/pei0804/articles/snowflake-schema)
      - あまり使わないかも？
  - おまけ：正規化
    - 第3正規化について以前甲木さんからレクチャーいただいた時のメモ
- 実際にやってみる
  - dbtの公式ブログの実践記事　※ブログではDuckDBかPostgreSQL使っているが、Snowflakeでも出来るはず。可能ならばブログにする
    - [Building a Kimball dimensional model with dbt | dbt Developer Blog](https://docs.getdbt.com/blog/kimball-dimensional-model)
- 改めて、1と2の情報を読み、実践したあとでの知識補完をする
  - Data Modeling with Snowflakeから、使えそうなところを読む
    - [Amazon | Data Modeling with Snowflake: A practical guide to accelerating Snowflake development using universal data modeling techniques | Gershkovich, Serge, Graziano, Kent | Data Warehousing](https://www.amazon.co.jp/Data-Modeling-Snowflake-accelerating-development/dp/1837634459/)
    - Qiitaでのこの本に対する感想記事
      - [Data Modeling with Snowflakeを読んでみた #Snowflake - Qiita](https://qiita.com/aki_naka/items/5d44b596a36741e167f7)
- 参考情報
  - 大福帳とディメンショナルモデリングどっちがいいの？
    - 渋谷さんの記事
      - [Snowflakeパフォーマンスのカギはやっぱりデータモデリング](https://zenn.dev/ryotas_data/articles/34624130412e14)
  - ER図などを作成するためのツール
    - https://www.holistics.io/blog/open-source-data-modeling-tools/
    - https://www.holistics.io/blog/top-5-free-database-diagram-design-tools/
    - Dbdiagram.io、Diagrams.net あたりが良さそう？完全無料なら Diagram.net
  - 各企業の参考
    - 風音屋
      - https://techblog.kazaneya.com/20231215-access-fact-table-design/
    - タイミー
      - https://tech.timee.co.jp/entry/2023/10/23/143322
  - 本　※英語本は積む傾向があるため、優先度低め
    - The Data Warehouse Toolkit: The Definitive Guide to Dimensional Modeling
    - [Amazon | The Data Warehouse Toolkit: The Definitive Guide to Dimensional Modeling | Kimball, Ralph, Ross, Margy | Structured Design](https://www.amazon.co.jp/dp/1118530802)
      - 分かりづらいとのこと(kenさん)
    - [Amazon | Star Schema: The Complete Reference | Adamson, Christopher | Data Warehousing](https://www.amazon.co.jp/dp/0071744320)
      - 具体例があって、上のキンボールさんの本より良いとのこと(kenさん)

- [ディメンショナルモデリングに入門しよう！Snowflakeとdbt Cloudで「Building a Kimball dimensional model with dbt」をやってみた | DevelopersIO](https://dev.classmethod.jp/articles/building-a-kimball-dimensional-model-with-snowflake-and-dbt/)
  - モデリングの理解に有用か

## ぺいさんのその他

- [2024年に描く青写真(データアーキテクチャ) / strongest-data-architecture-discussion-2024 - Speaker Deck](https://speakerdeck.com/pei0804/strongest-data-architecture-discussion-2024)
- [SELECTを使った手間なしSnowflakeコスト最適化 - CARTA TECH BLOG](https://techblog.cartaholdings.co.jp/entry/select-cloud-cost-optimize-cmf)
- [Snowflakeの力を引き出すためのdbtを活用したデータ基盤開発の全貌 - CARTA TECH BLOG](https://techblog.cartaholdings.co.jp/entry/snowflake-dbt-data-platform-vision)
- [Snowflakeと共に過ごした一年間。その進化過程と未来へのVision - CARTA TECH BLOG](https://techblog.cartaholdings.co.jp/entry/snowflake-data-platform-vision)
- [dbt x snowflakeで使っていないテーブルとビューを安全に一括で削除する - CARTA TECH BLOG](https://techblog.cartaholdings.co.jp/entry/2024/01/15/113000)
- [アドテクのビッグデータを制するSnowflakeの力 / data-cloud-world-tour-tokyo-2023 - Speaker Deck](https://speakerdeck.com/pei0804/data-cloud-world-tour-tokyo-2023)

## Snowflake

- [Snowflakeパフォーマンスのカギはやっぱりデータモデリング](https://zenn.dev/ryotas_data/articles/34624130412e14)
  - 良くある誤解が書いてある
  - Snowflake特有の話もある感じ
  - 誤解1：列指向なので、ディメンションをまとめることの効果は低い
    - パーティションがあるためそんなことはない
  - 誤解2：現代のクラウドDWHは列指向なので、結合のパフォーマンスが悪い
    - 行指向でもそうですが、クエリの実行計画次第という側面が大きい
  - 誤解3：データ民主化時代において、ディメンショナルモデリングはエンドユーザの学習コストが高すぎる
    - 民主主義という名の社会主義で草
