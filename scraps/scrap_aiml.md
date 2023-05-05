# AIML

### [2023-05-04 CLIP ViT-L/14がリリース (Hugging Face)](https://huggingface.co/laion/CLIP-ViT-L-14-DataComp.XL-s13B-b90K)

- ImageNetで79.2%のゼロショット精度を実現したCLIP ViT-L/14がリリース
- CLIPを大きく上回り、LAION-2Bで学習させた大型モデル（ViT-g/14）を凌駕

### [2023-05-04 StarCoder: コード生成用の最先端のLLM (Hugging Face)](https://huggingface.co/blog/starcoder)

- ベンチマークでは、OpenAIのcode-cushman-001 (12B)モデルも凌駕している
- VSCodeの拡張機能「HF Code Autocomplete」として使える（APIキーとかは必要そう）
  - [HF Code Autocomplete - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=HuggingFace.huggingface-vscode)

### [2023-05-04 MaMMUT: マルチモーダルのための新しい基盤モデルアーキテクチャの研究 (Google Research)](https://ai.googleblog.com/2023/05/mammut-simple-vision-encoder-text.html)

- 視覚言語基盤モデルは、一般的にはCLIPなどに代表される対照学習と次トークン予測の２つの主要なシナリオが一般的
- 前者と後者で得意な下流タスクがことなるため課題
- MaMMUTはこれを解決するアーキテクチャとなっており、更に先行研究よりも多くの画像フレームを扱えるため、動画処理にもメリットがある
- 要するにImage側のエンコーダ結果をテキスト側のデコーダのCross Attentionとして使うところがポイントっぽい

### [2023-05-03 SpikeGPT: より軽量な環境で動かすことが可能な言語モデルの可能性](https://zenn.dev/octu0/scraps/0078b6e9925674)

### [2023-05-03 BigQueryのテーブルクローン機能がGA (Google Cloud)](https://cloud.google.com/bigquery/docs/release-notes#May_03_2023)

### [2023-05-03 LLMの独自コンテキスト拡張(RAG)にKendraを使用する例の紹介 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/quickly-build-high-accuracy-generative-ai-applications-on-enterprise-data-using-amazon-kendra-langchain-and-large-language-models/)

### [2023-05-03 Gravitonプロセッサに対するPyTorch 2.0の推論性能の最適化を実現 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/optimized-pytorch-2-0-inference-with-aws-graviton-processors/)

### [2023-05-01 長文から論点を抽出して、その論点を軸に文章の要約を試みる](https://note.com/mahlab/n/ndce1a18681e8)

- 手順は以下
  - CharacterTextSplitterで300字のチャンクに分割
  - チャンク毎にtext-embedding-ada-002で埋め込みベクトルを生成
  - Faissを使いk-means法でクラスタ数を5としてクラスタに分ける
  - 各クラスタ毎にload_summarize_chainで要約する
  - 各クラスタにLLMでタイトルをつけてもらう
- 割と要約の選択肢として良いのかも。

### [2023-05-03 OpenLLaMA : LLaMAのApache-2.0実装が動き始めている](https://twitter.com/haoliuhl/status/1653460937897295873)

