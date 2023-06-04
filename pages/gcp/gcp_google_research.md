# Google Research

### [2023-04-21 Visual Blocks for ML: Accelerating machine learning prototyping with interactive tools – Google AI Blog](https://ai.googleblog.com/2023/04/visual-blocks-for-ml-accelerating.html)

### [2023-04-14 Google Research : 自動微分を越えるアルゴリズム](https://ai.googleblog.com/2023/04/beyond-automatic-differentiation.html)

- 相変わらず先進的。
- 一応、AutoBoundとしてライブラリを公開しているらしい。

### [2023-04-20 Google Research : 長期な時系列予測のための研究正解TiDEモデルの紹介](https://ai.googleblog.com/2023/04/recent-advances-in-deep-long-horizon.html)

- 既存手法としてTransformer系のFEDformerやPatchTSTを例にしている
- TiDEはシンプルなMLPアーキテクチャがベースのEncoder-Decoderモデルとなっている
- 入力として過去の出力yやAttributes、特徴量xから構成される
- これらはGoogle CloudのVertex AutoML Forecastingで近々利用できるようになる予定

### [2023-04-25 Google Research : 多項式複雑度でNASを実現するLayerNAS](https://ai.googleblog.com/2023/04/layernas-neural-architecture-search-in.html)

- 探索すべきモデル候補の数が1桁減少し、計算量や最終的な性能がより良いモデルアーキテクチャを発見することが可能

### [2023-05-04 MaMMUT: マルチモーダルのための新しい基盤モデルアーキテクチャの研究 (Google Research)](https://ai.googleblog.com/2023/05/mammut-simple-vision-encoder-text.html)

- 視覚言語基盤モデルは、一般的にはCLIPなどに代表される対照学習と次トークン予測の２つの主要なシナリオが一般的
- 前者と後者で得意な下流タスクがことなるため課題
- MaMMUTはこれを解決するアーキテクチャとなっており、更に先行研究よりも多くの画像フレームを扱えるため、動画処理にもメリットがある
- 要するにImage側のエンコーダ結果をテキスト側のデコーダのCross Attentionとして使うところがポイントっぽい

### [2023-05-13 F-VLM: Open-Vocabulary Object Detection upon Frozen Vision and Language Models](https://ai.googleblog.com/2023/05/f-vlm-open-vocabulary-object-detection.html)

- カテゴリを限定しない物体検出器という感じで、カテゴリ名をText Encoderで埋め込む
- 分類用のヘッドは学習対象する
- Vision EncoderとText EncoderはFrozenでやる
- SAMの物体検出版？というわけではなさそうだが、汎用性は高そう

### [2023-05-25 I/O 2023でのGoogle Research](https://ai.googleblog.com/2023/05/google-research-at-io-2023.html)

- PaLM2意外の研究内容についても触れられている
- 個人的にはChirpという音声認識を把握してなかった、まだプレビューだがWhisperとの比較をしたい。
- Text to Speechで利用可能
  - [Chirp: Universal speech model  |  Cloud Speech-to-Text v2 documentation  |  Google Cloud](https://cloud.google.com/speech-to-text/v2/docs/chirp-model)

### [2023-05-25 大規模データセットのための差分プライベートクラスタリング](https://ai.googleblog.com/2023/05/differentially-private-clustering-for.html)

### [2023-05-26 チャートなどのグラフを理解する基盤モデルの研究](https://ai.googleblog.com/2023/05/foundation-models-for-reasoning-on.html)

### [2023-05-31 ソフトウェア開発活動のための大規模シーケンスモデル](https://ai.googleblog.com/2023/05/large-sequence-models-for-software.html)

### [2023-06-01 検索支援型視覚言語事前トレーニング](https://ai.googleblog.com/2023/06/retrieval-augmented-visual-language-pre.html)
