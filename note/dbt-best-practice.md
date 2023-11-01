べスプラをざっと読んだメモ

## [How we structure our dbt projects](https://docs.getdbt.com/guides/best-practices/how-we-structure/1-guide-overview)

- models配下は３構造
  - staging
  - intermediate
  - mart

```
jaffle_shop
├── README.md
├── analyses
├── seeds
│   └── employees.csv
├── dbt_project.yml
├── macros
│   └── cents_to_dollars.sql
├── models
│   ├── intermediate
│   │   └── finance
│   │       ├── _int_finance__models.yml
│   │       └── int_payments_pivoted_to_orders.sql
│   ├── marts
│   │   ├── finance
│   │   │   ├── _finance__models.yml
│   │   │   ├── orders.sql
│   │   │   └── payments.sql
│   │   └── marketing
│   │       ├── _marketing__models.yml
│   │       └── customers.sql
│   ├── staging
│   │   ├── jaffle_shop
│   │   │   ├── _jaffle_shop__docs.md
│   │   │   ├── _jaffle_shop__models.yml
│   │   │   ├── _jaffle_shop__sources.yml
│   │   │   ├── base
│   │   │   │   ├── base_jaffle_shop__customers.sql
│   │   │   │   └── base_jaffle_shop__deleted_customers.sql
│   │   │   ├── stg_jaffle_shop__customers.sql
│   │   │   └── stg_jaffle_shop__orders.sql
│   │   └── stripe
│   │       ├── _stripe__models.yml
│   │       ├── _stripe__sources.yml
│   │       └── stg_stripe__payments.sql
│   └── utilities
│       └── all_dates.sql
├── packages.yml
├── snapshots
└── tests
    └── assert_positive_value_for_total_amount.sql
```

## [Staging: Preparing our atomic building blocks](https://docs.getdbt.com/guides/best-practices/how-we-structure/2-staging)

- stagingでやること
  - リネーム、キャスト、単位変換、カテゴリエンコード
- stagingでやらないこと
  - join、aggregate
- sqlファイルの命名規則
  - `stg_{source_name}__{table_name}.sql`
- Materializedの設定はviewにする
  - 新鮮なデータを取得し、それを使って実体化したいので
  - データコンシューマからクエリされることを意図しておらず、従ってそれほど迅速かつ効率的に実行する必要のないモデルでウェアハウス内のスペースを無駄にすることを避けることができます（？）
    - まあ基本軽いし実行時にやればええやろ的に理解
- ステージングモデルはソースマクロを使用する唯一の場所とする
- ステージングモデルはソーステーブルと1対1の関係を持つ
- 下流はこのステージングを参照する
- クリーンでDRYなステージングレイヤーを維持するために、joinすることもありうる。
  - その場合はstagingにサブディレクトリを掘る
