# ブログネタ帳

## re:Invent 2022

- DEI201 : The power of responsibility in AI/ML
- BOA322 : Build and deploy a live, ML-powered music genre classifier
- AIM206 : Integrate and derive insights from multi-modal health data
- BOA307 : Building well-architected serverless applications
- AIM339 : Store features across teams with Amazon Feature Store, featuring Zalando
- AIM322 : Accelerate data preparation with Amazon SageMaker Data Wrangler

## MLマネージドサービス再入門

- AWS
  - Comprehend
  - Rekognition
  - Translate
  - Lookout for Equipment
  - Fraud Detector
- Google Cloud
  - Document AI
  - Vertex AI Vision
  - Vertex AI Matching Engine
  - Vertex AI Feature Store Streaming ingestion

## アプデ

- [Google Cloud、小売業向けの新たな AI ツールを発表](https://cloud.google.com/blog/ja/products/ai-machine-learning/google-cloud-unveils-new-ai-tools-for-retailers/)
  - 新たな棚卸用 AI で小売業の商品供給力向上を支援（現在、全世界でプレビュー版を提供中）
    - Vertex AI Vision をベースに、商品認識とタグ認識の 2 つの ML モデルを搭載した棚卸 AIの提供
  - 小売業者向け Discovery AI ソリューションの新たな AI 機能（こちらはGA）
    - 買い物客がカテゴリを選択すると、ML を利用して小売業者の EC サイトで最適な商品の並び順を選択可能に
  - Retail Search ソリューションの機能を強化（こちらはGA）
    - パーソナライズされた検索および閲覧結果を実現
  - Recommendations AI の新しいアップグレード（こちらはGA）
    - 新たなページレベルでの最適化機能
    - 新たに追加した収益最適化機能
    - 新しい Buy-it-Again モデル : 顧客の買い物履歴を活用し、リピート購入の見込みに関するパーソナライズされたレコメンデーションを提供
- [【アプデ】Personalizeが新レシピ「Trending Now」を追加](https://aws.amazon.com/jp/about-aws/whats-new/2023/01/amazon-personalize-new-recipe-trending-now/)
  - トレンドアイテムを特定する頻度を定義することができ、30分、1時間、3時間、1日ごとにおすすめアイテムを更新するオプションが用意
  - 既存のカスタムデータセットグループにTrending Nowソリューションを作成
  - カスタムdsgに対応しているので、バッチにも対応しているはず
- [【アプデ】PersonalizeがIAMポリシーにおけるタグのサポートを発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/01/amazon-personalize-supports-tag-based-resource-authorization/)
  - タグに基づくアクセス制御などが可能に。案件で使えるかもしれない。
- [Document AI OCR解説に関する日本語記事がでている](https://cloud.google.com/blog/ja/products/ai-machine-learning/top-reasons-to-use-gcp-document-ai-ocr)
  - Textractと比較したいところ
- [【ブログ】Document AI OCRエンジンに3つの新機能を追加](https://cloud.google.com/blog/products/ai-machine-learning/top-reasons-to-use-gcp-document-ai-ocr/?hl=en)
  - Document AI最近元気だな。
- [【アプデ】TranslateでのネストされたS3フォルダに保存されたファイルの翻訳サポートを開始](https://aws.amazon.com/jp/about-aws/whats-new/2022/12/amazon-translate-support-files-stored-s3-nested-folders/)
  - 特に言うことはなさそう
- [【アプデ】Translateでのバッチ処理時にファイル毎に言語判定が可能に](https://aws.amazon.com/jp/about-aws/whats-new/2022/12/amazon-translate-language-detection-support-batch-translation/)
  - ソース言語指定なしで、混在したものの翻訳が可能になったっぽい。
  - 各ファイルの最初の1,000文字をサンプリングして支配的なソース言語を検出（ので最初が肝心）
  - Amazon Comprehendの言語検出APIを活用しているらしい。
- [【アプデ】Rekognition Labelsが600のラベルを追加、2000以上の既存ラベルの精度を向上](https://aws.amazon.com/jp/about-aws/whats-new/2022/12/amazon-rekognition-labels-improves-accuracy-existing-labels-video/)
  - その他、ラベルの結果を「エイリアス」や「カテゴリー」で整理する機能を追加し、結果のフィルタリングをサポート
- [【アプデ】Rekognition Content Moderationのモデルが改善し誤検出を大幅に低減](https://aws.amazon.com/jp/about-aws/whats-new/2022/12/amazon-rekognition-labels-improves-accuracy-existing-labels-video/)
  - Content Moderationは、不適切、不要、または不快な画像や動画を検出できるディープラーニングベースの機能
  - 今回、電子商取引、ソーシャルメディア、オンラインコミュニティのコンテンツの誤検出率を大幅に低減し、本当に安全ではないコンテンツの検出率を低下させることなく実現。
- [【アプデ】Document AI OCR ProcessorがデジタルPDFの埋め込みテキストの抽出に対応](https://cloud.google.com/release-notes#December_19_2022)
  - PDFに非デジタルテキストが含まれている場合、光学式OCRモデルへ自動フォールバック
  - Document AI OCR に高度なバージョニングサポート
- [【アプデ】Fraud DetectorでData Model Explorerを提供開始](https://aws.amazon.com/jp/about-aws/whats-new/2022/12/amazon-fraud-detector-data-models-explorer/)
  - お客様のビジネス目標に沿った不正検知MLモデルをトレーニングするために必要な、推奨されるデータのガイダンスを提供
- [【アプデ】Forecastでコールドスタート予測に対応する新しいアプローチが発表](https://aws.amazon.com/jp/about-aws/whats-new/2022/11/amazon-forecast-generates-predictions-products-historical-data-more-accurate/)
  - メタデータを使用して類似商品の情報からコールドスタートのものを予測する仕組み
- [【アプデ】Personalizeでイベント記録を用いたオンラインでの評価指標の計算が可能に](https://aws.amazon.com/jp/about-aws/whats-new/2022/11/amazon-personalize-enables-measure-impact-recommendations/)
  - レコメンデーションのクリック率（CTR）などの測定も可能に。
  - メトリックと計算する関数（合計またはカウント）を定義するだけで、Personalizeが計算を実行。
  - どこまで定義できるのか要確認ですな
  - 結果はCloudWatchまたはS3アカウントにレポートを送信
- [【アプデ】RekognitionでImageProperties機能のサポート](https://awsapichanges.info/archive/changes/b4d341-rekognition.html)
  - すでにブログ化はされている。
    - [Amazon Rekognition のラベル検出機能にドミナントカラーと画像品質の検出オプションが追加されました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-rekognition-detect-image-properties/)
- [【アプデ】Document AI Warehouse](https://cloud.google.com/release-notes#November_10_2022)
  - Document AIはTextractのようなテキスト抽出サービス。
  - Document AI Warehouseは、ドキュメントと抽出データの検索や保管、管理を一元的なプラットフォーム上で行える。
  - このWarehouse上での、テキスト抽出機能が有効になったという意味と考えられる。

## フレームワーク

- polar
  - [テーブルデータではcudfだけではなくpolarsというものも良いらしいというのを受信](https://twitter.com/0verfit/status/1615271807191486466)
    - cudfはGPUが必要。
    - cudfを使えない人たちはpolarsがいいと複数人が回答しており興味深い

- TorchServe
  -  [【CADDi Tech Blog】Vertexで3ヶ月で作る運用可能なML API基盤](https://caddi.tech/archives/4123)
    - Vertex AI Endpoints、Vertex AI Model RegistryとTorchServeが良いらしい。
    - Vertex AI Model Registryはterraformで記述できないようだ。
    - TorchServeはAWSでも使えるはずなので気になった。

- TFX
  - [Kaggleで考えるMLシステムの設計とアーキテクチャ - Qiita](https://qiita.com/ieiringoo/items/dec48924e1b82e62752a)
    - TFXとアーキテクチャは面白かった。設計については深く書いてない

- tslearn
  - [時系列波形データの分類](https://qiita.com/tharashi/items/81ca83c83a7550901c87)
    - tslearnというライブラリを使ってクラスタリングする事例
    - 手法はk-shape法というもので2015年に書かれたアルゴらしい

- HuggingFace
  - [【HuggingFace】Transformersを使って画像の類似性システムを構築する方法](https://huggingface.co/blog/image-similarity)
    - 埋め込みベクトルのコサイン類似度を使うらしい
    - 軽いブログネタにはなるか
  - [【HuggingFace】PaddlePaddleがHuggingFaceで使えるように](https://huggingface.co/blog/paddlepaddle)
    - 2016年にBaiduが初めてオープンソース化したPaddlePaddleがHuggingFaceで使えるようになる
    - 画像系はこれからでPaddleNLPが先行しているらしい。
    - そのうち物体検出等(PaddleDetection)も統合されると利用ははかどりそう。

## NLP

- DeBERTaV2
  - [【Hugging Face】日本語 DeBERTa V2 モデルを公開（京都大）](https://huggingface.co/ku-nlp/deberta-v2-base-japanese)
    - コーパスは Wikipedia (3.2GB), CC100 (85GB) に加え OSCAR (54GB) を使っており日本語モデルの中では最大規模
      - [https://twitter.com/nobug5c9/status/1611636869963616258](https://twitter.com/nobug5c9/status/1611636869963616258)
    - ライセンスは、CC-BY-SA-4.0なので商用（ブログ）には使えそう

- Faiss
  - Faissとは、Facebook社が開発を行っている近似近傍探索のOSS
  - [ベクトル検索ライブラリ Faiss を試す｜npaka｜note](https://note.com/npaka/n/nb766e344a4fc)

- DeBERTaV3について
  - [DeBERTaV3: Improving DeBERTa using ELECTRA-Style Pre-Training with Gradient-Disentangled Embedding Sharing - retarfiの日記](https://retarfi.hatenablog.jp/entry/2022/12/15/090815)
    - 解説記事
  - [【Kaggle】Kaggleコンペ「AI4Code」振り返り - Qiita](https://qiita.com/yufuin/items/1bc0bb391ad65d8595d7)
    - シンプルに難しくてよくわからんかった…
    - もう少し詳しいのはこちら
      - [Google AI4Code – Understand Code in Python Notebooks | Kaggle](https://www.kaggle.com/competitions/AI4Code/discussion/367600)
    - とりあえず、deberta-v3とdistilrobertaを最近よく使われる感じかも。
  - [【Kaggle】【Feedback3コンペ振り返り】Winning Solution の良さげな手法を試してみた](https://zenn.dev/aidemy/articles/73886662eda995)
    - seed averagingもやっぱやる人おるんやな。
    - MultilabelStratifiedKFoldはマルチラベルの場合は必須そう。
    - ここでも「文章からの特徴抽出においては現状では DeBERTa V3 が第一択と捉えて間違いなさそうです。」とのこと。

- EmbeddingとSVR(RAPIDS)
  - [言語モデルのEmbeddingとSVR(RAPIDS)で言語モデルの再学習なしに学習する方法](https://secon.dev/entry/2022/12/13/090000-rapids-svr-svc-marc-ja/)
    - これがコンペとかでもまあまあ強いらしいという話。

- LUKE
  - [LUKEの解説記事](https://qiita.com/Mizuiro__sakura/items/9ccbd655501e78df5cc6)
    - 日本製でTransformersに採用された初のものらしい。
    - 先日largeも公開された。
      - https://twitter.com/ikuyamada/status/1585803910014697473?s=12&t=Zr77hnLnTg0OdKXlbDES9A
    - Apache License 2.0で利用しやすいモデルで、tohoku BERT baseを超えてるので期待
    - 単語間の関係性や、事前学習から察するにNERにも強いと予想。

## CV

- YOLOXとLambdaと私
  - [AWS LambdaのコンテナデプロイでYOLOv5の推論エンドポイントを作成する](https://dev.classmethod.jp/articles/aws-lambda-container-deploy-yolov5-inference-endpoint/)

- Box2Mask
  - [【論文】[2212.01579] Box2Mask: Box-supervised Instance Segmentation via Level-set Evolution](https://arxiv.org/abs/2212.01579)
  - [https://twitter.com/_akhaliq/status/1612034778236129280](https://twitter.com/_akhaliq/status/1612034778236129280)
  - 古典的なlevel-set evolutionをNNに結合し、バウンディングボックスの教師のみで、セグメンテーションのマスクを予測するBox2Maskを提案。
  - アプローチ自体はベースのモデル構造によらずに適用でき、CNNとTransformerベース双方で検証している。
  - Swin-Transformerを用いたBox2Maskは、COCOにおいて42.4%のマスク適用率を達成し、最近開発された完全マスク教師付き手法に匹敵する性能。

- ConvNext V2
  - [【論文】[2301.00808] ConvNeXt V2: Co-designing and Scaling ConvNets with Masked Autoencoders](https://arxiv.org/abs/2301.00808)
  - [https://twitter.com/_akhaliq/status/1610097123583819777](https://twitter.com/_akhaliq/status/1610097123583819777)
  - ConvNeXt V2が発表。ひさしくクラス分類用のモデルは追えてないが、一応今のSOTAっぽいと言えそう？

- CLIPSegについて
  - [【Hugging Face】ゼロショット画像セグメンテーションモデルであるCLIPSegをTransformersライブラリで使用する方法](https://huggingface.co/blog/clipseg-zero-shot)
    - CLIPSegはまだ限界があるものの、セグメンテーションのラベル付けを人手でやるための補助として使える。
    - CLIPに画像やテキストを与えると埋め込みベクトルが生成される。
    - あーこれ読んだらCLIPすげーってなるな。ベクトルの類似度を使えば画像検索とかに応用できるのか。

- SegFormer
  - [セマンティックセグメンテーションSOTAモデルSegFormerでのfine tuningチュートリアルを提供](https://twitter.com/RisingSayak/status/1604852453475643393)
    - SegFormerをPyTorchとTensorFlowの双方で実施可能

- Stable Diffusionの仕組み
  - [Stable Diffusion の仕組みを理解する - ABEJA Tech Blog](https://tech-blog.abeja.asia/entry/advent-2022-day19)
    - ざっくり以下な感じかな？
      - 画像をノイズに変換する（学習パラメータは無い補完処理などで実現するらしい）
      - なんかノイズ空間だと特性を維持したまま色々注入できるらしいので、テキストとかを埋め込んで混ぜる
      - テキストを埋め込んで元の画像に戻るように学習する
      - そうするとテキストをいじると、元の画像が良い感じに変換される

- データ拡張ライブラリimgaug
  - 以下で使用されていた
    - [【ブログ】Lookout for Visionのデータ拡張対応方法](https://aws.amazon.com/jp/blogs/machine-learning/image-augmentation-pipeline-for-amazon-lookout-for-vision/)
      - ライブラリを使った拡張方法を提示しており、機能追加というわけではない。
      - imgaugというライブラリを使っている。

## 音声

- WhisperX
  - [WhisperX: Whisperと音素単位のASRを使って正確な音素単位のアラインメントを実行する](https://qiita.com/syoyo/items/98377869b037a87f1634)
  - Whisperだけでは長い発話単位なので、それで正確な発話位置がわかりそう
  - stable-tsとの違いは？

- 話者判定の最新手法
  - [【Google Research】Pixel向けに話者判定ありの書き起こしを実現](https://ai.googleblog.com/2022/12/who-said-what-recorders-on-device.html)
  - 話者判定は以下の論文に基づく（Speaker Diarizationとしては最新と認識して良さそう）
    - [[2109.11641] Turn-to-Diarize: Online Speaker Diarization Constrained by Transformer Transducer Speaker Turn Detection](https://arxiv.org/abs/2109.11641)

- [【Hugging Face】Audio Spectrogram Transformerが使用可能に](https://huggingface.co/docs/transformers/main/en/model_doc/audio-spectrogram-transformer)
  - Audio Spectrogram TransformerはAudio分類のSOTAモデル
  - 事前学習モデルのfine tuningも可能

- audio-datasets
  - [【Hugging Face】Audio用のデータセットハブの紹介](https://huggingface.co/blog/audio-datasets)
    - Whisperのfine tuningでもでてきたけど、AudioデータもHugging Faceで結構使いまわせる
    - 主にASR（音声認識）用と、Audio Classification用に分かれる。

- 音声分離 Demucs
  - [【藤本健のDigital Audio Laboratory】AIでボーカル・ドラムを取り出す、無料音声分離「Demucs」を試す-AV Watch](https://av.watch.impress.co.jp/docs/series/dal/1460920.html)

- Whisperの結果をトークン毎にタイムスタンプ出力できる
  - [jianfch/stable-ts: Stabilizing timestamps of OpenAI's Whisper outputs down to word-level](https://github.com/jianfch/stable-ts)
  - READMEの２つめのmp4ファイルのデモが分かりやすい。
  - 読み解いたときはこれができると思ってなかった。多少ずれてるときもありそうだが、日本語ではどうなるか。

## 時系列データ

- ETSformer
  - [最先端時系列データ分析モデルETSformerを使ってみた - Qiita](https://qiita.com/Isaka-code/items/848589fc4d7dd153e915)
    - 時系列のSOTAモデルとしてETSformerの紹介。
    - 中身については深く書いてなかった、指数平滑化をうまく使うらしい。
- メタ特徴量について
  - [【Kaggle】American Express - Default Predictionコンペで金メダルを獲得しました - Platinum Data Blog by BrainPad](https://blog.brainpad.co.jp/entry/2022/12/22/154432)

## 理論

- 損失関数
  - [[2301.05579] A survey and taxonomy of loss functions in machine learning](https://arxiv.org/abs/2301.05579)
    - 損失関数を体系的に整理した論文らしい。
    - 結構難しそうだけどきちんと読んだ方がよさそう。
