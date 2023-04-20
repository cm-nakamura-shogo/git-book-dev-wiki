# アプリケーション開発


### [2023-04-18 JupyterにS3をブラウジングする拡張機能があるらしい](https://dev.classmethod.jp/articles/202304-jupyterhub_s3-md/)

### [2023-04-18 LocalStack 2.0がリリース](https://www.publickey1.jp/blog/23/awslocalstack_20.html)

- 無料で使えるオープンソース版では、Amazon S3やDynamoDB、AWS Lambdaなど主要なAPIが利用可能
- IAM、ElasticCache、Amazon RDS、Custom DNSなどは有償

### [2023-04-18 モノレポでstorybookを作成してAmplifyにデプロイ](https://dev.classmethod.jp/articles/storybook-amplify/)

- 興味のある組み合わせだが、あまりわからない。

### [2023-04-16 PythonのThreading Moduleについて](https://note.com/mega_gorilla/n/n101748d37b07)

- 使い方に関するまとめ記事

### [2023-04-15 俺たちのフロントエンド”大”自慢大会](https://dev.classmethod.jp/articles/20230414-findy-classmethod-frontend-event/)

- 最も興味をひかれたのはbulletproof-reactかな
- CRA前提なので、Next.jsの場合は、pages/featuresを持ってくる
- 公式もそう言っている
  - [https://github.com/alan2207/bulletproof-react/issues/21](https://github.com/alan2207/bulletproof-react/issues/21)
- その他、bulletproof-reactの紹介
  - [Reactベストプラクティスの宝庫！「bulletproof-react」が勉強になりすぎる件](https://zenn.dev/manalink_dev/articles/bulletproof-react-is-best-architecture)
  - [本気で考えるReactのベストプラクティス！bulletproof-react2022](https://zenn.dev/t_keshi/articles/bulletproof-react-2022)

### [2023-04-11 AWS / Google Cloud / Azure それぞれの推しサービス](https://dev.classmethod.jp/articles/developersio-day-one-favorite-services-aws-google-cloud-azure/)

### [2023-04-09 緊急解説！　突如出現したnitrogqlの中身と裏側](https://zenn.dev/uhyo/articles/nitrogql-beta-release)

### [2023-04-03 コードレビューを爆速にするための組織づくり](https://zenn.dev/hacobell_dev/articles/code-review-blocker)

- Working Agreementは大事やな。
  - チームメンバーはレビュー依頼を受けたら、それを優先タスクとする
  - レビューでコメントがあれば、レビュイーは返信と修正を優先タスクとする。意思疎通に時間がかかるようであればペアレビュー、モブプロを検討する
  - レビュイーはレビュアーにレビューの催促を Slack などでしてもよい
  - 当日にレビューをする時間が取れない場合、デイリースクラムなどで告知し、代わりにレビューをするメンバーを相談する
- 参照されいるラベルを付けるのも参考となるかも。

### [2023-03-24 とってもやさしいフロントエンド入門](https://zenn.dev/sharefull_blog/articles/eeff318b5cecb4)

- すごい入門。
- これを読んだ後Next.jsチュートリアルで良いかと。

### [2023-03-23 ZOZOTOWNのWebホーム画面をNext.jsでリプレイスして得た知見](https://techblog.zozo.com/entry/replacing-zozo-with-nextjs-knowledge)

- SSRがあるとサーバーが必要になるという話
- 基礎をチュートリアルやった後に読むと理解が深まる

### [2023-03-19 個人的 Finch CLI チートシート を作ってみた](https://dev.classmethod.jp/articles/the-finch-cli-cheat-sheet-v0-4-1/)

- Windows使いなので今のところ触る機会がない
- 標準になる可能性も秘めているので、いずれは使うことになるのかも。

### [2023-02-28「SaaS事業開発でやった10の失敗」](https://twitter.com/shin_sasaki19/status/1630432263359070208)

### [2022-12-29 熱量を失ったサーバーレスという世界（個人の所感） - Sweet Escape](https://www.keisuke69.net/entry/2022/12/29/135620)

### [2022-10-18 会議の目的は「課題を議論すること」ではない　参加者の「迷い」をなくす、会議のゴールの伝え方 - ログミーBiz](https://logmi.jp/business/articles/327653)

- これは良かったぞ。

### [2021-12-21 とってもやさしいGo言語入門](https://zenn.dev/sharefull_blog/articles/1fb628d82ed79b)

- 割と低レイヤになじみがない人向けなのかも

### [2021-05-13 30個以上の個人開発を失敗。そこから自分のサービスで生きていけるようになるまでの話。](https://note.com/iritec/n/n17c741c5f02d)

### [2021-05-01 [JS] Fetch APIでFormDataをPOSTするときにContent-Typeを指定しないようにしよう。 - Qiita](https://qiita.com/YOCKOW/items/0b9635c62840998708f7)

- content-typeには、`boundary=`も書いてあるのが正しいので、`multipart/form-data`だけ指定するとboundaryがサーバー側でわからなくなる。
- ただしくは、`multipart/form-data; boundary=----hogehogehoge`が正なので。
- これはJSの話だが他の言語でもあるかもしれないので注意。

### [2021-06-27 個人開発でwebサービスを作ったら人生で初めてバズった話](https://qiita.com/katsunory/items/4e7611b057c664781636)

### [2018-05-07 デスマーチが起きる理由 - ３つの指標](https://gist.github.com/voluntas/9c1d9d51e86a853fed6889f743a12145)

### [2018-07-13 ソーシャルゲームの価値を上げるログデータのつくりかた](https://blog.applibot.co.jp/2018/07/13/collecting-high-quality-log-in-social-game/)

- ゲームにおけるログデータとは
