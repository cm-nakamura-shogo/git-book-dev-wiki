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

### [2023-06-01 Vertex AIバッチ予測リクエストの入力または出力として、マルチリージョンのBigQueryテーブルを指定できるように](https://cloud.google.com/release-notes#June_01_2023)

### [2023-06-07 Vertex AIのPaLM 2 for Text, Embedding for Text, Generative AI StudioがGAに](https://cloud.google.com/release-notes#June_07_2023)

- 発表されたもののうちPaLM 2 for ChatとTuning for PaLM 2以外はGAになったっぽい

### [2023-06-07 Vertex AI Model Gardenが(GA)で提供開始](https://cloud.google.com/release-notes#June_07_2023)

- Model GardenはVertex AIと選択したOSSモデルの発見、テスト、カスタマイズ、デプロイを支援するプラットフォーム

### [2023-06-07 Vertex AI Codey APIsがプレビュー開始](https://cloud.google.com/release-notes#June_07_2023)

- Codey APIを利用することで、コード生成、コード補完、コードチャットAPIをGCPプロジェクトからも利用することが可能に
- Codey APIは、Generative AI studioまたはRESTコマンドでプログラム的に使用可能


## 参考記事

### [2023-04-20 自己流 Vertex AI Pipelines 開発プラクティス](https://note.com/tatsuyashirakawa/n/n146551bc5a66)

### [2023-05-13 Vertex AI Workbenchが良さそうという話](https://twitter.com/naganumat/status/1657309179110117378)

- Colaboratory の企業版みたいなイメージ
- Cloud Storage と BigQuey にすぐアクセスできる

### [2021-08-05 機械学習パイプラインの要件と Vertex Pipelines / Kubeflow Pipelines V2 による実装 - Speaker Deck](https://speakerdeck.com/asei/kubeflow-pipelines-v2-niyorushi-zhuang)

### [2021-12-09 Vertex Pipelines + KFPのArtifact(不)完全ガイド](https://zenn.dev/kurushi/articles/01ac5fdc4e1bfc)
