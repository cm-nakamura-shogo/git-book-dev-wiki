# Google Cloud全般

## アップデート

### [2023-04-18 日本でもGoogle Bardが利用可能に](https://qiita.com/MasaruYamazaki/items/a107d4455500420ffd5b)

- [Google の会話型 Generative AI である Bard が日本から利用可能になったので試してみました！ | DevelopersIO](https://dev.classmethod.jp/articles/bard-googles-generative-ai-is-now-available-in-japan/)

### [2023-05-11 Bardが日本語に対応 (Google Japan Blog)](https://japan.googleblog.com/2023/05/bard.html)

- ウェイトリストがなくなり180カ国以上ですぐに英語での利用が可能になったこと、そして日本語と韓国語に対応したことが発表
- Bardは現在、Googleが開発した最新のAI基盤モデル「PaLM 2」を用いており、今後さらに強力な基盤モデルのGeminiへ移行する予定
- その他のソース
  - [At Google I/O, generative AI gets to work | Google Cloud Blog](https://cloud.google.com/blog/products/ai-machine-learning/google-cloud-at-io-2023/?hl=en)
  - [［速報］Googleの生成的AI「Bard」が日本語に対応。ウェイトリストもなくなり、すぐに利用できるように。Google I/O 2023 － Publickey](https://www.publickey1.jp/blog/23/googleaibard.html)

### [2023-05-11 Google I/Oでの新製品Gen App Builderに搭載の検索エンジンEnterprise Searchを解説したセッション](https://twitter.com/kazunori_279/status/1656404071522381824?)

- Google検索譲りのセマンティック検索機能を提供。LLMとの統合で全く新しいユーザ体験を実現

### [2023-05-11 Google I/Oで自然言語でAIと対話するだけで誰でもアプリが作れる「Duet AI for AppSheet」発表](https://www.publickey1.jp/blog/23/googleaiduet_ai_for_appsheet.html)

### [2023-05-11 LangChain AI、Chroma、Hubbleなどコラボレーションをダイレクトコールアウト](https://twitter.com/manhnd11/status/1656366327018455043)

### [2023-05-11 Bard(バード)とGPT-4の出力を横並びにする比較記事](https://qiita.com/kumag0r0/items/77dbe743643183ae3e98)

- 結構肉薄しているという印象は私と同じ。

### [2023-06-26 Retail APIのデータエクスポート機能がGA](https://cloud.google.com/release-notes#June_26_2023)

- リテールデータのBigQueryへのエクスポートが一般公開（GA）
- これによりデータを使って、すぐに使える Looker ダッシュボードで主要業績評価指標を取得したり、Vertex AI とステップバイステップの手順を使用して売上予測を行うことが可能
- エンティティは、小売組織を複数のセグメントに細分化する方法として利用できる
- 例えば、エンティティは、店舗がある異なる地域や、買収などの異なるブランドの店舗を表すことなどが可能に
- Data quality（データ品質）ページでは、商品カタログとユーザーイベントデータの品質を評価し、Retail Search でどの検索パフォーマンス階層をアンロックしているかを表示


### [2023-06-28 Document AIのアップデート](https://cloud.google.com/release-notes#June_28_2023)

- 以下のOCR機能がGA
  - インテリジェントな文書品質分析
  - デジタルPDFからのネイティブテキスト
  - 記号レベルの抽出
  - 言語ヒント
- DOCXのサポートはプレビュー
  - 15ページまでのDOCXファイルを同期処理、または30ページまでのDOCXファイルを非同期処理可能
- doc.proto-to-vision.proto 変換ツールに修正を加え、Vision APIテキスト検出からドキュメントOCRへの移行を容易に

### [2023-06-28 Text to SpeehのStudio Voicesが一部のタグを除いてSSMLに対応](https://cloud.google.com/release-notes#June_28_2023)

- SSMLは音声合成マークアップ言語
- 対応から除外されているタグは、<mark>、<emphasis>、<prosody>、<lang>

### [2023-06-29 Anti Money Laundering AIがGAとなりv1が利用可能に](https://cloud.google.com/release-notes#June_29_2023)

- アンチマネーロンダリング（AML）AIは、人工知能（AI）を活用してマネーロンダリングを防止するサービス
- APIは以下の機能をサポート
  - engineConfigリソースによるモデルのチューニング
  - モデルを使ったバックテストと予測
  - エンジンコンフィグ、モデル、バックテスト、予測リソースからのメタデータのエクスポート

### [2023-06-28 Vertex AIでGoogleのユニバーサル音声モデル（USM）Chirpを使い始める](https://medium.com/google-cloud/getting-started-with-chirp-the-googles-universal-speech-model-usm-on-vertex-ai-f54edaf4da93)

- Chirpを利用する方法の公式解説記事