- 各所の反応
  - [https://twitter.com/manjiroukeigo/status/1653543983325515776](https://twitter.com/manjiroukeigo/status/1653543983325515776)
  - [https://twitter.com/umiyuki_ai/status/1653506794503942148](https://twitter.com/umiyuki_ai/status/1653506794503942148)
  - [https://twitter.com/_kaiinui/status/1653498780501807105](https://twitter.com/_kaiinui/status/1653498780501807105)

### [2023-05-03 SAM + ResNet(fine-tuning) + ChatGPTで冷蔵庫の具材からレシピ推薦](https://dev.classmethod.jp/articles/chatgpt-recomend-recip)

- SAMのイメージがまだわかないな。

### [2023-05-01 GPT-3でZennの使い方を回答できる問い合わせシステムを作ってみた](https://dev.classmethod.jp/articles/zenn-chat-with-gpt3)

- LLamaIndexとか使わずにやる例となっており、Pineconeに対してベクトル検索している

### 2023-04-30 Semantic Kernel についての記事がいくつか

- [Semantic Kernel のサンプル概要](https://zenn.dev/hiromu/articles/20230430_semantikkernel)
- [Azure OpenAI Service を便利に使うための Semantic Kernel を試してみよう on C#](https://zenn.dev/microsoft/articles/semantic-kernel-1)
- [Semantic Kernel のスキルを外部ファイルで定義して読み込む](https://zenn.dev/microsoft/articles/semantic-kernel-2)

### [2023-04-29 Stability AIからDeepFloyd IFが公開](https://note.com/te_ftef/n/nd83eb09a3990)

- と思ったらこの記事はベースとなっているImagenの記事
- DeepFloydは学習元丸パクりのAI画像が作れると話題になってる模様

### [2023-04-29 LlamaIndex 0.6.0 - データに対する新しいクエリインターフェイス｜npaka｜note](https://note.com/npaka/n/n4254fc549dc0)

- 大きめの変更が加えられており、APIが整理されている
- queryなどの使い方の違い、indexはビューに過ぎない点などが特徴か

### [2023-04-28 音声合成に使用可能な事前学習モデルHuBERTをApache-2.0ライセンスで公開](https://twitter.com/yasyune1023/status/1651893684521287682)

### [2023-04-28 RWVK v10 14bが公開](https://twitter.com/meteor_eternal/status/1651716023605919744)

- これが商用利用可能なOSSの頼みの綱やで。ホンマに。

### [2023-04-28 生成AIの利用ガイドラインを作成するための手引き](https://storialaw.jp/blog/9414)

- 入力データの著作権や個人情報、自社機密情報、生成物などのついての手引きが記載
- 個人情報の議論について
  - 本記事の結論としては、OpenAI社とDPAを締結すれば、OpenAIのAPIを利用する場合には、個人データを入力するに際して本人の同意は必要ないとしている。
- 自社の機密情報について
  - いまのところ、サービス提供者の秘密保持義務について明記した条文はないため、秘密管理性を満たすかは解釈上明確ではなく、自社の情報を入力すべきではないとしている。
- 生成物について
  - 得られる結果の著作権について
    - 基本的な使い方では、著作物の利用は原則として依拠性がない（著作権侵害には該当しない）と考えられる
    - ただし、意図的に似た出力を得ようとプロンプトを調整したりする場合は、依拠性が肯定されると考えられる
    - 企業におけるリスク軽減という観点からは、そういった利用を禁止する旨を明記する
  - プロンプトの著作権も、創作性があれば「プログラムの著作物」として保護されるため注意が必要
  - また、生成物の商用利用について、OpenAIの場合は、生成物に関する権利についても全てユーザに移転する旨が規定されていますので、生成物の利用についての制限はない。

### [2023-04-28 Stability.aiがStableVicunaを発表](https://ja.stability.ai/blog/stablevicuna-open-source-rlhf-chatbot)

- Vicuna系ということはLLaMA系なので商用利用不可

### [2023-04-27 Pineconeのデータ管理についてのプラクティス](https://dev.classmethod.jp/articles/pinecone-data-management-practice/)

- 長いテキストは分割せざるを得ないので、出所が同じものはmetadataで工夫しましょうという話

### [2023-04-27 vicuna-13bのデータセットについて](https://twitter.com/npaka123/status/1651435773298880518)

- CarperAI/vicuna-13b-fine-tuned-rlhfや報酬モデルで使われるデータセットが整理されている

### [2023-04-27 Hugging Face Transformersを使いTensrFlowとTPUを言語モデルの学習方法](https://huggingface.co/blog/tf_tpu)

### [2023-04-26 vicuna-13bで embedding vectorの計算 (& GPT･RWKVとの比較)｜Kan Hatakeyama｜note](https://note.com/kan_hatakeyama/n/n2fbd81ac1d45)

- 埋め込みを別ライブラリで実施する記事としては参考となる
- 比較結果自体は、評価が主観であり、モデル規模もアンフェアな条件なので参考程度

### [2023-04-26 OpenAIのブランドガイドラインが公開された](https://dev.classmethod.jp/articles/about-openai-brand-guidelines/)

- 明記する必要のあることがいくつかありそう
- マークについても言及がある

### [2023-04-26 Harnessing the Power of LLMs in Practice: A Survey on ChatGPT and Beyond](https://www.researchgate.net/publication/370224758_Harnessing_the_Power_of_LLMs_in_Practice_A_Survey_on_ChatGPT_and_Beyond)

- GitHubで必要な論文などの情報がまとめられている
  - [https://github.com/Mooler0410/LLMsPracticalGuide](https://github.com/Mooler0410/LLMsPracticalGuide)
- 正攻法で学術的なまとめで、LangChainやLlamaIndexなどについては特に言及がない

### [2023-04-25 ChatGPTのWeb版がオプトアウトをより簡易に提供](https://openai.com/blog/new-ways-to-manage-your-data-in-chatgpt)

- 30日保存はAPIと同様なので注意。
- 不正使用を監視するために必要な場合に使われるとのこと。
- また、ChatGPT Businessもアナウンスされているが、単純にデフォルトでオプトアウトという形らしい。
- 弊社ブログ
  - [https://dev.classmethod.jp/articles/chatgpt-web-chat-history-off/](https://dev.classmethod.jp/articles/chatgpt-web-chat-history-off/)

### [2023-04-25 Google Research : 多項式複雑度でNASを実現するLayerNAS](https://ai.googleblog.com/2023/04/layernas-neural-architecture-search-in.html)

- 探索すべきモデル候補の数が1桁減少し、計算量や最終的な性能がより良いモデルアーキテクチャを発見することが可能

### [2023-04-24 GPT4Toolsの公開](https://gpt4tools.github.io/)

- Toolsに画像処理をいくつかいれてあり、それをユーザのクエリから選ぶ感じで対話的に画像処理をするツール
- 前の出力を次の入力とすることができるので、編集を対話的に実施できる感じみたい

### [2023-04-24 vicuna-13bは日本語でも結構性能いいらしい](https://twitter.com/nucode/status/1650354319323979778)

- 一般のご家庭のGPUマシンでも動作する

### [2023-04-24 Scaling Transformer to 1M tokens and beyond with RMT](https://arxiv.org/abs/2304.11062)

- 200万トークンの処理が可能にスケーリングするモデルについての論文
- Recurrent Memory Transformerという昨年の論文に基づいている
  - [https://arxiv.org/abs/2207.06881](https://arxiv.org/abs/2207.06881)
- 絵だけみる感じたと階層的にやる感じなのかなー、比較的ロースペック(1080Ti)で実験しているので検証はし易そうだがコードがない
- この動画で話題になっている
  - [https://www.youtube.com/watch?v=0404XdXnUvU](https://www.youtube.com/watch?v=0404XdXnUvU)

### [2023-04-24 大規模言語モデルのための強化学習｜npaka｜note](https://note.com/npaka/n/ne6d2e7e076ea)

- なぜ「強化学習」が「教師あり学習」よりも言語モデルの学習に適しているのか、考察した記事で面白い

### [2023-04-23 tiktokenでトークンについて掘り下げた記事](https://nikkie-ftnext.hatenablog.com/entry/how-chatgpt-tokenize-japanese-text-tackling-with-tiktoken)

- 1漢字（ユニコード）が２つのトークンに分割されているのは知らなかった
- 使われ方が似ている文字が近くの文字コードに来ているとは限らないから、これは少し斬新だなという感想

### [2023-04-23 次世代のRWKVモデルに使用する想定のマルチ言語トークナイザーが公開](https://twitter.com/forasteran/status/1649919025458323456)

- 日本語の例でも示されており今後に期待できる。

### [2023-04-22 LangChain 0.0.146でcompress retrieved documentをリリース](https://twitter.com/hwchase17/status/1649428295467905025)

- クエリする前にRetriver側の情報を、クエリに関連する情報に圧縮する。
- Retriver作成時に圧縮するわけでないことに注意
- 以下で試した記事がある
  - [LangChainの新機能Contextual Compression Retrieverを試す｜mah_lab / 西見 公宏｜note](https://note.com/mahlab/n/n7d72e83904cc)

### [2023-04-21 0421DS協会_ChatGPTによって描かれる未来とAI開発の変遷.pdf](https://speakerdeck.com/hirosatogamo/0421dsxie-hui-chatgptniyotutemiao-kareruwei-lai-toaikai-fa-nobian-qian)

- Microsoft SAの記事のアップデート版かな？

### [2023-04-21 Whisper JAX : Whisperを70倍高速化を観測](https://twitter.com/currypurin/status/1649402118699360258)

- 一時間の音声を15秒で書き起こす
- なおGPU, TPU駆動が前提

### [2023-04-21 Jpn10%のRWKVが観測](https://twitter.com/meteor_eternal/status/1649361381697929217)

- いままではOtherという形だったので、日本語に特化している点は期待できる

### [2023-04-20 Google Research : 長期な時系列予測のための研究正解TiDEモデルの紹介](https://ai.googleblog.com/2023/04/recent-advances-in-deep-long-horizon.html)

- 既存手法としてTransformer系のFEDformerやPatchTSTを例にしている
- TiDEはシンプルなMLPアーキテクチャがベースのEncoder-Decoderモデルとなっている
- 入力として過去の出力yやAttributes、特徴量xから構成される
- これらはGoogle CloudのVertex AutoML Forecastingで近々利用できるようになる予定

### [2023-04-20 Stability AIがLLMとなるStableLMを発表](https://github.com/Stability-AI/StableLM)

- AWSとの連携は期待が持てる。日本語対応が期待されるところ。
- OpenAssistantはさっそくStableLMに対応
  - [https://huggingface.co/OpenAssistant](https://huggingface.co/OpenAssistant)
- ファインチューニング済みモデルもいくつか公開されている
  - [https://twitter.com/haruto_qu/status/1648734352933818370](https://twitter.com/haruto_qu/status/1648734352933818370)
- 日本語も頑張ってくれるつもりみたい
  - [https://twitter.com/stabilityai_jp/status/1648709992281948160](https://twitter.com/stabilityai_jp/status/1648709992281948160)

### [2023-04-19 LangChainをRWKVで駆動する例](https://note.com/npaka/n/n130a57aa384a)

- まあまだまだこれからだな
- `from langchain.llms import RWKV`でlangchainから使えるのは楽やね
- 使用モデルは`RWKV-4-Raven-14B-v9-Eng99%-Other1%-20230412-ctx8192.pth`
- 私のブログでは`RWKV-4-Raven-14B-v8-EngAndMore-20230408-ctx4096.pth`を使ってて、Ravenのアップデートが速いな

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

### [2023-04-19 llama-indexがGoogle検索などの検索機能を追加](https://twitter.com/jerryjliu0/status/1648347966615465984)

- 以下が挙げられている
  - 📝 Note-taking capabilities
  - 🌐 Web Page search
  - 🔎 @google search capabilities

### [2023-04-19 GPT4All-JがGPTであるLLaMaを除去しApacheとなった](https://twitter.com/sonesuke/status/1648414463517949953)

- オープン化は急速に進んでいる

### [2023-04-19 CAFA 5 Protein Function Prediction](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction)

- アミノ酸配列からタンパク質の機能を予測するコンペ
- データが329MBと小さめなので参加しやすいかも
- 締めは2023-08-21

### [2023-04-19 特徴量エンジニアリングとFeature Storeを使ってほぼリアルタイムな特徴量による裏付けを分析](https://aws.amazon.com/jp/blogs/machine-learning/use-streaming-ingestion-with-amazon-sagemaker-feature-store-and-amazon-msk-to-make-ml-backed-decisions-in-near-real-time/)

- ストリーミングの取り込みはAmazon Managed Streaming for Apache Kafka (MSK)(Amazon MSK)を使用
- 事例としてはトランザクションに対する不正検知となっており、結構おもしろい

### [2023-04-18 JumpStartでドメインに適応したLLMをfine-tuningする事例](https://aws.amazon.com/jp/blogs/machine-learning/financial-text-generation-using-a-domain-adapted-fine-tuned-large-language-model-in-amazon-sagemaker-jumpstart/)

- モデルはLLM GPT-J 6Bを使用。

### [2023-04-18 日本でもGoogle Bardが利用可能に](https://qiita.com/MasaruYamazaki/items/a107d4455500420ffd5b)

- [Google の会話型 Generative AI である Bard が日本から利用可能になったので試してみました！ | DevelopersIO](https://dev.classmethod.jp/articles/bard-googles-generative-ai-is-now-available-in-japan/)

### [2023-04-18 VicunaがGPT-4のように画像を入力として処理できるように](https://twitter.com/tikgiau/status/1647767975804452864)

- MiniGPT-4とうたっており、Gradioを使ったデモも公開されている

### [2023-04-17 1次元の時系列をFFT等を使い2次元にmapするTimeNetを提案](https://arxiv.org/abs/2210.02186)

- 1次元時系列を複数の期間に基づく2次元テンソル集合に変換することで、時間変動の分析を2次元空間に拡張
- 短期・長期予測、インピュテーション、分類、異常検知など、5つの主要な時系列解析タスクにおいて一貫した最先端を達成
- 「FFT等」のところが論文読まないと分からないな

### [2023-04-17 llama_indexの公式がソースにクエリの答えが含まれているかを評価する方法を紹介](https://twitter.com/jerryjliu0/status/1647626532519841793)

- それぞれのソースとクエリを入力として、含まれるかどうかをYes,Noで答えさせることにより実現

### [2023-04-17 llama_indexの公式が単一のルータを使って使用するIndexを複数の中から選択する例の紹介](https://twitter.com/gpt_index/status/1647625929165008897)

- LangChainと同じようなアイディアで、多分各インデックスの説明文とクエリの比較により判断するものかと

### [2023-04-17 OSS版LLaMAみたいなRedPajamaプロジェクトが発表](https://github.com/togethercomputer/RedPajama-Data/)

- LLaMAトレーニングデータセット再現
- 今のところデータセットのみの話っぽい

### [2023-04-17 Meta AIが高性能なコンピュータビジョンモデルをトレーニングする新しい手法 DINOv2 を発表](https://ai.facebook.com/blog/dino-v2-computer-vision-self-supervised-learning/)

- ファインチューニング不要で、さまざまなコンピュータビジョンのタスクに活用可能
- 自己教師あり学習を採用。あらゆる画像の集合体から学習可能
- 深度推定など、現在の標準的なアプローチでは学習が難しいものも学習できる
- 続報解説がきている
  - [https://twitter.com/timdarcet/status/1649435730291093506](https://twitter.com/timdarcet/status/1649435730291093506)
- よくみると、NC-4.0なので非商用かー

### [2023-04-17 大規模言語モデルをデプロイするためのパイプライン、最適化について](https://aws.amazon.com/jp/blogs/machine-learning/deploy-large-models-at-high-performance-using-fastertransformer-on-amazon-sagemaker/)

- LMI DLC(Large Model Inference, Deep Learning Container)と呼ばれている
- モデルの圧縮や分割方法など網羅的に記載されているかも

### [2023-04-17 SageMaker Data Wrangleでnltkやscipyを使う事例](https://aws.amazon.com/jp/blogs/machine-learning/authoring-custom-transformations-in-amazon-sagemaker-data-wrangler-using-nltk-and-scipy/)

- カスタム変換でnltkやscipyを使うことができる

### [2023-04-17 Fraud Detectorの新機能であるコールドスタートを使用する例](https://aws.amazon.com/jp/blogs/machine-learning/overcome-the-machine-learning-cold-start-challenge-in-fraud-detection-using-amazon-fraud-detector/)

- わずか100イベント程度でリアルタイムの不正防止MLモデルを迅速にブートストラップできる

### [2023-04-17 SageMaker Collections : モデルレジストリのモデルを整理する新機能](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-collections-organize-model-registry/)

- 登録されたモデルのうち互いに関連するものをグループ化し、階層的に整理することが可能
### [2023-04-17 Inferentia2によるHuggng Face Transformersの高速化](https://huggingface.co/blog/accelerate-transformers-with-inferentia2)

- こちらはHugging Face側の記事
### [2023-04-17 低コストで高性能な生成系 AI 推論用の Amazon EC2 Inf2 インスタンスが一般公開](https://aws.amazon.com/jp/blogs/news/amazon-ec2-inf2-instances-for-low-cost-high-performance-generative-ai-inference-are-now-generally-available/)

- 日本語の公式ブログ記事
- 言語モデル以外でも、inf2.8xlargeやinf2.xlarge辺りは音声処理でもターゲットになるかもしれない。

### [2023-04-16 Nishikaの材料コンペの2nd place solution解説](https://qiita.com/mi-212/items/694124649d2848a6b559)

- GNNのアーキテクチャとしてNequIPを採用

### [2023-04-16 LangChain の チェーン・エージェントの評価](https://note.com/npaka/n/n7f7479bd3e19)

- こういった生成系の評価の悩みとそれの解決策が記載
- データの欠如についてはデータセットが記載されており、評価はLangChainの機能として評価用のツールやチェーンを紹介

### [2023-04-16 OpenAssistantの発表](https://twitter.com/omarsar0/status/1647339407173664772)

- みんなで作るInstructGPTという位置づけ
- リリースにはモデル、データセット、チャットインターフェイスが含まれている
- データセットOASST1をApache 2.0で公開している
  - [https://twitter.com/_philschmid/status/1647288182252228612](https://twitter.com/_philschmid/status/1647288182252228612)


### [2023-04-16 npakaさん : OpenAI APIのファインチューニングの学習データのガイドライン](https://note.com/npaka/n/n021a59452dc8)

- いずれ必要になるかもしれないファインチューニングの知識

### [2023-04-16 ChatGPTやBigChatの活用ヒントまとめ](https://twitter.com/developer_quant/status/1647447763838468097)

### [2023-04-15 LLMOpsに有益なツール群のまとめ](https://twitter.com/nepinepimate3/status/1647136562105454592)

- LLMというか範囲が広すぎるのであんま意味ないかも
- たぶんまったく使う用途の無いものも含まれている

### [2023-04-15 Streamlitで実装されたQAチェーンを評価するauto-evaluatorの紹介](https://blog.langchain.dev/auto-eval-of-question-answering-tasks/)

- OpenAIモデルだけでなく、RetrieverやEmbeddingに使うモデルも変更しながら評価が可能なツールとなっている

### [2023-04-14 Google Research : 自動微分を越えるアルゴリズム](https://ai.googleblog.com/2023/04/beyond-automatic-differentiation.html)

- 相変わらず先進的。
- 一応、AutoBoundとしてライブラリを公開しているらしい。

### [2023-04-14 ベクトルデータベース Pinecone の概念を整理する](https://dev.classmethod.jp/articles/pinecone-overview/)

- 密・疎・ハイブリットなど詳しく

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

### [2023-04-13 LLMを高速に学習できるDeepSpeed-ChatをMicrosoftが公開](https://zenn.dev/howdy39/articles/a4a6f07a95a023)

- OPT-13Bが7.5時間で$1,920（約25万円）単位とのこと

### [2023-04-13 Alpacaフォーマットの日本語データセットが CC BY-SA 3.0で公開](https://huggingface.co/datasets/kunishou/databricks-dolly-15k-ja)

- 商用利用も可能なAlpacaのデータセット
- これを元にしたLLMが今後活発になるのでは

### [2023-04-12 langchainでAzure OpenAI使ったり、AD認証しながらReAct構成するコード](https://twitter.com/hiro_gamo/status/1645819925787971584)

### [2023-04-12 商用利用可能なDolly 2.0がDatabricks社からリリース](https://gigazine.net/news/20230413-dolly-2-0-open-instruction-following-llm-for-commercial-use/)

- 公式
  - [https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm](https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm)

### [2023-04-12 CAMEL: エージェント同士を会話させる論文の実験をLangChainで実現する方法](https://twitter.com/hwchase17/status/1645834030519296000)

- 元論文は3/31に出ている以下
  - [https://arxiv.org/abs/2303.17760](https://arxiv.org/abs/2303.17760)

### [2023-04-12 MLOps のはじめかた - Speaker Deck](https://speakerdeck.com/asei/mlops-nohazimekata)

- Money Forward社のMLOpsの知見
- StepFunctionsやInferenciaがでてくる
- MLOpsだからと言って新しい技術を採用すると痛い目にあう（これは確かに）

### [2023-04-12 ChatGPT Retrieval Pluginをローカルで動かす事例](https://dev.classmethod.jp/articles/running-chatgpt-retrieval-plugin-api-locally/)


### [2023-04-12 ColabでCerebras-GPTを試す](https://note.com/npaka/n/n82f74e62c30f)

- 日本語はダメそう

### [2023-04-12 LlamaIndexでPinconeを使って疎と密のハイブリットな検索を試す](https://note.com/npaka/n/n63afe0e6684a)

- devioの記事と疎密の意味が少し違いそう？要確認。

### [2023-04-11 day1のChatGPT会のレポート](https://dev.classmethod.jp/articles/report-developersio-day1-chatgpt-beginning/)

### [2023-04-11 Kaggle: Image Matching Challenge 2023が開始](https://www.kaggle.com/competitions/image-matching-challenge-2023/overview/evaluation)

- 参照画像から対象画像の回転と並進を予測するコンペ
- 用途としては3D再構成に使うのが目的らしい

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

### [2023-04-10 ChatGPTの機会と脅威](https://www.docswell.com/s/ku-suke/KNRR6P-chatgpt-enterprise)

- かなりまとまっていてて活用方針の参考となる
- Azure OpenAIってGPT-3.5のfine-tuneできるんやっけ？？とはなっている
- 研究用ととはいえ商用利用不可なので、たぶん企業の研究は無理では…

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

### [2023-04-05 LLaMAをWeb対話データでチューニングしたKoala-13B](https://twitter.com/sakuragi_zero/status/1643308310807052288)

- Alpacaとかとの差が良く分からん…
- 公式
  - [https://bair.berkeley.edu/blog/2023/04/03/koala/](https://bair.berkeley.edu/blog/2023/04/03/koala/)
- LLaMA系なので商用利用はできない

### [2023-04-01 音源分離技術の基礎と動向](https://www.jstage.jst.go.jp/article/essfr/16/4/16_257/_pdf/-char/ja)

- 音源分離について日本語でまとめられている記事

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

### [2023-03-14 DocsBot AI を使ってみた](https://zenn.dev/howdy39/articles/a4a6f07a95a023)

- 任意のドキュメントを食わせて検索可能なSaaS
- 社内的にやりたいことと、似ている例

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

### [2023-03-08 日本のロボティクスに関する記事](https://www.nature.com/articles/d41586-023-00668-z)

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

### [2023-03-02 Dropout Reduces Underfitting](https://arxiv.org/abs/2303.01500)

- [https://twitter.com/shriver_light/status/1649395937457094657](https://twitter.com/shriver_light/status/1649395937457094657)
  - Dropoutが過学習だけでなく、学習初期の未学習にも効くことを発見
  - バッチ間の勾配分散を減らし、学習初期だけDropoutすると最終的なlossも削減可能
  - 学習後期だけ使うと汎化性能が向上するという研究

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

### [2023-02-03 自民党AIの進化と実装に関するプロジェクトチーム](https://note.com/akihisa_shiozaki/n/n4c126c27fd3d)

- 松尾さんとかの見解も資料として上がってて面白い
- がその思いとは裏腹に国産LLMを作る話にはならなかったらしい

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

### [2021-09-08 GPT-2のパラメータについての解説記事](https://zenn.dev/tyaahan/articles/a8d99900000002)

- 割ときちんと解説されていてよくわからずに使っている場合は読んでおいた方が良い


### [2019-12-01 Captumを試す](https://qiita.com/gorogoroyasu/items/819ce2613e72ac96d588)

- 機械学習モデルを解釈し、理解するための手法をまとめたライブラリ
- SHAPやGradCAMの話と思えばいい、その他の手法も多くある

