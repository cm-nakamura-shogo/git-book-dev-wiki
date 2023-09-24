
## contents

- [2023-09-11 公開論文から学ぶ Google のテクノロジー : パート 3：データベース技術編 | Google Cloud 公式ブログ](https://cloud.google.com/blog/ja/products/gcp/google-technology-through-published-papers-part3/)
  - シリーズ紹介

## articles

- [2023-09-04 Cloud SpannerのData Boostを触ってみた | DevelopersIO](https://dev.classmethod.jp/articles/cloud-spanner-data-boost/)
  - Data Boostを有効化することでCloud Spannerが稼働しているコンピューティングとは独立したコンピューティングリソースを追加可能
  - これにより稼働中の環境に影響を与えることなく連携クエリを実行することが可能に
  - リードレプリカのようなもの???何が違うんだろう
  - ColossusはGFSの後継でいろんなサービスで使われているらしい（Guriさんいわく）

## updates

- [2023-08-14 Cloud Run release notes  |  Cloud Run Documentation  |  Google Cloud](https://cloud.google.com/run/docs/release-notes#August_14_2023)
  - Serverless VPC Accessコネクタなしで、VPCネットワークに直接トラフィックを送信できるようになりました（プレビュー）。
- [2023-08-29 Colab Enterprise release notes  |  Google Cloud](https://cloud.google.com/colab/docs/release-notes#August_29_2023)
  - Colab Enterpriseがプレビュー版で利用可能になりました。
  - Colab Enterpriseは、Colaboratoryの人気の高いコラボレーション機能とGoogle Cloudのセキュリティおよびコンプライアンス機能を組み合わせたものです。
  - Colab Enterpriseには以下が含まれます：
    - IAMアクセスコントロールによる共有およびコラボレーション機能。
    - 設定可能なランタイムテンプレートを備えたGoogleマネージドコンピュートおよびランタイムプロビジョニング。
    - Vertex AIおよびBigQueryとの統合。
    - Duet AIによるインラインコード補完機能
    - ノートブックコードを実行するためのエンドユーザー認証。
  - 始めるには、Colab Enterpriseの紹介を参照するか、ノートブックを作成してコーディングを開始してください。