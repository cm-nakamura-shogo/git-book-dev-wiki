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

## アップデート

### [2023-04-19 SageMaker Studio LabがCAPTCHAに対応しボットやスクリプトの使用を抑制](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-sagemaker-studiolab-combats-bots-captcha/)

- あの画像に記載された文字を手入力したりするやつ