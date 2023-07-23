# Vertex AI

## Vertex AIとは

- kubeflowベース。
- kubeflowやk8sに慣れ親しんでおいた方がよい。

- Vertex AIのラーニングパス
  - https://cloud.google.com/blog/ja/topics/developers-practitioners/new-ml-learning-path-vertex-ai

- メルカリ活用例
  - https://engineering.mercari.com/blog/entry/20220224-similar-search-using-matching-engine/

## 参考記事

### [2021-08-05 機械学習パイプラインの要件と Vertex Pipelines / Kubeflow Pipelines V2 による実装 - Speaker Deck](https://speakerdeck.com/asei/kubeflow-pipelines-v2-niyorushi-zhuang)

### [2021-12-09 Vertex Pipelines + KFPのArtifact(不)完全ガイド](https://zenn.dev/kurushi/articles/01ac5fdc4e1bfc)

### [2023-04-20 自己流 Vertex AI Pipelines 開発プラクティス](https://note.com/tatsuyashirakawa/n/n146551bc5a66)

### [2023-05-13 Vertex AI Workbenchが良さそうという話](https://twitter.com/naganumat/status/1657309179110117378)

- Colaboratory の企業版みたいなイメージ
- Cloud Storage と BigQuey にすぐアクセスできる

## アップデート

- [2023-05-10 Vertex AIがGenerative AIをサポート。まだプレビュー (Google Cloud)](https://cloud.google.com/release-notes#May_10_2023)
  - モデルは以下。チャットから埋め込み、チューニングまでカバーしていそう。本気を出してきたか。
    - PaLM 2 for Text: text-bison@001
    - PaLM 2 for Chat: chat-bison@001
    - Embedding for Text: textembedding-gecko@001
    - Generative AI Studio for Language
    - Tuning for PaLM 2
- [2023-05-16 Vertex AI Custom Trainingが Experimentsとの深い統合に対応](https://cloud.google.com/release-notes#May_16_2023)
  - オートロギングを有効にしてトレーニングジョブを送信し、パラメータとモデルのパフォーマンスメトリクスを自動的に記録することが可能に
- [2023-05-16 Vertex AI PipelinesのスケジューラAPIがプレビューで利用可能に](https://cloud.google.com/release-notes#May_16_2023)
  - 頻度、開始時間（オプション）、終了時間（オプション）を指定することで、Vertex AIで定期的に実行されるパイプラインをスケジュールすることが可能に
 [2023-06-01 Vertex AIバッチ予測リクエストの入力または出力として、マルチリージョンのBigQueryテーブルを指定できるように](https://cloud.google.com/release-notes#June_01_2023)
- [2023-06-07 Vertex AIのPaLM 2 for Text, Embedding for Text, Generative AI StudioがGAに](https://cloud.google.com/release-notes#June_07_2023)
  - 発表されたもののうちPaLM 2 for ChatとTuning for PaLM 2以外はGAになったっぽい
- [2023-06-07 Vertex AI Model Gardenが(GA)で提供開始](https://cloud.google.com/release-notes#June_07_2023)
  - Model GardenはVertex AIと選択したOSSモデルの発見、テスト、カスタマイズ、デプロイを支援するプラットフォーム
- [2023-06-07 Vertex AI Codey APIsがプレビュー開始](https://cloud.google.com/release-notes#June_07_2023)
  - Codey APIを利用することで、コード生成、コード補完、コードチャットAPIをGCPプロジェクトからも利用することが可能に
  - Codey APIは、Generative AI studioまたはRESTコマンドでプログラム的に使用可能
 [2023-06-15 chat-bison@001のモデルが更新され、コンテキストフィールドの指示に従いやすくなった](https://cloud.google.com/release-notes#June_15_2023)
 [2023-06-20 A100 80GBアクセラレータは現在、一部の地域でカスタム・トレーニング・ジョブ向けに一般提供](https://cloud.google.com/release-notes#June_20_2023)
- [2023-06-26 Vertex AI WorkbenchがM109のリリースに対応](https://cloud.google.com/release-notes#June_26_2023)
  - Python 3.10およびCUDA 11.8を含むPytorch 2.0のユーザー管理型ノートブックインスタンスが利用可能に
  - その他のソフトウェア・アップデートやバグ修正など
- [2023-06-30 Vertex Explainable AIのexample-based explanationsサポートが一般的に利用可能](https://cloud.google.com/release-notes#June_30_2023)
- [2023-07-06 Vertex AIアップデート](https://cloud.google.com/release-notes#July_07_2023)
  - Vertex AI Model EvaluationはGAに。また以下がプレビュー。
    - スライスされたメトリクスによるモデル評価。
    - 公平性と偏りのメトリクスによるモデル評価。
    - AutoML画像分類モデルの視覚エラー分析。
- [2023-07-10 Vertex AIアップデート](https://cloud.google.com/release-notes#July_10_2023)
  - PaLM 2 for Chat (chat-bison) のサポートが (GA) で利用可能に。
- [2023-07-12 Vertex AIアップデート](https://cloud.google.com/release-notes#July_12_2023)
  - text-bisionのバッチ処理リクエストがGAに。
- [2023-07-18 Vertex AIアップデート](https://cloud.google.com/release-notes#July_18_2023)
  - text-bisionのモデルチューニングを更新：
  - チューニングパイプラインがアップグレードされ、text-bisonにおいてより効率的なチューニングとパフォーマンスの向上を実現。
  - 新しい learning_rate パラメーターにより、各反復のステップサイズを調整できる。
- [2023-07-19 Vertex AI Workbenchアップデート](https://cloud.google.com/release-notes#July_19_2023)
  - Vertex AI Workbenchインスタンスがプレビューで利用可能に
  - Vertex AI Workbenchインスタンスは、マネージドノートブックとユーザマネージドノートブックの機能を組み合わせて、堅牢なデータサイエンスソリューションを提供
  - サポートされる機能は以下の通りです：
    - アイドルタイムアウト
    - BigQueryとクラウドストレージの統合
    - エンドユーザとサービスアカウントの認証
    - VPCサービスコントロール
    - 顧客管理暗号化キー（CMEK）
    - ヘルスステータスの監視
    - スケジュールによるノートブックの実行
    - Dataprocの統合