- 結構同じ記法が登場するので、自動生成するツールもある
  - [https://github.com/dbt-labs/dbt-codegen](https://github.com/dbt-labs/dbt-codegen)
  - [https://hub.getdbt.com/dbt-labs/codegen/latest/](https://hub.getdbt.com/dbt-labs/codegen/latest/)
- Utilitiesフォルダ
  - これはステージングフォルダにはありませんが、基本的な構成要素の一部として考えておくと便利です
  - models/utilitiesディレクトリは、マクロから生成された汎用モデルや、シードに基づいて生成された汎用モデルを保存する場所です
  - 最も一般的な使用例は、dbt utilsパッケージで生成された日付の背骨です。
  - あまりよく分からなかった

## [Intermediate: Purpose-built transformation steps](https://docs.getdbt.com/guides/best-practices/how-we-structure/3-intermediate)

- ビジネス上の関心領域ごとにサブディレクトリに分割
- sqlファイルの命名規則
  - `int_[entity]s_[verb]s.sql`
- intermediateレイヤーで起こり得る変換は多様であるため、厳密にどのように名前を付けるか難しい
- 最も良い指針は、intermediateレイヤーの動詞で考える
  - pivoted、aggregated_to_user、joined、fanned_out_by_quantity、funnel_created
- ダブルアンスコは使わなくて良い
  - 結局破綻するらしい
- あまり早い段階で分割や最適化を行わないこと
  - もしマートモデルが10個未満で、開発や使用に問題がない状況
  - ステージングレイヤーは例外だが、そうでなければサブディレクトリは不要
  - たぶんintermediate内に、という風に理解した
- sql内にjinjaでfor文などの制御構文を書ける
- intermediateはエンドユーザ（ダッシュボード、アプリ）に公開しない
- materializedはephemerallyにする
- intermediateの目的は、マートモデルの複雑さを解消すること
  - マートに10個のJOINではなく、２つのintermediateモデルをJOINする

## [Marts: Business-defined entities](https://docs.getdbt.com/guides/best-practices/how-we-structure/4-marts)

- セマンティック・レイヤーを使用するか否かで異なる
  - 使用しないプロジェクトでは、このベストプラクティスに従って、大幅に非正規化することが推奨
  - セマンティックレイヤーを使用している場合は、MetricFlowが最も柔軟に対応できるように、できるだけ正規化することを推奨
- 部署や関心のある分野ごとにグループ化する
- マートの数が10個以下であれば、サブフォルダの必要性はあまりない
- 中間層と同様に、あまり早い段階で最適化しすぎないように
- 純粋なマートの場合、ここには時間ディメンション（orders_per_day）は存在しないことに注意
- Materializedはtables or incrementalとする
  - すべてのマートモデルをデフォルトでインクリメンタルにしようと急ぐと、余計な手間がかる
- martとintermediateの判断基準はjoin数は一つキーとなりそう（必ずしもではないが）
- あるマートを使用して別の後発のマートを構築することは問題ないがリソースの浪費や循環的な依存関係を避けるために慎重な検討が必要
- 本番環境ではビューとエフェメラルモデルをマートまで積み重ね、エンドユーザに本当に使ってもらいたいモデルができたときだけ、チェーンの最後にデータをウェアハウスに構築する（テーブルにする）ことが理想的
- しかし開発ではいくつかの困難が生じる
  - ある種のエラーが後のモデルで表面化しているように見えても、実際はモデルチェーン内のずっと以前の依存関係（エラーが発生するモデルより前に構築されたDAG内の祖先モデル）に起因していることがある
  - データベースエラーの場所や内容を特定するのが難しい場合、一時的に特定のモデルチェーンをテーブルとして構築し、実際にエラーが発生している場所でウェアハウスがエラーを投げるようにすることが役立ちます。
- sqlファイルの命名規則
  - たぶんない、テーブル名通り
  - そのためよく見たらmartのsqlにはmartって付けないみたいだ

## [Marts for the Semantic Layer](https://docs.getdbt.com/guides/best-practices/how-we-structure/5-semantic-layer-marts)

- またプレビューらしいので一旦スキップ
  - https://classmethod.slack.com/archives/C02BAHX349F/p1696294775626299


## [The rest of the project](https://docs.getdbt.com/guides/best-practices/how-we-structure/6-the-rest-of-the-project)

- 昔はschema.ymlに書いていたけど今は分割するらしい
  - `_[directory]__models.yml`
  - `_[directory]__sources.yml`
- docも以下のように書くとのこと
  - `_[directory]__docs.md`
  - [About documentation | dbt Developer Hub](https://docs.getdbt.com/docs/collaborate/documentation#using-docs-blocks)

```text
models
├── intermediate
│   └── finance
│       ├── _int_finance__models.yml
│       └── int_payments_pivoted_to_orders.sql
├── marts
│   ├── finance
│   │   ├── _finance__models.yml
│   │   ├── orders.sql
│   │   └── payments.sql
│   └── marketing
│       ├── _marketing__models.yml
│       └── customers.sql
├── staging
│   ├── jaffle_shop
│   │   ├── _jaffle_shop__docs.md
│   │   ├── _jaffle_shop__models.yml
│   │   ├── _jaffle_shop__sources.yml
│   │   ├── base
│   │   │   ├── base_jaffle_shop__customers.sql
│   │   │   └── base_jaffle_shop__deleted_customers.sql
│   │   ├── stg_jaffle_shop__customers.sql
│   │   └── stg_jaffle_shop__orders.sql
│   └── stripe
│       ├── _stripe__models.yml
│       ├── _stripe__sources.yml
│       └── stg_stripe__payments.sql
└── utilities
    └── all_dates.sql
```
- ymlを一つにすることも技術的にはできるけどバッドプラクティス
- materializedなどは共通設定も使う

```yaml
-- dbt_project.yml

models:
  jaffle_shop:
    staging:
      +materialized: view
    intermediate:
      +materialized: ephemeral
    marts:
      +materialized: table
      finance:
        +schema: finance
      marketing:
        +schema: marketing
```

- タグ付けもまた、この原則が発揮される領域
  - dbtに慣れていない人の多くは、厳密なフォルダ構造ではなくタグに頼ってしまい、すぐにすべてのモデルにタグが必要な状態に陥ってしまいます。
  - これは不必要な複雑さを生み出す
  - dbt build --select marts.marketingのようなフォルダベースの選択は、すべてのマーケティング関連モデルにタグを付け、すべての開発者が新しいモデルにそのタグを追加することを覚えていることを期待し、dbt build --select tag:marketingを使うよりもはるかにシンプルです。
  - ベタで日本語訳をはったけど、たぶんタグは例外的に使って、基本はフォルダ単位でタグを決めておく方が良いらしい
- `seed`フォルダ
  - ルックアップテーブル用のシード
  - モデリングに役立つがソースシステムには存在しないルックアップテーブルをロードすること
  - この例のプロジェクトでは、従業員をcustomer_idにマップする小さなシードを用意し、特別なロジックで従業員の購買を処理できるようにしている
  - ソース・データをロードするためのシードはNG
- `analyses`フォルダ
  - 分析クエリ保存用
  - Jinja を使用してバージョン管理したいクエリを保存可能
  - ここには無限の可能性があります（あんま使わんか？）
  - [dbt-labs/dbt-audit-helper: Useful macros when performing data audits](https://github.com/dbt-labs/dbt-audit-helper)
- `tests`フォルダ
  - 複数の特定のテーブルを同時にテストするための テスト
  - dbtのテストが進化するにつれて、単発のテストを書く必要性が少なくなってきました。
  - dbt-utils と dbt-expectations の追加テストの間に、ほとんどすべての状況をカバーすることができます
  - [dbt-labs/dbt-utils: Utility functions for dbt projects.](https://github.com/dbt-labs/dbt-utils)
  - [calogica/dbt-expectations: Port(ish) of Great Expectations to dbt test macros](https://github.com/calogica/dbt-expectations)
- `snapshot`フォルダ
  - ソース・データから、ゆっくりと変化するタイプ 2 のディメンジョン・レコードを作成するためのもの
  - これはdbtドキュメントで詳しく説明されていますが、他のフォルダとは異なり、より明確な目的があります。
  - [Add snapshots to your DAG | dbt Developer Hub](https://docs.getdbt.com/docs/build/snapshots)
- `macro`フォルダ
  - 何度も行う変換をDRYにするためのマクロです。スナップショットと同様、マクロの詳細については、このガイドの範囲外であり、別の場所で十分にカバーされています
  - [Jinja and macros | dbt Developer Hub](https://docs.getdbt.com/docs/build/jinja-macros)
  - [How do I document macros? | dbt Developer Hub](https://docs.getdbt.com/faqs/docs/documenting-macros)
- プロジェクト分割について
  - 「他に選択肢がないか、より複雑な回避策を省くことができない限り、分割は避けるべきだ」というスタンス
  - ガバナンス上の理由やプロジェクトサイズが大きすぎる場合はありっぽい

## 最後に

jaffle_shopどこにあんねん
