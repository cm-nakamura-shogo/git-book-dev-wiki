# LLM : Retriever(LlamaIndex)

### [2023-04-09 LlamaIndexでクエリに回答したリファレンスを取得する方法](https://dev.classmethod.jp/articles/get-reference-in-query-of-llamaindex/)

- file_metadataを使うことで、node.node.extra_infoにファイル名をもたせることができる。
- リファレンスの情報はレスポンスのsource_nodesに含まれる

### [2023-04-11 LlamaIndex でSQL生成を試す](https://note.com/hmj_kd/n/n24c8e2858e96)

- スキーマからSQLを生成している面白い事例


### [2023-04-11 LlamaIndexの検証機能 ResponseとSourceをGPT-4に評価させて正しいかを判断する](https://twitter.com/jerryjliu0/status/1645451897372024832)

- 以下のコード例によればGPT-4に検証させている様子（つまりGPT-4のAPIが使えない場合は使えない機能）
  - https://github.com/jerryjliu/llama_index/blob/main/examples/evaluation/TestNYC-Evaluation-Query.ipynb

### [2023-04-12 LlamaIndexでPinconeを使って疎と密のハイブリットな検索を試す](https://note.com/npaka/n/n63afe0e6684a)

- devioの記事と疎密の意味が少し違いそう？要確認。

### [2023-04-17 llama_indexの公式がソースにクエリの答えが含まれているかを評価する方法を紹介](https://twitter.com/jerryjliu0/status/1647626532519841793)

- それぞれのソースとクエリを入力として、含まれるかどうかをYes,Noで答えさせることにより実現

### [2023-04-17 llama_indexの公式が単一のルータを使って使用するIndexを複数の中から選択する例の紹介](https://twitter.com/gpt_index/status/1647625929165008897)

### [2023-04-19 llama-indexがGoogle検索などの検索機能を追加](https://twitter.com/jerryjliu0/status/1648347966615465984)

- 以下が挙げられている
  - 📝 Note-taking capabilities
  - 🌐 Web Page search
  - 🔎 @google search capabilities

- LangChainと同じようなアイディアで、多分各インデックスの説明文とクエリの比較により判断するものかと

### [2023-04-29 LlamaIndex 0.6.0 - データに対する新しいクエリインターフェイス｜npaka｜note](https://note.com/npaka/n/n4254fc549dc0)

