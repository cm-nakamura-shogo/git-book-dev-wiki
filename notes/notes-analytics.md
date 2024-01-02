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

## dbt

- [Snowflakeの力を引き出すためのdbtを活用したデータ基盤開発の全貌 - CARTA TECH BLOG](https://techblog.cartaholdings.co.jp/entry/snowflake-dbt-data-platform-vision)
  - codegen、dbt_project_evaluatorなどは気になる
  - SQLFluffではなくsqlfmtを採用
  - yamlfixもあると便利だな
  - 新しく追加されたデータを全量ではなく一部でテストするようなマクロを作成している点も面白い
  - CI環境のデータベースはコミット単位でスキーマを作成している
  - dev環境では開発者別にデータベースを定義している点も面白い
    - 開発環境では、個々の開発者が~/.dbt/profiles.ymlを使用してプロファイルを管理しています。
    - 一方、CIおよび本番環境では、リポジトリ内のdbt/profile/profiles.ymlを用いてプロファイルが設定されています
- [広告レポーティング基盤に、dbtを導入したら別物になった話 / tokyo-dbt-meetup-4 - Speaker Deck](https://speakerdeck.com/pei0804/tokyo-dbt-meetup-4)
  - テーブルマイグレーションをdbtに任せる
  - append_new_columnsはちょっときになる
- [dbtでカラムレベルのリネージを表示してくれるVSC拡張機能「Turntable」](https://zenn.dev/datum_studio/articles/992becef3a8f35)
  - これは気になる