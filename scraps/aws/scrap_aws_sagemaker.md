# Amazon SageMaker

## Articles

- [2022-04-14 【Amazon SageMaker】ネットワーク設計パターンをまとめてみた | DevelopersIO](https://dev.classmethod.jp/articles/sagemaker-network-vpc-architecture-2022-04/#toc-1)
- [2022-12-01 UIが一新されたAmazon SageMaker Studioの歩き方 | DevelopersIO](https://dev.classmethod.jp/articles/how-to-walk-around-amazon-sagemaker-studio-new-ui/#toc-5)
- [2023-07-14 Amazon SageMaker ドメイン作成時に設定が必要な各パラメータを解説 | DevelopersIO](https://dev.classmethod.jp/articles/amazon-sagemaker-domain-setup-parameter/#toc-2)
- [2023-07-25 SageMaker JumpStartを使用して、インターネット接続のないVPCモードでジェネレーティブAI基盤モデルを使用する](https://aws.amazon.com/jp/blogs/machine-learning/use-generative-ai-foundation-models-in-vpc-mode-with-no-internet-connectivity-using-amazon-sagemaker-jumpstart/)
  - Flan T5-XXLを使用
- [2023-07-26 SageMaker JumpStartでStable Diffusion XLを使用する](https://aws.amazon.com/jp/blogs/machine-learning/use-stable-diffusion-xl-with-amazon-sagemaker-jumpstart-in-amazon-sagemaker-studio/)
- [2023-08-18 SageMakerのノートブックインスタンスを時間になったら起動・停止して、アイドル状態が続いたら停止させてみた | DevelopersIO](https://dev.classmethod.jp/articles/sagemaker-notebook-scheduled-start-stop/)

## Update

- [2023-07-24 SageMaker Feature Store がクロスアカウントの共有、検出、アクセスのサポートを開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-sagemaker-feature-store-account-sharing-discovery-access/)
- [2023-08-21 Amazon SageMaker Studio LabがSageMaker Distributionをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-studio-lab-supports-sagemaker-distribution/)
- [2023-08-21 Amazon Sagemaker Data WranglerがS3アクセスポイントに対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-data-wrangler-s3-access-points/)
  - 単一のバケットポリシーを変更する代わりに、組織は特定のユースケースに合わせた個々のポリシーを持つ複数のアクセスポイントを作成することができ、設定ミスや機密データへの意図しないアクセスのリスクを低減します。
- [2023-08-22 Amazon SageMaker Data WranglerがAmazon EMRのロールベースのアクセスコントロールに対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-data-wrangler-role-access-emr/)
  - [Apply fine-grained data access controls with AWS Lake Formation in Amazon SageMaker Data Wrangler | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/apply-fine-grained-data-access-controls-with-aws-lake-formation-in-amazon-sagemaker-data-wrangler/)
- [2023-08-23 Amazon SageMaker、新しいローリングデプロイメントエンドポイントアップデートオプションを発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-rolling-deployment-endpoint-update-option/)
  - ローリングデプロイメント戦略を使用して Amazon SageMaker エンドポイントをアップデートできるように
- [2023-08-23 Amazon SageMakerモデルカードがモデルカードのクロスアカウント共有に対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-model-cards-cross-account-sharing-model-cards/)
- [2023-08-24 Amazon SageMaker、ディープラーニングモデル開発向けGPU/CPUプロファイラツールのプレビューを発表](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-sagemaker-preview-gpu-cpu-profiler-tooling-model-development/)
  - Amazon SageMaker Profilerのプレビューを発表
  - [Announcing the Preview of Amazon SageMaker Profiler: Track and visualize detailed hardware performance data for your model training workloads | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/announcing-the-preview-of-amazon-sagemaker-profiler-track-and-visualize-detailed-hardware-performance-data-for-your-model-training-workloads/)
- [2023-09-01 SageMaker CanvasがJDBCによる追加のデータコネクタをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/09/amazon-sagemaker-canvas-data-connectors-jdbc/)
  - Salesforce、Databricks、SQL Server、MySQL、PostgreSQL、MariaDB、Amazon RDS、およびAmazon Aurora用の8つの新しいJDBCコネクタをサポート
- [2023-09-01 Sagemaker Real-time Inferenceがレスポンスストリーミングをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/09/sagemaker-real-time-inference-response-streaming/)
- [2023-09-05 Amazon SageMakerの地理空間機能がGPUベースのインスタンスでノートブックをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/09/amazon-sagemaker-geospatial-notebook-gpu-instances/)
  - 書いてある通り
- [2023-09-06 Amazon SageMaker InferenceがPyTorchのMME(マルチモデルエンドポイント)をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/09/amazon-sagemaker-inference-multi-model-endpoints-pytorch/)
  - TorchServe を使用してデプロイされた PyTorch モデルをサポートするように
  - [Run multiple generative AI models on GPU using Amazon SageMaker multi-model endpoints with TorchServe and save up to 75% in inference costs | AWS Machine Learning Blog](https://aws.amazon.com/jp/blogs/machine-learning/run-multiple-generative-ai-models-on-gpu-using-amazon-sagemaker-multi-model-endpoints-with-torchserve-and-save-up-to-75-in-inference-costs/)
- [2023-09-06 Amazon SageMaker JumpStartを使用して、Llama 2モデルをfine-tuningすることが可能に](https://aws.amazon.com/jp/blogs/machine-learning/fine-tune-llama-2-for-text-generation-on-amazon-sagemaker-jumpstart/)
  - LLMは巨大なモデルであるため、fine-tuningにもLoRAや量子化、データ並列化トレーニング(FSDP)などの設定がある
  - モデル規模により使用可能なfine-tuning方法に違いがある
  - fine-tuningにかかる時間なども記載されており、70Bで最大8時間程度の計測結果がある
- [2023-09-06 Amazon SageMaker JumpStartを使用したGenerative AIとRAGによる安全なエンタープライズアプリケーションの構築](https://aws.amazon.com/jp/blogs/machine-learning/build-a-secure-enterprise-application-with-generative-ai-and-rag-using-amazon-sagemaker-jumpstart/)
  - RAGにOpenSearchを使うアーキテクチャ例
