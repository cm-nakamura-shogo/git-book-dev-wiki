# LLM : Retriever(LangChain)

### [2023-02-23 LangChainのAgentがどのようにToolを選択しているかを確認したメモ](https://www.inoue-kobo.com/ai_ml/langchain-agent/)

- descritionsが重要という点がポイントか
- Python使いでも概要をおさえるのは良さそう

### [2023-03-11 ChatGPTクローンをFastAPI・WebSocket・LangChain・Reactで](https://zenn.dev/ktechb/articles/chatgpt-clone-stream)

- 普通にバックエンドフロントエンドは参考になるやも
- 記憶には、LangChainのPromptTemplateを使っている

### [2023-04-08 GPTをドーピングする LangChain 基礎編](https://zenn.dev/takiko/articles/24217eece242e1)

- TypeScriptでLangChainをする網羅的な内容

### [2023-04-11 LangChainとsupabaseを組み合わせるexample](https://blog.langchain.dev/langchain-x-supabase/)

- テンプレートを見てみないと詳細はわからぬ。

### [2023-04-12 langchainでAzure OpenAI使ったり、AD認証しながらReAct構成するコード](https://twitter.com/hiro_gamo/status/1645819925787971584)

### [2023-04-12 CAMEL: エージェント同士を会話させる論文の実験をLangChainで実現する方法](https://twitter.com/hwchase17/status/1645834030519296000)

- 元論文は3/31に出ている以下
  - [https://arxiv.org/abs/2303.17760](https://arxiv.org/abs/2303.17760)

### [2023-04-16 LangChain の チェーン・エージェントの評価](https://note.com/npaka/n/n7f7479bd3e19)

- こういった生成系の評価の悩みとそれの解決策が記載
- データの欠如についてはデータセットが記載されており、評価はLangChainの機能として評価用のツールやチェーンを紹介

### [2023-04-19 LangChainの0.0.143がリリース](https://twitter.com/langchainai/status/1648359232104976384)

- 結構規模が大きい
- Jira Toolkit : エージェントがJIRAの課題を検索し、作成することが可能
- Annoy VectorStore : vectorstoreが追加。Python バインディングを持つ C++ ライブラリ
- Image Caption Loader : Hugging FaceからBLIPモデルを使用し、画像のキャプションを生成し、それをデータとして読み込む
- Twitter Tweet Loader : Pythonパッケージを使用し、twitterユーザーのリストのツイートからテキストを読み込むことができるように
- Confluence Document Loader : これはそのまま
- Diffbot Document Loader : ？？？
- Big Query specific SQL Prompt : これもそのままかな
- Boolean filter for OpenSearch : ？？？

### [2023-04-19 LangChainをRWKVで駆動する例](https://note.com/npaka/n/n130a57aa384a)

- まあまだまだこれからだな
- `from langchain.llms import RWKV`でlangchainから使えるのは楽やね
- 使用モデルは`RWKV-4-Raven-14B-v9-Eng99%-Other1%-20230412-ctx8192.pth`
- 私のブログでは`RWKV-4-Raven-14B-v8-EngAndMore-20230408-ctx4096.pth`を使ってて、Ravenのアップデートが速いな

### [2023-04-20 プロンプトエンジニアリングから始めるLangChain入門 - Speaker Deck](https://speakerdeck.com/os1ma/puronputoenziniaringukarashi-merulangchainru-men)

- LangChainを調べる際に有用

### [2023-04-22 LangChain 0.0.146でcompress retrieved documentをリリース](https://twitter.com/hwchase17/status/1649428295467905025)

- クエリする前にRetriver側の情報を、クエリに関連する情報に圧縮する。
- Retriver作成時に圧縮するわけでないことに注意
- 以下で試した記事がある
  - [LangChainの新機能Contextual Compression Retrieverを試す｜mah_lab / 西見 公宏｜note](https://note.com/mahlab/n/n7d72e83904cc)

### [2023-05-03 LangChain v0.0.155アップデート](https://twitter.com/langchainai/status/1653469034804023298?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-05-06 サクッと始めるプロンプトエンジニアリング【LangChain / ChatGPT】](https://zenn.dev/umi_mori/books/prompt-engineer)

- LangChainを使うときに一番最初に読むにはええかも

### [2023-05-12 チャットボットのテストのためのチャットボットを作って自動で対話してもらう (mah_labさん)](https://note.com/mahlab/n/n377fef03d5a4)

- 2人の人格を作ってお互いに対話させるデモ
- 何をテストしたいのか正直分からんかった。少なくともプロンプトをテストするものではなく、LLMのテストな位置づけか。

### [2023-05-16 LangChainとAzure OpenAI版GPTモデルの連携部分を実装してみる - Qiita](https://qiita.com/tmiyata25/items/7a04096342241d8a2b4c)

- LangChain、簡単なベクターストアはできて結構よさげかもしれん。

### [2023-05-28 [翻訳] LangChainにおけるドキュメントに対するQ&Aのコンセプトガイド - Qiita](https://qiita.com/taka_yayoi/items/8f3251b44f4a6c7f5c64)

- よさげなのだが途中で終わっているので公式を読んだ方がよさそう

### [2023-06-03 LangChainの get_openai_callback が便利という話](https://twitter.com/mlbear2/status/1664801611594752000)

- 勉強時のご参考
