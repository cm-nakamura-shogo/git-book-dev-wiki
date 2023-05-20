# LLM : アプリケーション(記事)

### [2023-05-11 低レイテンシーなテキスト生成について (Hugging Face)](https://huggingface.co/blog/assisted-generation)

- 量子化、バッチ化、並列化が既存
- これに対してASSISTANT MODELを使って生成することで低レイテンシーを実現
- TransformersのAPIを使えば簡単に利用可能らしい

### [2023-05-09 StarCoderをチャット用にチューニングして利用する (Hugging Face)](https://huggingface.co/blog/starchat-alpha)

### [2023-05-01 長文から論点を抽出して、その論点を軸に文章の要約を試みる](https://note.com/mahlab/n/ndce1a18681e8)

- 手順は以下
  - CharacterTextSplitterで300字のチャンクに分割
  - チャンク毎にtext-embedding-ada-002で埋め込みベクトルを生成
  - Faissを使いk-means法でクラスタ数を5としてクラスタに分ける
  - 各クラスタ毎にload_summarize_chainで要約する
  - 各クラスタにLLMでタイトルをつけてもらう
- 割と要約の選択肢として良いのかも。

### [2023-03-19 NAVERがGPT-3と商品検索を組み合わせた論文](https://twitter.com/sz_dr/status/1637460944707289088)

- コンテキスト保持の仕組みの参考になると考えられる

### [2023-03-10 GPTが出した回答の確からしさを見えるようにしてみる](https://acro-engineer.hatenablog.com/entry/2023/03/10/100000)

- NLIタスク、前提文と仮説文が与えられたときに、仮説文が前提文に対して、以下のいずれかの関係であることを推論するタスクで検証

### [2023-03-08 ChatGPT APIとFaissを使って長い文章から質問応答する仕組み](https://qiita.com/sakasegawa/items/16714fa132e874cab069)

- sakasegawa氏
- LlamaIndexを使わずにスクラッチで仕組みを考える場合には良いかも。

### [2023-03-06 ChatGPTとMakeを使ってGmailの返信を自動化してみる](https://qiita.com/sakasegawa/items/d8fb1889cdc77d050c01)

- sakasegawa氏
- Makeはいわゆるmakeではなくてインテグレーションするツールの話
