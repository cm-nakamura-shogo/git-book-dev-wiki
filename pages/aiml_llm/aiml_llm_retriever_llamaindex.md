# LLM : Retriever(LlamaIndex)

### [2023-05-28 LlamaIndex 0.6.12](https://github.com/jerryjliu/llama_index/compare/v0.6.11...v0.6.12)

- ResponseMode.COMPACT_ACCUMULATEが追加
  - COMPACTがチャンク再統合なのでより効率的に動作する
- プロンプト関連の処理がPromptTypeというAPIで再構成されている
  - https://github.com/jerryjliu/llama_index/blob/v0.6.12/llama_index/prompts/prompt_type.py

### [2023-05-26 LlamaIndex 0.6.11](https://github.com/jerryjliu/llama_index/compare/v0.6.10.post1...v0.6.11)

- vellum_aiとのインテグレーション
  - プロンプトをバージョンアップ/デプロイ/監視する
- BaseCallbackHandlerにstart_traceとend_traceが追加
  - ともなってLlamaDebugHandlerにもいくつか修正が入っている
- DynamoDBのストアが追加
  - index_store, doc_store, vectore_storeにも対応している

### [2023-05-24 LlamaIndex 0.6.10](https://github.com/jerryjliu/llama_index/compare/v0.6.9...v0.6.10)

- 余り変更点は多くなさそう
- PDFReaderのメタデータにpage_labelに加えて、file_nameが追加されている

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

### [2023-05-02 LlamaIndexのデバッグ機能のCallbackManagerとLlamaDebugHandlerの追加](https://twitter.com/gpt_index/status/1653407672602071040?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-04-29 LlamaIndex 0.6.0 - データに対する新しいクエリインターフェイス｜npaka｜note](https://note.com/npaka/n/n4254fc549dc0)

- 大きめの変更が加えられており、APIが整理されている
- queryなどの使い方の違い、indexはビューに過ぎない点などが特徴か
- クイックスタートガイドの続編
  - [LlamaIndex クイックスタートガイド - v0.6.0｜npaka｜note](https://note.com/npaka/n/n50475d6c3118)


### [2023-04-19 llama-indexがGoogle検索などの検索機能を追加](https://twitter.com/jerryjliu0/status/1648347966615465984)

- 以下が挙げられている
  - 📝 Note-taking capabilities
  - 🌐 Web Page search
  - 🔎 @google search capabilities

### [2023-04-17 llama_indexの公式がソースにクエリの答えが含まれているかを評価する方法を紹介](https://twitter.com/jerryjliu0/status/1647626532519841793)

- それぞれのソースとクエリを入力として、含まれるかどうかをYes,Noで答えさせることにより実現

### [2023-04-17 llama_indexの公式が単一のルータを使って使用するIndexを複数の中から選択する例の紹介](https://twitter.com/gpt_index/status/1647625929165008897)

- LangChainと同じようなアイディアで、多分各インデックスの説明文とクエリの比較により判断するものかと


### [2023-04-12 LlamaIndexでPinconeを使って疎と密のハイブリットな検索を試す](https://note.com/npaka/n/n63afe0e6684a)

- devioの記事と疎密の意味が少し違いそう？要確認。


### [2023-04-11 LlamaIndexの検証機能 ResponseとSourceをGPT-4に評価させて正しいかを判断する](https://twitter.com/jerryjliu0/status/1645451897372024832)

- 以下のコード例によればGPT-4に検証させている様子（つまりGPT-4のAPIが使えない場合は使えない機能）
  - https://github.com/jerryjliu/llama_index/blob/main/examples/evaluation/TestNYC-Evaluation-Query.ipynb


### [2023-04-11 LlamaIndex でSQL生成を試す](https://note.com/hmj_kd/n/n24c8e2858e96)

- スキーマからSQLを生成している面白い事例


### [2023-04-09 LlamaIndexでクエリに回答したリファレンスを取得する方法](https://dev.classmethod.jp/articles/get-reference-in-query-of-llamaindex/)

- file_metadataを使うことで、node.node.extra_infoにファイル名をもたせることができる。
- リファレンスの情報はレスポンスのsource_nodesに含まれる
