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

