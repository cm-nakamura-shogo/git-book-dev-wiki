# Amazon SageMaker

## Amazon SageMaker Serverless Inference

必要に応じてエンドポイントを立ち上げることが可能なサービス。

ただし、GPU対応していないため、今後はそこの対応が期待される。

Serverlessが最適化どうか判断するためのベンチマークについて、以下のブログで紹介されている。

- [Introducing the Amazon SageMaker Serverless Inference Benchmarking Toolkit | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/introducing-the-amazon-sagemaker-serverless-inference-benchmarking-toolkit/)

## Amazon SageMaker Clarify

機械学習モデルの解釈可能性を可視化するサービス。

SHAPなどを使って寄与度を算出することが可能となっている。

- [【速報】その予測は本当に正しいの？データの偏りを検出するサービス「Amazon SageMaker Clarify」登場！ #reinvent | DevelopersIO](https://dev.classmethod.jp/articles/breaking-amazon-sagemaker-clarify/)

## Amazon SageMaker Automatic Model Tuning

「ランダム」、「ベイズ」、「ハイパーバンド」、「グリッドサーチ」が使用可能。

「グリッドサーチ」は2022-10発表。

- [Amazon SageMaker Automatic Model Tuning now supports grid search | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/amazon-sagemaker-automatic-model-tuning-now-supports-grid-search/)

「ハイパーバンド」は良く知らなかったけど、Bandit-Basedなランダムサーチらしい。(2016年発表なので比較的新しいかも)

- [https://arxiv.org/abs/1603.06560](https://arxiv.org/abs/1603.06560)

## Amazon SageMaker Data Labeling

機械学習モデルのトレーニング向けのデータセットを作成するサービス。

料金としては、数千ドルから数万ドルが事例としてある様子。

- [Data Labeling の料金 - Amazon SageMaker Ground Truth - Amazon Web Services](https://aws.amazon.com/jp/sagemaker/data-labeling/pricing/?nc=sn&loc=3)

### Amazon SageMaker Ground Truth

自社のデータラベリングワークフローやワークフォースを柔軟に構築および管理する。

Amazon Mechanical Turk、サードパーティーベンダー、または独自のプライベートワークフォースを介して人間のアノテーターを使用するオプションを提供可能。

また、自動ラベル付けされた合成画像を生成することも可能。(2022-06にGA)

以下の記事の紹介によると、作成したデータセットはSageMaker以外にもRekognition Custom Labelsでもそのまま使用可能。

- [[Amazon SageMaker] Ground Truthで物体検出用のデータセットを作成してみました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-sagemaker-ground-truth-create-dataset/)

### Amazon SageMaker Ground Truth Plus

ラベリングアプリケーションを構築したり、ラベル付けのための労働力を自ら管理したりすることなく、質の高いトレーニングデータセットを作成することが可能。

データをアップロードするだけで、SageMaker Ground Truth Plus がお客様に代わってデータラベリングワークフローとワークフォースを作成および管理する。

re:invent2021で発表された。

## Amazon SageMaker Data Wrangler

機械学習向けのデータ前処理用のサービス。

データソースとしては、S3やAthena、Redshiftなど。

AWS SDK for pandas(旧称：AWS Data Wrangler)とは別物のため注意。

Wrangler自体で課金というよりはStudioを立ち上げてたりジョブを実行する際に課金される様子。

- [いつどこで課金が発生してる？Amazon SageMakerの動きと料金体系をセットで考える | DevelopersIO](https://dev.classmethod.jp/articles/sagemaker-pricing/)

## 参考記事

### [2022-04-14 【Amazon SageMaker】ネットワーク設計パターンをまとめてみた](https://dev.classmethod.jp/articles/sagemaker-network-vpc-architecture-2022-04/)

### [2023-04-20 SageMaker Inference Recommenderの最新のアップデート](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/general-availability-amazon-codecatalyst/)

以下が挙げられている

- SageMaker Python SDKによる推論リコメンダーの実行サポート
- 推論レコメンダーの操作性向上
- 推論リコメンダーの柔軟な運用を可能にする新APIを公開
- ロギングとメトリクスのためのAmazon CloudWatchとのより深い統合

### [2023-04-21 バッチ処理のユースケースに対応したSageMaker Pipelineの例を紹介](https://aws.amazon.com/jp/blogs/machine-learning/create-sagemaker-pipelines-for-training-consuming-and-monitoring-your-batch-use-cases/)

### [2023-04-27 CustomOpsでTrainiumの機能を拡張する方法](https://aws.amazon.com/jp/blogs/machine-learning/how-to-extend-the-functionality-of-aws-trainium-with-custom-operators/)

- TrainiumやInferentiaは、Neuron SDKを通じてソフトウェアでCustomOpsをサポート
- GPSIMDエンジンを用いてハードウェアを加速させる
  - General Purpose Single Instruction Multiple Data engine

### [2023-04-20 AWS-CDKを使い爆速で機械学習環境SageMakerStudioを構築する。with TypeScript - Qiita](https://qiita.com/kennyQiita/items/628be93f8aa7ea37be68)

### [2023-05-02 SageMaker上のTriton推論サーバで動作するFILバックエンドの詳細](https://aws.amazon.com/jp/blogs/machine-learning/hosting-ml-models-on-amazon-sagemaker-using-triton-xgboost-lightgbm-and-treelite-models/)

- Triton推論サーバがエンドポイントで使用
- FIL(Forest Inference Library)は各フレームワーク（XGBoost, LightGBM, cuML）の独自性をうまく吸収してくれそう

### [2023-05-02 独自のMLモデルをSageMaker Canvasに持ち込み、正確な予測を生成する方法](https://aws.amazon.com/jp/blogs/machine-learning/bring-your-own-ml-model-into-amazon-sagemaker-canvas-and-generate-accurate-predictions/)

- 以下３つのアーキテクチャ事例を紹介している
  - SageMaker AutopilotとCanvas
  - SageMaker JumpStartとCanvas
  - SageMaker Model RegistryとCanvas

### [2023-05-02 SageMaker JumpStartの基盤モデルによるRetrieval Augmented Generationを用いたQA](https://aws.amazon.com/jp/blogs/machine-learning/question-answering-using-retrieval-augmented-generation-with-foundation-models-in-amazon-sagemaker-jumpstart/)

- LLMsを用いたRAGによるテキスト生成では、LLMsに供給されるコンテキストの一部として特定の外部データを供給することで、ドメイン固有のテキスト出力を生成することが可能
- 以下２つの事例を取り上げている
  - LangChainライブラリとAmazon SageMakerのエンドポイントを使う方法
  - SageMakerのKNNアルゴリズムを使って、SageMakerのエンドポイントを使って大規模データの意味検索を行う方法
- LLMsはオープンソース（GPT-J-6B、Flan T5 UL2、BloomZ 7B1）を使っており、近年のに比べると軽量なものの事例

### [2023-05-03 SageMakerドメイン復旧についてのソリューション事例 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/implement-backup-and-recovery-using-an-event-driven-serverless-architecture-with-amazon-sagemaker-studio/)

### [2023-05-04 SageMaker JumpStartを使ってGenerative AIをAWSで始める方法 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/get-started-with-generative-ai-on-aws-using-amazon-sagemaker-jumpstart/)

### [2023-05-09 SageMaker上のTriton推論サーバで動作するPythonバックエンドの紹介](https://aws.amazon.com/jp/blogs/machine-learning/host-ml-models-on-amazon-sagemaker-using-triton-python-backend/)

- FILの記事に似ている。違いが良く分からん。

### [2023-05-09 SageMaker上のESMFold言語モデルによるタンパク質構造予測の高速化](https://aws.amazon.com/jp/blogs/machine-learning/accelerate-protein-structure-prediction-with-the-esmfold-language-model-on-amazon-sagemaker/)

- ESMFoldは、アミノ酸配列からタンパク質の構造を予測するために開発された、高精度な深層学習ベースの手法
- AlpaFold2などと異なり、ルックアップやMultiple Sequence Alignmentを必要とせず、外部データベースへの依存もない
- その代わりに大規模なタンパク質言語モデル（pLM）をバックボーンとして使用する

### [2023-05-10 SageMaker CanvasのML予測を使ってAmazon QuickSightで予測ダッシュボードを公開する事例](https://aws.amazon.com/jp/blogs/machine-learning/publish-predictive-dashboards-in-amazon-quicksight-using-ml-predictions-from-amazon-sagemaker-canvas/)

### [2023-05-10 GravitonでSageMakerの推論コストを削減する](https://aws.amazon.com/jp/blogs/machine-learning/reduce-amazon-sagemaker-inference-cost-with-aws-graviton/)

- Graviton3ベースのEC2 c7gインスタンスを使ったSageMakerリアルタイム推論の例
- 比較対象として、16個のvCPUと32GiBのメモリのスペックで横並びに評価している
- Gravitonインスタンスにモデルをデプロイするには、AWS DLC(Deep Learning Container)を使用するか、ARMv8.2アーキテクチャに対応したコンテナを自身で用意すればよいとのこと
- 自身で用意するための公式ドキュメント
  - [Building your own algorithm container — Amazon SageMaker Examples 1.0.0 documentation](https://sagemaker-examples.readthedocs.io/en/latest/advanced_functionality/scikit_bring_your_own/scikit_bring_your_own.html)

### [2023-05-16 SageMaker JumpStartでGPT-NeoXT-Chat-Base-20Bという基盤モデルを提供開始](https://aws.amazon.com/jp/blogs/machine-learning/gpt-neoxt-chat-base-20b-foundation-model-for-chatbot-applications-is-now-available-on-amazon-sagemaker/)

- 20Bなので性能は良さそうだが、日本語対応が微妙かもしれない。

### [2023-05-17 SageMaker JumpStartで大規模言語モデルによるサーバーレスな会議要約バックエンドを構築](https://aws.amazon.com/jp/blogs/machine-learning/build-a-serverless-meeting-summarization-backend-with-large-language-models-on-amazon-sagemaker-jumpstart/)

- Flan-T5-XLを使う。日本語モデルに差し替えできれば有用かもしれない。
- Lambda + S3のバケツリレーでTranscribeとSageMaker Endpointを使う
- SageMaker Endpointのお値段が。。

### [2023-05-22 SageMaker JumpstartによるFLAN T5 XLのインストラクションファインチューニング](https://aws.amazon.com/jp/blogs/machine-learning/instruction-fine-tuning-for-flan-t5-xl-with-amazon-sagemaker-jumpstart/)

### [2023-05-23 AWS CDKを使用してAmazon SageMaker JumpStartから生成型AIモデルをデプロイする](https://aws.amazon.com/jp/blogs/machine-learning/deploy-generative-ai-models-from-amazon-sagemaker-jumpstart-using-the-aws-cdk/)

- アプリにはECS + Fargateを使用し、Streamlitで構築する
- 画像生成とNLU・テキスト生成にはAPIGW + Lambda + SageMaker Endpointを使用
- これらすべてを4つのStackに分けてCDKで構築している

### [2023-05-24 SageMaker Jumpstart Text2Textでバッチ変換を実行する例](https://aws.amazon.com/jp/blogs/machine-learning/perform-batch-transforms-with-amazon-sagemaker-jumpstart-text2text-generation-large-language-models/)

- こちらもFLAN T5を使用する例


### [2023-05-30 SageMakerの使用量を分析し、使用状況に応じたコスト最適化の機会を見極める(全五回シリーズ)](https://aws.amazon.com/jp/blogs/machine-learning/part-1-analyze-amazon-sagemaker-spend-and-determine-cost-optimization-opportunities-based-on-usage-part-1/)

### [2023-05-30 SageMaker XGBoostが完全分散型GPUトレーニングを提供開始](https://aws.amazon.com/jp/blogs/machine-learning/amazon-sagemaker-xgboost-now-offers-fully-distributed-gpu-training/)

- マルチGPUでのトレーニングに対応

### [2023-05-31 SageMakerで基盤モデルを使用して認定試験へ学習する](https://aws.amazon.com/jp/blogs/machine-learning/accelerate-your-learning-towards-aws-certification-exams-with-automated-quiz-generation-using-amazon-sagemaker-foundations-models/)

### [2023-05-31 SageMaker Python SDKでAmazon SageMakerリソースのデフォルトを設定・使用する](https://aws.amazon.com/jp/blogs/machine-learning/configure-and-use-defaults-for-amazon-sagemaker-resources-with-the-sagemaker-python-sdk/)

### [2023-05-31 SageMaker上でTritonのPyTorchバックエンドを深く理解する](https://aws.amazon.com/jp/blogs/machine-learning/host-ml-models-on-amazon-sagemaker-using-triton-cv-model-with-pytorch-backend/)

### [2023-05-31 Amazon ECS でTrainiumインスタンスを使用してコンテナ内でMLワークロードを実行する](https://aws.amazon.com/jp/blogs/machine-learning/scale-your-machine-learning-workloads-on-amazon-ecs-powered-by-aws-trainium-instances/)

### [2023-06-07 SageMakerで最新のLLM基盤モデル Falcon-40Bをトレーニング](https://aws.amazon.com/blogs/machine-learning/technology-innovation-institute-trains-the-state-of-the-art-falcon-llm-40b-foundation-model-on-amazon-sagemaker/)

- 最近界隈で石油マネーLLMと話題になっているやつ
- 記事はゼロから事前学習モデルを作る方法について紹介されているのであくまで読み物として

### [2023-06-06  SageMaker Python SDKを使用して、Amazon SageMaker Offline Featurestoreから機械学習可能なデータセットを構築する](https://aws.amazon.com/blogs/machine-learning/build-machine-learning-ready-datasets-from-the-amazon-sagemaker-offline-feature-store-using-the-amazon-sagemaker-python-sdk/)

### [2023-06-09 Tritonを使用してAmazon SageMaker上でONNXモデルをホストする](https://aws.amazon.com/jp/blogs/machine-learning/host-ml-models-on-amazon-sagemaker-using-triton-onnx-models/)

- ONNXの最大のメリットは、異なるフレームワークやツール間でMLモデルを表現し、交換するための標準化された形式を提供すること
- 記事では、GPUを使用するマルチモデルエンドポイント（MME）向けにONNXベースのモデルをデプロイする方法を紹介

### [2023-06-12 SageMaker Hugging Face Estimatorとモデル並列ライブラリを使ってGPT-Jをfine tuningする](https://aws.amazon.com/jp/blogs/machine-learning/fine-tune-gpt-j-using-an-amazon-sagemaker-hugging-face-estimator-and-the-model-parallel-library/)

- モデル並列化に関する説明があってよい

### [2023-06-12 Amazon SageMaker上でOpenChatkitのモデルを使用したカスタムチャットボットアプリケーションを構築](https://aws.amazon.com/jp/blogs/machine-learning/build-custom-chatbot-applications-using-openchatkit-models-on-amazon-sagemaker/)

## アップデート

### [2023-04-19 SageMaker Studio LabがCAPTCHAに対応しボットやスクリプトの使用を抑制](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-studiolab-combats-bots-captcha/)

- あの画像に記載された文字を手入力したりするやつ

### [2023-04-25 ローカルMLコードのリモートジョブへの変換を高速化](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-local-ml-code-conversion-jobs/)

- SageMaker Python SDKを使って、作成したローカルMLコードを、依存関係とともに、最小限のコード変更でトレーニングジョブとして実行できるように
- コードにPythonデコレータを追加するだけで、そのコード、データセット、ワークスペース環境の設定を受け取り、SageMaker Trainingジョブとして実行
- サンプルノートブックは[こちら](https://github.com/aws/amazon-sagemaker-examples/tree/main/sagemaker-remote-function)
- 公式ブログは[こちら](https://aws.amazon.com/jp/blogs/machine-learning/run-your-local-machine-learning-code-as-amazon-sagemaker-training-jobs-with-minimal-code-changes/)

### [2023-04-27 SageMaker with TensorBoardの一般提供を開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-hosted-tensorboard/)

- TensorBoardを使用して、SageMakerトレーニングジョブのモデル収束の問題を可視化し、デバッグが可能に
- TensorBoardは、トレーニングセットと検証セットにおけるモデルの精度やロスを追跡するために一般的に使用される観測可能ツール
- 価格表にも更新があり、ホスティングするためにml.r5.largeインスタンスが使われ、US Eastで1時間$0.126程度
- 東京リージョンではまだ使えない。
- 公式ブログ
  - [Amazon SageMaker with TensorBoard: An overview of a hosted TensorBoard experience | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/amazon-sagemaker-with-tensorboard-overview-of-a-hosted-tensorboard-experience/)

### [2023-05-01 Data Wranglerが画像データ作成に対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-sagemaker-data-wrangler-image-data-preparation/)

- ラベリング、トレーニング、推論のための画像データを準備することが可能に
- S3から画像をプレビューしてインポートし、さまざまな組み込み画像変換を使用して、画像データのクリーン化、標準化、品質改善を行う
- ビルトイン変換には、リサイズ、重複の削除、回転、反転、グレイスケール、コントラストの強化、ぼかし、ノイズの追加など
- スニペットを使って、異常値の検出や画像からテキストを抽出するなどの高度な使用例もサポート
- 公式ブログ
  - [Prepare image data with Amazon SageMaker Data Wrangler | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/prepare-image-data-with-amazon-sagemaker-data-wrangler/)

### [2023-05-03 SageMakerのデプロイインスタンスにml.inf2とml.trn1が対応 (AWS)](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/sagemaker-ml-inf2-ml-trn1-instances-model-deployment/)

- 公式ブログでも
  - [2023-05-04 SageMaker上でInferentia2とTrainiumを使ってGenerative AIの推論を低コスト・高パフォーマンスで実現する方法](https://aws.amazon.com/jp/blogs/machine-learning/achieve-high-performance-with-lowest-cost-for-generative-ai-inference-using-aws-inferentia2-and-aws-trainium-on-amazon-sagemaker/)

### [2023-05-10 SageMaker Serverless Inferenceのプロビジョンドコンカレンシーを発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/provisioned-concurrency-amazon-sagemaker-serverless-inference/)

- Serverless Inferenceのコールドスタートを緩和し、ワークロードの予測可能なパフォーマンス特性を得ることが可能に
- [Announcing provisioned concurrency for Amazon SageMaker Serverless Inference | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/announcing-provisioned-concurrency-for-amazon-sagemaker-serverless-inference/)

### [2023-05-10 SageMaker CanvasでMLモデルを本番で運用できるように](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-sagemaker-canvas-operationalize-ml-models-production/)

- 学習したモデルをワンクリックでSageMaker Model registryに登録できるように
- 公式ブログ
  - [Operationalize ML models built in Amazon SageMaker Canvas to production using the Amazon SageMaker Model Registry | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/operationalize-ml-models-built-in-amazon-sagemaker-canvas-to-production-using-the-amazon-sagemaker-model-registry/)

### [2023-05-10 SageMakerノートブックがml.p4d、ml.p4de、ml.inf1インスタンスをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-sagemaker-notebooks-ml-p4d-ml-p4de-ml-inf1-instances/)

- inf1はinf2が先行していた

### [2023-05-10 SageMaker Autopilotは、重みを持つMLモデルのトレーニングや、8つの目的指標をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/sagemaker-autopilot-training-ml-models-weights-eight-objective-metrics/)

- Ensembleモードでの重み付き客観指標による訓練をサポート
- 追加目的指標は、RMSE、MAE、R2、Balanced Accuracy、Precision、Precision Macro、Recall、Recall Macro
- 標準的な指標がそろった感じか
- APIアップデートが先行していた
  - [2023-05-02 Sagemaker Autopilotは、サンプルの重みと追加の目的指標を持つトレーニングモデルをサポート (AWS)](https://awsapichanges.info/archive/changes/bd55ca-api.sagemaker.html)


### [2023-05-19 SageMaker Geospatial MLが一般提供開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-sagemaker-supports-geospatial-ml-generally-available/)

### [2023-05-25 SageMaker JumpStartがLLMのドメイン固有のデータセットによるfine-tuning機能を提供](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-sagemaker-jumpstart-fine-tuning-foundation-models-domain-adaptation/)

- 公式ブログによる紹介はGPT-J 6Bモデル
  - [Domain-adaptation Fine-tuning of Foundation Models in Amazon SageMaker JumpStart on Financial data | AWS Machine Learning Blog](https://aws.amazon.com/blogs/machine-learning/domain-adaptation-fine-tuning-of-foundation-models-in-amazon-sagemaker-jumpstart-on-financial-data/)

### [2023-05-26 SageMaker Notebook インスタンスに ml.p4d と ml.infが追加](https://awsapichanges.info/archive/changes/3e813c-api.sagemaker.html)

### [2023-05-30 SageMaker Ground Truth PlusがRLHF(Reinforcement Learning from Human Feedback)に対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/sagemaker-ground-truth-plus-human-feedback-fine-tuning-data-generative-ai/)

- RLHFにより人間の好みに合った出力を学習できる
- 公式ブログ
  - [High-quality human feedback for your generative AI applications from Amazon SageMaker Ground Truth Plus | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/high-quality-human-feedback-for-your-generative-ai-applications-from-amazon-sagemaker-ground-truth-plus/)

### [2023-06-06 SageMaker Automatic Model Tuningが探索や試行、最大実行時間を目標変数に基づいた自動選択が可能に](https://aws.amazon.com/about-aws/whats-new/2023/06/sagemaker-automatic-model-tuning-configurations/)

- ジョブ定義の一部として必要だったハイパーパラメータの範囲、チューニング戦略、ジョブ数などの設定を指定する必要がない新しい設定であるautotuneを提供する

### [2023-06-07 SageMaker Pipelinesにおいて、パイプライン内の任意のステップをサブワークフローとして実行することができる新機能を発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/06/amazon-sagemaker-pipelines-selective-executions/)

- 関連するAPI Changes
  - [https://awsapichanges.info/archive/changes/372fd4-api.sagemaker.html](https://awsapichanges.info/archive/changes/372fd4-api.sagemaker.html)

### [2023-06-07 SageMaker Canvasがモデルの再トレーニングと、更新されたデータセットによるバッチ予測ワークフローの自動化機能を提供](https://aws.amazon.com/about-aws/whats-new/2023/06/amazon-sagemaker-canvas-ml-models-workflows-datasets/)

- プロダクション向きの機能がでてきた
- 対応するデータソースは、ローカルアップロードとAmazon S3のみ。
- [公式ブログ](https://aws.amazon.com/blogs/machine-learning/retrain-ml-models-and-automate-batch-predictions-in-amazon-sagemaker-canvas-using-updated-datasets/)

### [2023-06-08 Amazon SageMaker DistributionがECRから利用可能に](https://aws.amazon.com/jp/blogs/machine-learning/get-started-with-the-open-source-amazon-sagemaker-distribution/)

- Amazon SageMaker Distributionは、機械学習、データサイエンス、可視化のための主要なフレームワークを含むDockerイメージのセット
- CPUとGPUの2種類を準備し、PyTorch、TensorFlow、KerasなどのDeep Learningフレームワーク、numpy、scikit-learn、pandasなどのPythonパッケージ、およびJupyter LabなどのIDEが含まれる
- GPU版は5.3GB程度のイメージサイズ

### [2023-06-09 Falcon 40B基盤モデルがSageMaker JumpStartで利用可能に](https://aws.amazon.com/jp/about-aws/whats-new/2023/06/falcon-40b-foundation-model-tii-sagemaker-jumpstart/)

- Falcon 40Bは、Apache 2.0ライセンスで利用可能な400億パラメータの大規模言語モデル
- 以下のサンプルノートブックで試すことが可能
  - [amazon-sagemaker-examples/introduction_to_amazon_algorithms/jumpstart-foundation-models/text-generation-falcon.ipynb](https://github.com/aws/amazon-sagemaker-examples/blob/main/introduction_to_amazon_algorithms/jumpstart-foundation-models/text-generation-falcon.ipynb)
