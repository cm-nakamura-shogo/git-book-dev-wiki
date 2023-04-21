# フロントエンド

### [2023-04-18 モノレポでstorybookを作成してAmplifyにデプロイ](https://dev.classmethod.jp/articles/storybook-amplify/)

- 興味のある組み合わせだが、あまりわからない。

### [2023-04-15 俺たちのフロントエンド”大”自慢大会](https://dev.classmethod.jp/articles/20230414-findy-classmethod-frontend-event/)

- 最も興味をひかれたのはbulletproof-reactかな
- CRA前提なので、Next.jsの場合は、pages/featuresを持ってくる
- 公式もそう言っている
  - [https://github.com/alan2207/bulletproof-react/issues/21](https://github.com/alan2207/bulletproof-react/issues/21)
- その他、bulletproof-reactの紹介
  - [Reactベストプラクティスの宝庫！「bulletproof-react」が勉強になりすぎる件](https://zenn.dev/manalink_dev/articles/bulletproof-react-is-best-architecture)
  - [本気で考えるReactのベストプラクティス！bulletproof-react2022](https://zenn.dev/t_keshi/articles/bulletproof-react-2022)

### [2023-03-24 とってもやさしいフロントエンド入門](https://zenn.dev/sharefull_blog/articles/eeff318b5cecb4)

- すごい入門。
- これを読んだ後Next.jsチュートリアルで良いかと。

### [2023-03-23 ZOZOTOWNのWebホーム画面をNext.jsでリプレイスして得た知見](https://techblog.zozo.com/entry/replacing-zozo-with-nextjs-knowledge)

- SSRがあるとサーバーが必要になるという話
- 基礎をチュートリアルやった後に読むと理解が深まる

### [2021-12-05 Utility-FirstなCSS,UIフレームワークを比較してみた(TailwindCSS, Chakra UI, MUI)](https://zenn.dev/kiyokiyoabc/articles/f688f2cee95f04)

- Chakra UIとTailwindってケンカするんか？
- この界隈やっぱよくわからん…

### [2021-05-01 [JS] Fetch APIでFormDataをPOSTするときにContent-Typeを指定しないようにしよう。 - Qiita](https://qiita.com/YOCKOW/items/0b9635c62840998708f7)

- content-typeには、`boundary=`も書いてあるのが正しいので、`multipart/form-data`だけ指定するとboundaryがサーバー側でわからなくなる。
- ただしくは、`multipart/form-data; boundary=----hogehogehoge`が正なので。
- これはJSの話だが他の言語でもあるかもしれないので注意。