- 大きめの変更が加えられており、APIが整理されている
- queryなどの使い方の違い、indexはビューに過ぎない点などが特徴か
- クイックスタートガイドの続編
  - [LlamaIndex クイックスタートガイド - v0.6.0｜npaka｜note](https://note.com/npaka/n/n50475d6c3118)

### [2023-05-02 LlamaIndexのデバッグ機能のCallbackManagerとLlamaDebugHandlerの追加](https://twitter.com/gpt_index/status/1653407672602071040?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-05-16 LlamaIndex 0.6.8の紹介](https://twitter.com/gpt_index/status/1658481782923362306)

- PDFの出典元を得られるように
  - SimpleDirectoryReaderでpdfを読み込むと自動でnodeのextra_infoにpage_labelが付与
  - [https://github.com/jerryjliu/llama_index/blob/main/docs/examples/citation/pdf_page_reference.ipynb](https://github.com/jerryjliu/llama_index/blob/main/docs/examples/citation/pdf_page_reference.ipynb)
- LLM-based Rerankingでより高精度なRetrievalを行う
  - stage1が埋め込みベクトル、stage2がLLMを使ったRerankingで高速かつ精度の良いNode抽出を行える
  - [https://twitter.com/jerryjliu0/status/1657827898517012486](https://twitter.com/jerryjliu0/status/1657827898517012486)
- 外部にデータを送信しない「ローカルオンリー」モードで使用するチュートリアルを追加
  - [https://twitter.com/jerryjliu0/status/1658119334080724993](https://twitter.com/jerryjliu0/status/1658119334080724993)
  - LLMはGPT4ALL、埋め込みにはsentence-transformersを使用する例となっている

### [2023-05-20 LlamaIndex 0.6.9](https://twitter.com/gpt_index/status/1659593915903926277)

- Fsspecをサポート
  - vector_store/doc_store内のオブジェクトを、fsspecがサポートするあらゆるオブジェクトストレージに永続化が可能に
  - S3, GCS, Azure blobその他が含まれる
- S3KVStore
  - S3をネイティブなKey-Valueストアとしてサポートするように
  - S3DBKVStoreという名前でdoc_storeとindex_storeに対応
  - BaseKVStoreはこれでMongoDBS3が対応し、KVStoreで使えるようになるはず
  - あまりドキュメントには記載されていない
- ResponseBuilderにAccumulatorが追加
  - ResponseMode.ACCUMULATEが増えている
  - 各ノードに均等にクエリし結果を連結するらしい。
  - ともなって設計的にBaseResponseBuilderが生えており、抽象化が進んだ
- SubQuestionQueryEngineが追加
  - 複雑なクエリ（例：比較対照）を多くのサブクエリに分解して実行するクエリエンジン

### [2023-05-24 LlamaIndex 0.6.10](https://github.com/jerryjliu/llama_index/compare/v0.6.9...v0.6.10)

- 余り変更点は多くなさそう
- PDFReaderのメタデータにpage_labelに加えて、file_nameが追加されている

### [2023-05-26 LlamaIndex 0.6.11](https://github.com/jerryjliu/llama_index/compare/v0.6.10.post1...v0.6.11)

- vellum_aiとのインテグレーション
  - プロンプトをバージョンアップ/デプロイ/監視する
- BaseCallbackHandlerにstart_traceとend_traceが追加
  - ともなってLlamaDebugHandlerにもいくつか修正が入っている
- DynamoDBのストアが追加
  - index_store, doc_store, vectore_storeにも対応している

### [2023-05-28 LlamaIndex 0.6.12](https://github.com/jerryjliu/llama_index/compare/v0.6.11...v0.6.12)

- ResponseMode.COMPACT_ACCUMULATEが追加
  - COMPACTがチャンク再統合なのでより効率的に動作する
- プロンプト関連の処理がPromptTypeというAPIで再構成されている
  - https://github.com/jerryjliu/llama_index/blob/v0.6.12/llama_index/prompts/prompt_type.py


### [2023-05-28 LlamaIndex 0.6.13](https://github.com/jerryjliu/llama_index/compare/v0.6.12...v0.6.13)

- [Graphsignal](https://graphsignal.com/)との連携
  - AIエージェントやLLMを搭載したアプリケーションに観測性を提供
- SQLAutoVectorQueryEngineの追加

### [2023-05-30 LlamaIndex 0.6.14](https://github.com/jerryjliu/llama_index/compare/v0.6.13...v0.6.14)

- ChatEngineなる新しいエンジンが追加
  - 種類としてはSimpleChatEngine、ReActChatEngine、CondenseQuestionChatEngine
  - as_chat_engineでインスタンス化し、切り替えはChatModeで実施できる。デフォルトはCondenseQuestionChatEngine。
- 内部的にglobal_service_contextができている。用途は不明。
- PromptTypeにCONVERSATION、DECOMPOSE、CHOICE_SELECTが追加

### [2023-05-31 LlamaIndex 0.6.15](https://github.com/jerryjliu/llama_index/compare/v0.6.14...v0.6.15)

- Agentに関するユースケースが追加されたのみ
  - [docs/use_cases/agents.md](docs/use_cases/agents.md)

### [2023-06-01 LlamaIndex 0.6.16](https://github.com/jerryjliu/llama_index/compare/v0.6.15...v0.6.16.post1)

- 引数など使い方に影響のある名前変更あり
  - デフォルト定数に一部変更有。これに応じて引数が変わるので要注意。
    - NodeParser側
      - DEFAULT_CHUNK_OVERLAPが200から20に。これは要注意。
      - DEFAULT_CHUNK_SIZEはそのまま。
      - chunk_size_limitもchunck_sizeに変わっている
    - PromptHelper側
      - MAX_CHUNK_OVERLAPが消滅。max_chunk_overlapが非推奨となり代わりにchunk_overlap_ratioを使用するようになった影響
      - DEFAULT_CHUNK_OVERLAP_RATIOは0.1となっている
      - MAX_CHUNK_SIZEがDEFAULT_CONTEXT_WINDOWに名前変更
      - NUM_OUTPUTSがDEFAULT_NUM_OUTPUTSに名前変更
  - 各データストアのto_dictがなくなりto_jsonに変更
- RetryQueryEngineが追加
  - 内部でFeedbackQueryTransformationを使う
  - FeedbackQueryTransformationが追加
    - Evaluatorの結果を使ってクエリにフィードバックが可能に。これがEvaluatorを抽象型にした背景っぽい。
  - BaseEvaluatorという新しい抽象型で評価系が実装
    - もともとQueryResponseEvaluatorがあったがEvaluatorが抽象型の親クラスを持つように変更されている
- PromptHelperの修正
  - compact_text_chunksがrepackという名前に代わっている
  - truncateという複数ノードのテキストをつなげる処理が追加
  - chunk_overlap_ratioが指定できるように
- PsychicReaderが追加
  - Psychicは多くのSaaSアプリのデータを1つのユニバーサルAPIで同期させることができるプラットフォーム

### [2023-06-01 LlamaIndex 0.6.16.post1](https://github.com/jerryjliu/llama_index/compare/v0.6.16...v0.6.16.post1)

- SubQuestionQueryEngineのパッチ

### [2023-06-03 LlamaIndex 0.6.17](https://github.com/jerryjliu/llama_index/compare/v0.6.16.post1...v0.6.17)

- Nodeの削除系操作について見直しが入っている
- RefDocInfoにAPIがいくつか追加

### [2023-06-03 LlamaIndex 0.6.18](https://github.com/jerryjliu/llama_index/compare/v0.6.17...v0.6.18)

- Vector StoreにMyScaleVectorStoreとSupabaseVectorStoreが追加
- FunctionTool、BaseToolSpecの具象化クラスNotionToolSpec、TestToolSpecが追加。用途はあまりわかってない
