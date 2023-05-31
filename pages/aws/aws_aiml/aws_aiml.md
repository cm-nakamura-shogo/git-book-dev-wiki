# AWS AIML全般

### [2023-05-25 OpenSearchとLangChainを組み合わせたソリューション](https://aws.amazon.com/jp/blogs/machine-learning/build-a-powerful-question-answering-bot-with-amazon-sagemaker-amazon-opensearch-service-streamlit-and-langchain/)

- OpenSearch, LangChain, Streamlitなどの組み合わせ
- モデルはFLAN-T5 XXLとGPT-j-6B(ベクトル側)なので差し替えが必要

### [2023-05-24 SageMaker JumpStart上での基盤モデルによる対話誘導型知的文書処理](https://aws.amazon.com/jp/blogs/machine-learning/dialogue-guided-intelligent-document-processing-with-foundation-models-on-amazon-sagemaker-jumpstart/)

### [2023-05-24 AWSのAIサービスを使って、住宅ローンの引受プロセスにおける書類検証や不正検知を自動化](https://aws.amazon.com/jp/blogs/machine-learning/automate-document-validation-and-fraud-detection-in-the-mortgage-underwriting-process-using-aws-ai-services-part-1/)

### [2023-05-10 JupyterConで開発の生産性を高めるための新しいツールを発表 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/announcing-new-jupyter-contributions-by-aws-to-democratize-generative-ai-and-scale-ml-workloads/)

- Jupyter AI
  - LLMを使い、プログラマーがソースコードを生成、デバッグ、説明するのを助けることが可能
  - また、ローカルファイルに関する質問に答えたり、簡単な自然言語のプロンプトからノートブック全体を生成したりすることも可能に
  - マジックコマンドと、JupyterLabのフレンドリーなチャットUIの両方を提供する
- Amazon CodeWhisperer Jupyter エクステンション
  - JupyterLabおよびAmazon SageMaker StudioのPythonノートブックに対して、リアルタイムで1行または全機能のコード提案を生成するCodeWhisperer拡張を無料でインストールして使用できることを発表
- Notebookのスケジュール実行
  - ノートブックスケジューリングツールが、オープンソースのJupyter拡張として登場
  - [Schedule your notebooks from any JupyterLab environment using the Amazon SageMaker JupyterLab extension | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/schedule-your-notebooks-from-any-jupyterlab-environment-using-the-amazon-sagemaker-jupyterlab-extension/)
- Amazon CodeGuru Jupyterエクステンション
  - ノートブックセル内のインジェクションの欠陥、データリーク、弱い暗号、暗号化の欠落などのセキュリティ脆弱性を検出するのを支援
  - また、MLライブラリAPIの誤用、無効な実行順序、非決定性など、計算ノートブックの可読性、再現性、正しさに影響する多くの一般的な問題を検出する

### [2023-05-09 MLflowをAWSで動作しSageMakerと連携する際にアクセス制御を実現する方法 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/securing-mlflow-in-aws-fine-grained-access-control-with-aws-native-services/)

- 前回記事と併せるとMLflowを稼働させる方法の参考になりそう

### [2023-05-08 TensorRTとTriton Inference Serverを使用した最適なパフォーマンスの推論方法について (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/host-ml-models-on-amazon-sagemaker-using-triton-tensorrt-models/)

### [2023-05-05 Amazon KendraとAmazon Rekognitionを統合し画像を検索できるエンジンを実現する方法 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/build-an-image-search-engine-with-amazon-kendra-and-amazon-rekognition/)

- 複雑な画像の例としてAWSのアーキテクチャ図を題材としている
- RekognitionのCustom Labelsやテキスト検出を使用

### [2023-05-03 LLMの独自コンテキスト拡張(RAG)にKendraを使用する例の紹介 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/quickly-build-high-accuracy-generative-ai-applications-on-enterprise-data-using-amazon-kendra-langchain-and-large-language-models/)

- 社内検証してくれた人がいるみたい
  - [Amazon Kendra と OpenAI により最新の AWS ユーザーガイドに基づいて回答するチャットアプリケーションのサンプルを試してみた | DevelopersIO](https://dev.classmethod.jp/articles/using-amazon-kendra-langchain-extensions/)

### [2023-05-03 Gravitonプロセッサに対するPyTorch 2.0の推論性能の最適化を実現 (AWS)](https://aws.amazon.com/jp/blogs/machine-learning/optimized-pytorch-2-0-inference-with-aws-graviton-processors/)

### [2023-04-19 特徴量エンジニアリングとFeature Storeを使ってほぼリアルタイムな特徴量による裏付けを分析](https://aws.amazon.com/jp/blogs/machine-learning/use-streaming-ingestion-with-amazon-sagemaker-feature-store-and-amazon-msk-to-make-ml-backed-decisions-in-near-real-time/)

- ストリーミングの取り込みはAmazon Managed Streaming for Apache Kafka (MSK)(Amazon MSK)を使用
- 事例としてはトランザクションに対する不正検知となっており、結構おもしろい

### [2023-04-18 JumpStartでドメインに適応したLLMをfine-tuningする事例](https://aws.amazon.com/jp/blogs/machine-learning/financial-text-generation-using-a-domain-adapted-fine-tuned-large-language-model-in-amazon-sagemaker-jumpstart/)

- モデルはLLM GPT-J 6Bを使用。

### [2023-04-17 大規模言語モデルをデプロイするためのパイプライン、最適化について](https://aws.amazon.com/jp/blogs/machine-learning/deploy-large-models-at-high-performance-using-fastertransformer-on-amazon-sagemaker/)

- LMI DLC(Large Model Inference, Deep Learning Container)と呼ばれている
- モデルの圧縮や分割方法など網羅的に記載されているかも

### [2023-04-17 SageMaker Data Wrangleでnltkやscipyを使う事例](https://aws.amazon.com/jp/blogs/machine-learning/authoring-custom-transformations-in-amazon-sagemaker-data-wrangler-using-nltk-and-scipy/)

- カスタム変換でnltkやscipyを使うことができる

### [2023-04-17 Fraud Detectorの新機能であるコールドスタートを使用する例](https://aws.amazon.com/jp/blogs/machine-learning/overcome-the-machine-learning-cold-start-challenge-in-fraud-detection-using-amazon-fraud-detector/)

- わずか100イベント程度でリアルタイムの不正防止MLモデルを迅速にブートストラップできる

### [2023-04-17 SageMaker Collections : モデルレジストリのモデルを整理する新機能](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-collections-organize-model-registry/)

- 登録されたモデルのうち互いに関連するものをグループ化し、階層的に整理することが可能

### [2023-04-17 低コストで高性能な生成系 AI 推論用の Amazon EC2 Inf2 インスタンスが一般公開](https://aws.amazon.com/jp/blogs/news/amazon-ec2-inf2-instances-for-low-cost-high-performance-generative-ai-inference-are-now-generally-available/)

- 日本語の公式ブログ記事
- 言語モデル以外でも、inf2.8xlargeやinf2.xlarge辺りは音声処理でもターゲットになるかもしれない。
