# LLM : 開発

### [2023-03-16 自動でプロンプトを作成するプロンプトエンジニアリング](https://twitter.com/awakia/status/1636130484756570112)

- エンジニアにはあまり意味がないかもな。

### [2023-03-26 大規模言語モデルで変わるMLシステム開発](https://speakerdeck.com/hirosatogamo/da-gui-mo-yan-yu-moderudebian-warumlsisutemukai-fa)

- Microsoft SAの解説記事
- プロンプトの話も結構含まれる

### [2023-03-28 大規模言語モデルの驚異と脅威 - Speaker Deck](https://speakerdeck.com/chokkan/20230327_riken_llm)

- まとめ記事を書く際には参考になりそうなひとつ。
- 個人的に新しい情報はなさそう。

### [2023-04-10 GPT関連のOSSライブラリまとめ](https://qiita.com/sonesuke/items/56a6e4b6532eafa104f4)

- 開発前に一読すれば良いかも。
- 実装自体を見てみると参考になる部分も多い。
- Semantic Kernelは良く知らなかったがMicrosoft製なので気になっている。
  - [2023-03-18 Microsoft が LLM をアプリ開発に統合するための OSS「Semantic Kernel」を発表 - Qiita](https://qiita.com/nohanaga/items/430b59209b02c298ef2a)
- HuggingGPTもMicrosoft製なんだな。

### [2023-04-10 ChatGPTの機会と脅威](https://www.docswell.com/s/ku-suke/KNRR6P-chatgpt-enterprise)

- かなりまとまっていてて活用方針の参考となる
- Azure OpenAIってGPT-3.5のfine-tuneできるんやっけ？？とはなっている
- 研究用ととはいえ商用利用不可なので、たぶん企業の研究は無理では…

### [2023-04-10 【誰でも簡単ChatGPT、GPT-4 利用】Azure OpenAI Serviceを使ってみた with LINE Bot【Azureでより安心・安全にAI機能が使える】 - Qiita](https://qiita.com/mochan_tk/items/8b64cf4ca713250030a4)

### [2023-04-11 day1のChatGPT会のレポート](https://dev.classmethod.jp/articles/report-developersio-day1-chatgpt-beginning/)

### [2023-04-11 LLMを使ったアプリケーションを作る際のエンジニアリングのポイント](https://huyenchip.com/2023/04/11/llm-engineering.html)

- LLMの非決定性にどう対処するか
- プロンプトエンジニアリングとその自動化
- 推論時にトークン数が多く消費される
- その他、LLMを活用したツールについてなど

### [2023-04-12 クックパッドの toB 向け事業における ChatGPT API の活用事例紹介 - クックパッド開発者ブログ](https://techlife.cookpad.com/entry/2023/04/12/142744)

### [2023-04-15 LLMOpsに有益なツール群のまとめ](https://twitter.com/nepinepimate3/status/1647136562105454592)

- LLMというか範囲が広すぎるのであんま意味ないかも
- たぶんまったく使う用途の無いものも含まれている

- Microsoft SAの記事のアップデート版かな？

### [2023-04-16 ChatGPTやBigChatの活用ヒントまとめ](https://twitter.com/developer_quant/status/1647447763838468097)

### [2023-04-21 0421DS協会_ChatGPTによって描かれる未来とAI開発の変遷.pdf](https://speakerdeck.com/hirosatogamo/0421dsxie-hui-chatgptniyotutemiao-kareruwei-lai-toaikai-fa-nobian-qian)

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

### [2023-04-30 【2024年版】ChatGPT APIを社内利用する時に採用すべきアーキテクチャを考えた - Qiita](https://qiita.com/yuno_miyako/items/ce80002adf76bd321ad3)

### [2023-05-01 ローカルLLM の対話で使われてるプロンプト書式まとめ (npakaさん)](https://note.com/npaka/n/n2e2cf5a458ac)

### [2023-05-06 Andrew Ngさんの開発者のためのプロンプトエンジニアリングの要点](https://note.com/mahlab/n/n96c84a441b4d)

- 組み込む際のご参考に
- こちらにもまとめられていた
  - [開発者のためのチャットGPTプロンプトエンジニアリング講座が公開されていたので眺めてみた - Qiita](https://qiita.com/mihoicchi/items/a7d04d6b2b3bfbc96e72)
- 色々あって泣けてくる

### [2023-05-11 生成AI周回遅れキャッチアップ勉強会！ - Speaker Deck](https://speakerdeck.com/minorun365/sheng-cheng-aizhou-hui-chi-rekiyatutiatuhumian-qiang-hui)

- ChatGPT Browsing Pluginは知らなかったな
- Chain of ThoughtやFew-shotなどのプロンプトエンジニアリング用語覚えられない

### [2023-05-14 CTOの視点から見たAzure OpenAI ServiceとOpenAIのChatGPT APIの深堀り比較 - Qiita](https://qiita.com/lazy-kz/items/32e8e7c86bdce67beb48)

- 結論、最新モデルかどうか意外はAzure OpenAI一択な気がする。

### [2023-05-14 FLAIR: オンラインで会話型ボットを検出するためのフレームワーク](https://elith.substack.com/i/121117725/論文)

- 人間とボットを効果的に区別するための質問シナリオ
  - 人間にとっては簡単だがボットにとっては難しいもの
  - ボットにとっては簡単だが人間にとっては難しいもの
- LLMの弱点
  - 文字のカウント、文字の置換、文字の配置
  - ランダム編集、ノイズ侵害
  - ASCIIアート
- LLMが得意なもの
  - 記憶、計算の一部
- 元論文
  - [[2305.06424] Bot or Human? Detecting ChatGPT Imposters with A Single Question](https://arxiv.org/abs/2305.06424)

### [2023-05-15 日本初の挑戦〜食べログによるChatGPTプラグイン開発の舞台裏](https://tech-blog.tabelog.com/entry/first-challenge-tabelog-chatgpt-plugin-devleopment)

- 技術的な話はあまりなかったが、脆弱性診断とかやるのはすごい。
- コンテキストを与えるとかはやってないのかも？キーワード検索をChatGPTでラッパした感じかもしれない

### [2023-05-18 0518LLMmeetup_LLMシステムの非機能要件対応_現場レポート.pdf - Speaker Deck](https://speakerdeck.com/hirosatogamo/0518llmmeetup-llmsisutemunofei-ji-neng-yao-jian-dui-ying-xian-chang-repoto)

よかった。認証の流れ、閉域化されたAzureでのアーキテクチャの例などが書いてある。

### [2023-05-19 大規模言語モデルの開発者が知っておくと役立つさまざまな数字](https://gigazine.net/news/20230519-llm-numbers/)

- GPT-3.5と4のコスト比、エンベッディングのコスト、セルフホストする際に使用できそうなSentenceTransformersなど有用な情報がある

### [2023-05-21 第1回 LLM 勉強会 - NII(国立情報学研究所)](http://llm-jp.nii.ac.jp/llm/2023/05/21/first-study-group.html)

- 特に以下の資料が正しくまとまっており有用
  - [Recent_LLMs.pptx - Google スライド](https://docs.google.com/presentation/d/178Nk6flxqS59E2J9SSj5ZhyZ8YD_3tWJ/edit#slide=id.p1)
- 言及されているが各モデルのライセンスのまとめ
  - [Mooler0410/LLMsPracticalGuide: A curated list of practical guide resources of LLMs (LLMs Tree, Examples, Papers)](https://github.com/Mooler0410/LLMsPracticalGuide#Usage-and-Restrictions)

### [2023-05-22 OpenCALM, Rinna, GPT-3.5の比較](https://elith.substack.com/i/122600758/調査)

- チャット用に調整したらもうちょいマシになるのかな

### [2023-05-23 ChatGPTを使い始める前に理解しておく情報や用語など | DevelopersIO](https://dev.classmethod.jp/articles/pre-chatgpt/)

### [2013-05-27 StackLLaMA : RLHFでLLaMAを学習するための実践ガイド｜npaka](https://note.com/npaka/n/n1248a4202df0)

- Hugging Faceの以下記事のまとめ
  - [StackLLaMA: A hands-on guide to train LLaMA with RLHF](https://huggingface.co/blog/stackllama)

### [2023-05-29 PEARL: 大規模言語モデルによる長文文書に対するタスクの改善](https://elith.substack.com/i/124082742/論文)

- 戦略として、中間ステップに分解することで入力例を改善する「PEARL」というフレームワークを提案
- PEARLは、ゼロショット とchain-of-thought promptingを上回る
- 中間ステップは以下の３つで構成
  - アクションマイニング：要約、検索など
  - プラン生成：アクションの実行するプラン
  - プラン実行：2で生成したプランを実際に実行する
- 元論文
  - [https://arxiv.org/pdf/2305.14564.pdf](https://arxiv.org/pdf/2305.14564.pdf)

### [2023-06-01 歴代チャットボットと最近のLLMのまとめ - Qiita](https://qiita.com/Ted-HM/items/192746b547547eb070da)

- 最近のものまでまとめてあるのは評価できるが、ざっくりすぎる＋多少論点がずれているものもあるので参考程度

### [2023-06-01 生成系AI/LLM に関する 注目アップデート ~MS Build 2023 編~ - Speaker Deck](https://speakerdeck.com/yujioshima/llm-niguan-suru-zhu-mu-atupudeto-ms-build-2023-bian)

- こちら社内文書に基づくChatBotの作成に有用そうでした。
- MS Build 2023のまとめから始まり、Cognitive Search + LLMでRetrieval Augmented Generationを実現する方法、
- 実際にメルカリ社内での活用方法の紹介があります。
- 個人的にクエリとドキュメントは類似性があるか疑問に思っており、
- そこも最後の活用方法でTwo tower modelで解決しているところが面白かったです。
- Two tower modelはVertex AI Matching Engineでも実現できそう
  - [Two-Tower ModelでEmbeddingsを作成してMatching Engineで法人名寄せを試す（前半）｜Koji Iino](https://note.com/lizefield/n/n67eb32d2c1a4)

### [2023-06-03 QLoRA: メモリの消費量を激減させつつ少ないデータでトレーニングできる手法](https://gigazine.net/news/20230603-qlora-finetuning-llm/)

- LoRAでは、元のモデルのパラメーター行列を低ランク近似した新たな行列をトレーニング対象にすることで、トレーニングに必要なメモリの消費量を削減
  - [[2106.09685] LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)
- このLoRAをベースに、追加で3つのテクニックを利用することで650億(65B)パラメーターのモデルを48GBしかメモリを搭載していないGPUでトレーニング可能に
- 学習も24時間のトレーニングでChatGPTの99.3%に匹敵する性能を引き出すことに成功
- ３つのテクニック
  - NF4での量子化 : QLoRAでは4bitで量子化を行う
  - 二重量子化 : 量子化の際に用いる定数についても量子化を行う
  - ページ最適化 : GPUメモリが上限に達した際に、通常のメモリへとデータを退避させて計算に必要なメモリを確保（ピークの使用率を抑える）

### [2023-06-03 24GB GPU で 20B LLM の RLHF ファインチューニング｜npaka](https://note.com/npaka/n/nff4091ea33ce)

- 以下の3月の記事の解説
  - [【Hugging Face】24GBのコンシューマ向けGPUで20BilionのLLMをファインチューニングする方法](https://huggingface.co/blog/trl-peft)

### [2023-06-05 AWSでLLMを学習するサンプルが公開](https://twitter.com/icoxfog417/status/1665687806176534528)

### [2023-06-09 Retrieval Augmented Generationを改良する2つの方法 | DevelopersIO](https://dev.classmethod.jp/articles/revise-retrieval-augmented-generation/)

- 単純なRAGの問題点を挙げて、解決策のChat/Askを解説している良記事
- LlamaIndexの課題やLangChainを使うべきという話も分かる気がする

### [2023-06-10 Azure OpenAI Service の クォータ管理](https://zenn.dev/microsoft/articles/be24a299f46a4d)

- Tokens Per Minute (TPM) のクォータを、各デプロイに対してユーザー任意の値 (1K 単位) で割り当てることができるように

### [2023-06-14 「ChatGPTについて調べてくれ」と社長から特命を受けた人のためのChatGPT概論(40min版)_v1.00.pdf - Speaker Deck](https://speakerdeck.com/doradora09/20230614-chatgptnituitediao-hetekure-toshe-chang-karate-ming-woshou-ketaren-notamenochatgptgai-lun-40minban-v1-dot-00)

### [2023-07-11 ベクトル検索で「以外」や「数字の大小」を試してみた | DevelopersIO](https://dev.classmethod.jp/articles/vector-search-except-and-numerical-big-small/)

- 有用記事。Embeddingsについては考察の余地があるな。