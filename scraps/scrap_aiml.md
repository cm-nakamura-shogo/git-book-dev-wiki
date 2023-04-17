# AIML

ほぼスクラップ帳。

mlnewsに載せないものも含まれる。基本は全部載せたものであるべきだが、別の方がシェアしたものはその限りではない。

以下misc-mlシェア検討済み。
---

### [2023-04-14 Google Colab で BabyAGI を試す](https://note.com/npaka/n/n97152182c98a)

- タスク駆動型自律エージェントのフレームワークです。ゴールに基づいてタスクの作成、優先順位付け、および実行を行う。
- 無限ループで自動でトークンを消費するのでそこは注意。
- GPT-4がやっぱ強い。

### [2023-04-14 SAMよりもより広範な機能をもつSEEMが公開](https://twitter.com/forasteran/status/1646829112844259329)

- この界隈がまだよくわからいので、差異をまだ理解できていない。

### [2023-04-14 SAMを利用したZero-shotなPanoptic Segmentation](https://twitter.com/tobiascornille/status/1646812086154960896)

- 「Segment Anything, Grounding DINO, and CLIPSeg.」というパイプラインで実現

### [2023-04-14 Databricks社のプラットフォームで学習した12Bの言語モデルを使ってみた](https://note.com/masayuki_abe/n/n72f66715a4f8)

