# Snowflake

## Snowpark

- [Machine Learning with Snowpark Python](https://quickstarts.snowflake.com/guide/machine_learning_with_snowpark_python/index.html?utm_cta=website-workload-data-science-resources-ml-with-snowpark-python-quickstart#0)
- [Snowpark Pythonでの関数とストアドプロシージャの呼び出し | Snowflake Documentation](https://docs.snowflake.com/ja/developer-guide/snowpark/python/calling-functions)
- [[新機能]Snowpark for PythonのコーディングがSnowsight上で出来る「Python Worksheets」がパブリックプレビューになりました #SnowflakeDB | DevelopersIO](https://dev.classmethod.jp/articles/snowflake-python-worksheets-public-preview/)
- [Snowpark Container Services — A Tech Primer | by Caleb Baechtold | Snowflake | Jul, 2023 | Medium](https://medium.com/snowflake/snowpark-container-services-a-tech-primer-99ff2ca8e741)
- [推薦システムにおけるSnowparkの活用 - dely Tech Blog](https://tech.dely.jp/entry/2023/03/24/131917)

## Snowflake Summit 2023

### サマリ

- これまでデータだけをやりとりできたSnowflake Marketplaceで、Streamlitを用いたデータアプリ・UDF・ストアドプロシージャを販売＆共有できるように
    - 公式ブログ：https://www.snowflake.com/blog/native-app-framework-available-developers-aws/
    - チュートリアル：https://quickstarts.snowflake.com/guide/getting_started_with_native_apps/#0
- Snowpark Container Servicesが発表され、コンテナアプリケーションをSnowflake上で実行可能となる予定。このサービスではアプリの基盤にNVIDIAのGPUを用いることも可能。さらに、開発したアプリをMarketplaceで公開可能になるため、自作のLLMを組み込んだアプリケーションが提供できる
  - Reka社の事例：Reka社が構築したLLMをStreamlitに組み込んだアプリを開発し、Snowflake Marketplaceを介して使用できるようにした
    - デモ動画：https://www.youtube.com/watch?v=wkLABriF-a0
  - 参考記事：https://www.snowflake.com/blog/https-www-snowflake-com-blog-snowpark-container-services-deploy-genai-full-stack-apps/?lang=ja
  - 参考記事：https://zenn.dev/yamnaku/articles/d92e447bb882a1#snowpark-container-service---%E3%81%82%E3%82%89%E3%82%86%E3%82%8B%E3%83%A9%E3%83%B3%E3%82%BF%E3%82%A4%E3%83%A0%E3%82%92snowflake%E4%B8%8A%E3%81%A7%E5%8B%95%E3%81%8B%E3%81%9D%E3%81%86
- Generative AIや機械学習の分野で、SnowflakeがMicrosoftとのパートナーシップを拡大することを発表
  - 参考記事：https://investors.snowflake.com/news/news-details/2023/Snowflake-Expands-Partnership-with-Microsoft-to-Bring-Large-Scale-Generative-AI-Models-and-Increased-Machine-Learning-Capabilities-to-the-Data-Cloud/default.aspx


### [Snowflake Expands Developer Programmability with Streaming Capabilities, DevOps, and more](https://www.snowflake.com/blog/snowflake-expands-developer-programmability-snowpark-container-services/)

- Python 3.9と3.10がSnowparkで使えるように　※Summit前にパブリックプレビュー
- Pythonパッケージのホワイトリストとブロックリスト　※プライベートプレビュー
- 外部ネットワーク アクセスを使用して安全な方法でAPI およびエンドポイントと統合できるように　※在プライベート プレビュー
- Snowpark Container Serviceで、GPUも選べて、コンテナアプリをクラスタ管理なしで簡単にデプロイできる
- Snowpark ML Modeling API
  - ML Modeling API　※パブリックプレビュー
    - ストアド プロシージャを作成したり並列化を利用したりすることなく、Snowflake のデータに対して Sklearn スタイルの処理をネイティブに実装できる
  - ML Operations API　※プライベートプレビュー
- Snowpark Model Registry
  - 学習後のモデルを格納するRegistry
  - ML Operations API を使用してモデルを Snowflake にシームレスにデプロイ
- Snowflake上でのStreamlit　※まもなくパブリックプレビュー
- ストリーミングパイプラインの構築
  - Dynamic TablesでSQL書くだけで変換パイプラインが作れる　※パブリックプレビュー
  - Snowpipe StreamingでKafkaなどのストリーミングデータを直接Snowflakeのテーブルへ　※まもなくGA
- 開発者エクスペリエンスの向上
  - Gitとの連携により、Git リポジトリに存在するアセットを Snowflake 内で表示、実行、編集、共同作業できる　※プライベートプレビュー
  - Snowflake CLIは、アプリ向けのワークロードに設計されたCLI。Streamlit、Native App、Snowpark Containers、Snowpark などのワークロード全体で Snowflake 上で実行されるアプリを作成、管理、更新、表示できる　※プライベートプレビュー
  - Event Tablesを使ったLoggingとTracing　※パブリックプレビュー

### [Snowflake Vision for Generative AI and LLMs](https://www.snowflake.com/blog/generative-ai-llms-summit-2023/)

- Snowflake Marketplaceを介して、Snowpark Container Servicesを使ったSnowflake Native Appをすぐにインストールすることが可能
  - LLMを用いたアプリケーションもあり、AI21 Labs、Reka、NVIDIA (NeMo フレームワーク、NVIDIA AI Enterpriseソフトウェア プラットフォームの一部)がすでに提供されている
  - デモはこちら
    - https://www.youtube.com/watch?v=wkLABriF-a0
- StremlitとLLMの組み込み
  - 7,000 を超える LLM を利用した Streamlit アプリがCommunity Cloud上にすでに作成されており、その数は日々増加しています。GitHub だけでも 190,000 以上の Streamlit コード が存在
  - SnowflakeとStremlitの統合もまもなくパブリックプレビュー
- ネイティブなLLM
- Document AIにより、ドキュメントから簡単にデータを抽出　※プライベートプレビュー

### [Snowpark:マネージドコンテナ、ML API、Python ランタイム、DevOps など](https://www.snowflake.com/blog/https-www-snowflake-com-blog-snowpark-ml-api-python-develops-more/?lang=ja)

- Snowflake内の新しいPython (Anaconda) ライブラリのサポート
  - 間もなくリリースされる予定のライブラリには、langchain、implicit、inbalanced-learn、rapidfuzz、rdkit、mlforecast、statsforecast、scikit-optimize、scikit-surpriseなど
- Python 非構造化データ処理 　※パブリックプレビュー
  - Python UDF、UDTF、ストアドプロシージャを活用して、内部/外部ステージまたはオンプレミスストレージにある非構造化ファイル (画像、動画、音声、カスタム形式など) を安全かつ動的に読み取れる
- 外部ネットワークアクセス　※プライベートプレビュー
  - Snowpark コード (UDFS/UDTF およびストアドプロシージャ) から外部エンドポイントにシームレスに接続
- Python パッケージポリシー　※プライベートプレビュー
  - 自分のアカウントで利用されている Anaconda パッケージのガバナンスを強化するための許可リストとブロックリストを設定できる
- ユーザー定義集計関数（UDAF）
  - 複数の行の値を処理し、結果として単一の集計値を返す関数をユーザーが作成できる
- ベクトル化された UDTF　※まもなくパブリックプレビュー
  - パーティション上で動作するテーブル関数を Pandas DataFrames として作成し、結果をPandas DataFrame または Pandas の配列として返すことができる
  - プロセス関数で行ごとにデータを収集するよりもdataframesを連結する方が速い
- Python Task API　※まもなくプライベートプレビュー
  - Snowflake Tasks/DAG を作成および管理するためのPyhon API
- Snowpark Local Testing　※プライベートプレビュー
  - Snowparkで開発する時、Snowflakeにライブ接続しなくてもSnowparkセッションとDataFrameの作成ができる
- Native Git Integration　※まもなくプライベートプレビュー
  - SnowflakeアカウントからGitリポジトリに安全に接続し、Snowflake内の任意のブランチ/タグ/コミットのコンテンツにアクセスできる
  - 統合後、ユーザーはステージ上のファイルのようにリポジトリとブランチを参照するだけで、UDF、ストアドプロシージャ、Streamlit Apps、およびその他のオブジェクトを作成できる
- Triggered Tasks　※プライベートプレビュー
  - Streamが更新されたタイミングで実行できるタスク
