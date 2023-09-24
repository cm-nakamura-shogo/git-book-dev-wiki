# AWS AIMLサービスその他

## articles

- [2023-09-04 小売業で売り上げ数量の予測を実現するサンプルソリューションを公開しました | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/retail-large-data-ml-e2e/)
  - シンプルで見通しが良いひな型をCDKで提供
- [2023-09-05 Amazon EC2 Inf1、Inf2 インスタンスにおける FastAPI と PyTorch モデルの AWS Inferentia 利用時の最適化 | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/optimize-aws-inferentia-utilization-with-fastapi-and-pytorch-models-on-amazon-ec2-inf1-inf2-instances/)
  - AWS Inferentia1 デバイスには 4 つの NeuronCore-v1 が含まれ、各 AWS Inferentia2 デバイスには 2 つの NeuronCore-v2 が含まれる
  - AWS Neuron SDK を使用すると、各 NeuronCore を並列に使用できる
  - Inf2 は、Inf1 と比較してコアの数は少ないですが、Inf1よりも4倍大きいスループットと10倍小さいレイテンシを提供することが可能
- [2023-09-08 Amazon Rekognition、Amazon SageMaker JumpStart、およびAmazon OpenSearch Serviceを使用した記事のセマンティック画像検索](https://aws.amazon.com/jp/blogs/machine-learning/semantic-image-search-for-articles-using-amazon-rekognition-amazon-sagemaker-foundation-models-and-amazon-opensearch-service/)
  - Rekognitionを使用して画像からメタデータを抽出するプロセスをStep FunctionsやLambdaで構築
  - メタデータをテキストとして埋め込みベクトルを作成する、モデルはJumpStartにあるGPT-J 6B Embeddingを使用
  - これをk-NN ベクトルとしてOpenSearch Service のインデックスに保存、一部はメタデータのまま保存
  - 要約モデルには、AI21 Labs Summarizeモデルを使用し、およそ10,000語を処理できるため多くのテキストは一度に要約できる
- [2023-09-12 AWS を使用した公益事業用スマートメータリングへのアプリケーション統合 | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/application-integration-in-utility-smart-metering-using-aws/)
  - この辺り検証せないかんのかも
  - ここなども
    - [AWS IoTと Kinesis Analyticsを使ったニアリアルタイムデータ収集と加工 - たそらぼ](https://tasotasoso.hatenablog.com/entry/2019/08/02/135115)

## updates

- [2023-08-29 AWS NeuronがLlama2やSDXLなどのモデルをサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/aws-neuron-llama2-gpt-neox-sdxl-ai-models/)
  - AWS Neuronは、生成AIのために特別に構築されたAmazon EC2のInferentiaとTrainiumベースのインスタンス用のSDK
