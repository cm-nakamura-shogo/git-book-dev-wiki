# LLM : アプリケーション(記事)

### [2023-03-06 ChatGPTとMakeを使ってGmailの返信を自動化してみる](https://qiita.com/sakasegawa/items/d8fb1889cdc77d050c01)

- sakasegawa氏
- Makeはいわゆるmakeではなくてインテグレーションするツールの話

### [2023-03-08 ChatGPT APIとFaissを使って長い文章から質問応答する仕組み](https://qiita.com/sakasegawa/items/16714fa132e874cab069)

- sakasegawa氏
- LlamaIndexを使わずにスクラッチで仕組みを考える場合には良いかも。

### [2023-03-10 GPTが出した回答の確からしさを見えるようにしてみる](https://acro-engineer.hatenablog.com/entry/2023/03/10/100000)

- NLIタスク、前提文と仮説文が与えられたときに、仮説文が前提文に対して、以下のいずれかの関係であることを推論するタスクで検証

### [2023-03-19 NAVERがGPT-3と商品検索を組み合わせた論文](https://twitter.com/sz_dr/status/1637460944707289088)

- コンテキスト保持の仕組みの参考になると考えられる

### [2023-05-01 長文から論点を抽出して、その論点を軸に文章の要約を試みる](https://note.com/mahlab/n/ndce1a18681e8)

- 手順は以下
  - CharacterTextSplitterで300字のチャンクに分割
  - チャンク毎にtext-embedding-ada-002で埋め込みベクトルを生成
  - Faissを使いk-means法でクラスタ数を5としてクラスタに分ける
  - 各クラスタ毎にload_summarize_chainで要約する
  - 各クラスタにLLMでタイトルをつけてもらう
  - 割と要約の選択肢として良いのかも。

### [2023-05-09 StarCoderをチャット用にチューニングして利用する (Hugging Face)](https://huggingface.co/blog/starchat-alpha)

### [2023-05-11 低レイテンシーなテキスト生成について (Hugging Face)](https://huggingface.co/blog/assisted-generation)

- 量子化、バッチ化、並列化が既存
- これに対してASSISTANT MODELを使って生成することで低レイテンシーを実現
- TransformersのAPIを使えば簡単に利用可能らしい

### [2023-05-13 ChatGPTで独自データを扱うためのエンべディング](https://note.com/ogatahisato/n/n899dcb459f35)

- 基本的な内容で新しいものはない

### [2023-06-12 自然な対話で商品検索！OpenAI と全文検索エンジンで対話型ゆるふわ検索 AI アシスタントを作ってみた](https://dev.classmethod.jp/articles/interactive-fuzzy-item-search-with-openai-api/)

- フレームワークや検索方法の判断基準などが書いてありとても有用

### [2023-06-14 GPT-3.5-turboの新機能を使ってCVPRの論文を良い感じに検索・推薦・要約するシステム](https://zenn.dev/turing_motors/articles/579ffa1c80661a)

- まあ想定の範囲内な内容だった
- streamlitは把握しておかないと今後役に立つのかもな

### [2023-06-15 LangChain の「OpenAI Functions Agent」を試す](https://note.com/hamachi_jp/n/nbcaa7cff259d)

- もともとtoolsが同様の機能であったため、かなり自然な形でFunction Callingがマージされている
- initialize_agentで、agent=AgentType.OPENAI_FUNCTIONSを指定するのみ

### [2023-06-17 OpenAIのFunction calling機能を活かした、LangChainの新機能Taggingを試す](https://note.com/hamachi_jp/n/n8237d3e0b8ed)

- Function Callingを使ってテキストに感情やスピード、ボリュームなどをタグ付けする機能
- 記事ではその結果をRINNAを使って音声合成している

### [2023-06-22 機械翻訳は人間を超えるのか | DevelopersIO](https://dev.classmethod.jp/articles/machine_translation_human/)

- さすがにDeepLの方がまだ頑張っていそう。GPT-4なら分からんけど。