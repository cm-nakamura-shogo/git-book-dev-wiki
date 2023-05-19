# Vertex AI

## Vertex AIとは

- kubeflowベース。
- kubeflowやk8sに慣れ親しんでおいた方がよい。

- Vertex AIのラーニングパス
  - https://cloud.google.com/blog/ja/topics/developers-practitioners/new-ml-learning-path-vertex-ai

- メルカリ活用例
  - https://engineering.mercari.com/blog/entry/20220224-similar-search-using-matching-engine/

## アップデート

### [2023-05-10 Vertex AIがGenerative AIをサポート。まだプレビュー (Google Cloud)](https://cloud.google.com/release-notes#May_10_2023)

- モデルは以下。チャットから埋め込み、チューニングまでカバーしていそう。本気を出してきたか。
  - PaLM 2 for Text: text-bison@001
  - PaLM 2 for Chat: chat-bison@001
  - Embedding for Text: textembedding-gecko@001
  - Generative AI Studio for Language
  - Tuning for PaLM 2

### [2023-05-16 Vertex AI Custom Trainingが Experimentsとの深い統合に対応](https://cloud.google.com/release-notes#May_16_2023)

- オートロギングを有効にしてトレーニングジョブを送信し、パラメータとモデルのパフォーマンスメトリクスを自動的に記録することが可能に

### [2023-05-16 Vertex AI PipelinesのスケジューラAPIがプレビューで利用可能に](https://cloud.google.com/release-notes#May_16_2023)

- 頻度、開始時間（オプション）、終了時間（オプション）を指定することで、Vertex AIで定期的に実行されるパイプラインをスケジュールすることが可能に

## 参考記事

### [2023-04-20 自己流 Vertex AI Pipelines 開発プラクティス](https://note.com/tatsuyashirakawa/n/n146551bc5a66)

### [2023-05-13 Vertex AI Workbenchが良さそうという話](https://twitter.com/naganumat/status/1657309179110117378)

- Colaboratory の企業版みたいなイメージ
- Cloud Storage と BigQuey にすぐアクセスできる