- dolly-v2-12bという名前でHugging Faceに公開。
  - [https://huggingface.co/databricks/dolly-v2-12b](https://huggingface.co/databricks/dolly-v2-12b)
- 日本語はNGっぽい。

### [2023-04-14 AutoGPTやAgentGPTやら自律的にタスクを解く](https://twitter.com/jerryjliu0/status/1646172524173209600?s=12&t=0nszgXsDXAd-L4WiCutIWg)

- AutoGPTは環境構築が必要だが、AgentGPTというWebサービス版がある。

### [2023-04-13 YeagerAI: Langchain Agentクリエイター](https://twitter.com/yeagerai/status/1646194523242995713)

- プロンプトでAgentを作ってしまうということ？

### [2023-04-13 LangChainをGUIで扱えるFlowiseAIがリリース](https://twitter.com/FlowiseAI/status/1646176565691023360)

- LangFlowより高機能なのかな？

### [2023-04-13 Alpacaフォーマットの日本語データセットが CC BY-SA 3.0で公開](https://huggingface.co/datasets/kunishou/databricks-dolly-15k-ja)

- 商用利用も可能なAlpacaのデータセット
- これを元にしたLLMが今後活発になるのでは

### [2023-04-12 CAMEL: エージェント同士を会話させる論文の実験をLangChainで実現する方法](https://twitter.com/hwchase17/status/1645834030519296000)

- 元論文は3/31に出ている以下
  - [https://arxiv.org/abs/2303.17760](https://arxiv.org/abs/2303.17760)

### [2023-04-12 ColabでCerebras-GPTを試す](https://note.com/npaka/n/n82f74e62c30f)

- 日本語はダメそう

### [2023-04-12 LlamaIndexでPinconeを使って疎と密のハイブリットな検索を試す](https://note.com/npaka/n/n63afe0e6684a)

- devioの記事と疎密の意味が少し違いそう？要確認。

### [2023-04-11 LlamaIndexの検証機能 ResponseとSourceをGPT-4に評価させて正しいかを判断する](https://twitter.com/jerryjliu0/status/1645451897372024832)

- 以下のコード例によればGPT-4に検証させている様子（つまりGPT-4のAPIが使えない場合は使えない機能）
  - https://github.com/jerryjliu/llama_index/blob/main/examples/evaluation/TestNYC-Evaluation-Query.ipynb

### [2023-04-11 LangChainとsupabaseを組み合わせるexample](https://blog.langchain.dev/langchain-x-supabase/)

- テンプレートを見てみないと詳細はわからぬ。

### [2023-04-11 LlamaIndex でSQL生成を試す](https://note.com/hmj_kd/n/n24c8e2858e96)

- スキーマからSQLを生成している面白い事例

### [2023-04-11 LLMを使ったアプリケーションを作る際のエンジニアリングのポイント](https://huyenchip.com/2023/04/11/llm-engineering.html)

- LLMの非決定性にどう対処するか
- プロンプトエンジニアリングとその自動化
- 推論時にトークン数が多く消費される
- その他、LLMを活用したツールについてなど

### [2023-04-11 Passregi CVの現在と取り組んできた改良](https://dev.classmethod.jp/articles/developers-io-day-one-passregi-cv-improvements/)

### [2023-04-10 SparseFormer: 人間の視覚認識に基づいたスパースなプロセスへの挑戦](https://twitter.com/_akhaliq/status/1645278535878049792)

- 現在の視覚ネットワークの多くは、画素やパッチなどの視覚単位を一律に処理する密なパラダイムに従っている
- これを人間の疎な視覚認識をエンドツーエンドで模倣する手法
- 計算コストの大幅な削減が可能
- コードは1,2か月後らしい…

### [2023-04-10 Pandas 2のバックエンドについて](https://blog.amedama.jp/entry/pandas2-dtype-backend)

- NumPyバックエンドだと、Pandas 1と同じ動作となる
- バックエンドを変えることで、整数型の欠損値を表現できるようになっている点は大きいかも

### [2023-04-10 GPT関連の参考になるアプリケーション](https://qiita.com/sonesuke/items/03c979177adccb7758f2)

- アーキテクチャが整理されててよい。
- ライブラリの活用方法で悩んだら見ると良いかも。

### [2023-04-10 GPT関連のOSSライブラリまとめ](https://qiita.com/sonesuke/items/56a6e4b6532eafa104f4)

- 開発前に一読すれば良いかも。
- 実装自体を見てみると参考になる部分も多い。
- Semantic Kernelは良く知らなかったがMicrosoft製なので気になっている。
  - [2023-03-18 Microsoft が LLM をアプリ開発に統合するための OSS「Semantic Kernel」を発表 - Qiita](https://qiita.com/nohanaga/items/430b59209b02c298ef2a)
- HuggingGPTもMicrosoft製なんだな。

### [2023-04-09 LlamaIndexでクエリに回答したリファレンスを取得する方法](https://dev.classmethod.jp/articles/get-reference-in-query-of-llamaindex/)

- file_metadataを使うことで、node.node.extra_infoにファイル名をもたせることができる。
- リファレンスの情報はレスポンスのsource_nodesに含まれる

### [2023-04-08 GPTをドーピングする LangChain 基礎編](https://zenn.dev/takiko/articles/24217eece242e1)

- TypeScriptでLangChainをする網羅的な内容
- Python使いでも概要をおさえるのは良さそう

### [2023-03-30 Evolving Zoom IQ, our AI smart companion, with new features and a collaboration with OpenAI](https://blog.zoom.us/zoom-iq-smart-companion/)

- zoomがリアルタイムでミーティング内容をまとめて、遅れてきた人にサマリー表示して、質問にも答えてくれるらしい。

### [2023-03-28 大規模言語モデルの驚異と脅威 - Speaker Deck](https://speakerdeck.com/chokkan/20230327_riken_llm)

- まとめ記事を書く際には参考になりそうなひとつ。
- 個人的に新しい情報はなさそう。

### [2023-03-28 pytorch2 + ROCm で RWKV(LLM Chatbot) と Wisper 動作確認メモ](https://zenn.dev/syoyo/articles/12c649cfa34ea0)

- ROCmが良く分からんけどAMD GPUで動かす仕組みかな

### [2023-03-26 大規模言語モデルで変わるMLシステム開発](https://speakerdeck.com/hirosatogamo/da-gui-mo-yan-yu-moderudebian-warumlsisutemukai-fa)

- Microsoft SAの解説記事
- プロンプトの話も結構含まれる

### [2023-03-22 Sparks of Artificial General Intelligence: Early experiments with GPT-4](https://arxiv.org/abs/2303.12712)

- Microsoft ResearchによるGPT-4を調査した論文
- 150ページにも及ぶため読めていない

### [2023-03-19 NAVERがGPT-3と商品検索を組み合わせた論文](https://twitter.com/sz_dr/status/1637460944707289088)

- コンテキスト保持の仕組みの参考になると考えられる

### [2023-03-11 ChatGPTクローンをFastAPI・WebSocket・LangChain・Reactで](https://zenn.dev/ktechb/articles/chatgpt-clone-stream)

- 普通にバックエンドフロントエンドは参考になるやも
- 記憶には、LangChainのPromptTemplateを使っている

### [2023-03-11 Slack上でOpenAI社のWhisper APIで文字書き起こしするSlackBot作成](https://qiita.com/ina111/items/1a7c3aac1ca02259783f)

- slack_boltを使っている
- 実装の多少参考にはなるはず。

### [2023-03-10 GPTが出した回答の確からしさを見えるようにしてみる](https://acro-engineer.hatenablog.com/entry/2023/03/10/100000)

- NLIタスク、前提文と仮説文が与えられたときに、仮説文が前提文に対して、以下のいずれかの関係であることを推論するタスクで検証

### [2023-03-09 OpenAI 言語モデルごとのエンコーディング一覧](https://zenn.dev/microsoft/articles/3438cf410cc0b5)

- エンコーディングというかトークナイザの話といった方が誤解が無さそう。
- とりあえずほとんどの最新のやつはcl100k_baseを使っている。

### [2023-03-08 ChatGPT APIとFaissを使って長い文章から質問応答する仕組み](https://qiita.com/sakasegawa/items/16714fa132e874cab069)

- sakasegawa氏
- LlamaIndexを使わずにスクラッチで仕組みを考える場合には良いかも。

### [2023-03-06 ChatGPTとMakeを使ってGmailの返信を自動化してみる](https://qiita.com/sakasegawa/items/d8fb1889cdc77d050c01)

- sakasegawa氏
- Makeはいわゆるmakeではなくてインテグレーションするツールの話

### [2023-03-04 Google の FLAN-20B with UL2 を動かしてChatGPT APIのように使ってみる！](https://qiita.com/sakasegawa/items/7394fe68eb0087b3c4a5)

- sakasegawa氏
- デカ言語モデルが手元で動く。A100を使う必要がある。
- 日本語対応していないため、FuguMTで翻訳している。

### [2023-02-23 LangChainのAgentがどのようにToolを選択しているかを確認したメモ](https://www.inoue-kobo.com/ai_ml/langchain-agent/)

- descritionsが重要という点がポイントか

### [2023-02-23 TransformerやAttentionの分かりにくい点についてのメモ](https://blog.statsbeginner.net/entry/2023/02/23/174435)

- これはさすがに今更なのでええやろう

### [2023-02-16 BigQueryの主キー/外部キー制約はJoin Eliminationには使われない](https://qiita.com/abe_masanori/items/c19cf240fa3eaeeff44c)

- 実際にデータのチェックが行われるわけではない
- データのチェックが行われないのであれば主キー/外部キー制約を付与する理由は何なのかというと、一般の DBMS ではオプティマイザが実行計画を最適化する際に利用される
- その最適化の手法の一つに不要な結合処理をスキップする Join Elimination という手法があり、そちらに利用される

### [2023-02-24 PythonでTableau風 BIツールによる視覚的データ探索をやってみよう 〜PyGWalker〜](https://qiita.com/hima2b4/items/dfdfb77cf3a588f4131a)

- BIツールみたいなことをPythonでやる

### [2022-12-12 話題爆発中のAI「ChatGPT」の仕組みにせまる！](https://qiita.com/omiita/items/c355bc4c26eca2817324)

- こちらも詳しい

### [2022-12-06 ChatGPTはどのように学習を行なっているのか](https://zenn.dev/ttya16/articles/chatgpt20221205)

- ChatGPT限定の結構詳しい記事

### [2022-12-05 音声認識モデル Whisper の推論をほぼ倍速に高速化した話](https://qiita.com/halhorn/items/d2672eee452ba5eb6241)

- API版ですら1時間のデータに少し時間がかかるので、課題になる場合はここら辺を見る必要がある。

### [2022-06-09 NN時代のモダンな不均衡データ補正](https://tjo.hatenablog.com/entry/2022/06/09/120000)

- 均衡にしたデータセットで学習して、その後全データセットでチューニングし直す方法があるみたい。
- 界隈ではtwo-phase trainingと呼ばれている
- 題材は、画像データに対する不均衡データに限定されているのかも

### [2019-12-01 Captumを試す](https://qiita.com/gorogoroyasu/items/819ce2613e72ac96d588)

- 機械学習モデルを解釈し、理解するための手法をまとめたライブラリ
- SHAPやGradCAMの話と思えばいい、その他の手法も多くある