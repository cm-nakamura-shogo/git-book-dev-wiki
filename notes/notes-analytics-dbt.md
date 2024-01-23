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
- [dbt Guide | The GitLab Handbook](https://handbook.gitlab.com/handbook/business-technology/data-team/platform/dbt-guide/)
  - GitLabのガイド
