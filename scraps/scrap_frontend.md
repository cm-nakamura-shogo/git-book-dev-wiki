# フロントエンド

### [2023-05-09 React Application Architecture for Production〜これ一冊で全てが網羅〜](https://zenn.dev/hrbrain/articles/437d0b7492ac47)

### [2023-04-28 レスポンシブデザインで Tailwind CSS と CSS custom properties を併用する体験が良過ぎる](https://zenn.dev/amon/articles/9e8b7d220d2661)

### [2023-04-25 React+ViteプロジェクトにStorybook（v7）を導入する | DevelopersIO](https://dev.classmethod.jp/articles/react-vite-storybook/)


### [2023-04-25 TypeScript開発に欠かせない？Zodライブラリの基本 | DevelopersIO](https://dev.classmethod.jp/articles/basic_usage_zod/)

- お、Zod確かによさそう。

### [2023-04-22 React Tailwindのコンポーネントを生成するAIサービス](https://twitter.com/carlosknopel/status/1649450389190721537)

- 実装はLangChainで実施されている
- 日本語でも動くので、Tailwindの書き方調べるの面倒なときにええかも

### [2023-04-21 【React】useMemo の使い時をまとめる](https://zenn.dev/chot/articles/react-when-to-use-memo)

- ようするに親コンポーネントが再レンダリングされた場合に、子コンポーネントはキャッシュから計算する処理みたい
- 子コンポーネントでuseMemoを使えばそのような動作となり、useMemoが依存する値が変化したときしか再計算しない
- で、その前提で使いどころの基準を解説している

### [2023-04-18 モノレポでstorybookを作成してAmplifyにデプロイ](https://dev.classmethod.jp/articles/storybook-amplify/)

- 興味のある組み合わせだが、あまりわからない。

### [2023-04-17 (Next13 /app) React Server Components 時代の状態管理術【前編】](https://zenn.dev/rgbkids/articles/039333a5e74712)

### [2023-04-16 Next.js App Router (app ディレクトリ) の逆引き辞典](https://zenn.dev/yumemi_inc/articles/next-13-app-overview)

### [2023-04-15 俺たちのフロントエンド”大”自慢大会](https://dev.classmethod.jp/articles/20230414-findy-classmethod-frontend-event/)

- 最も興味をひかれたのはbulletproof-reactかな
- CRA前提なので、Next.jsの場合は、pages/featuresを持ってくる
- 公式もそう言っている
  - [https://github.com/alan2207/bulletproof-react/issues/21](https://github.com/alan2207/bulletproof-react/issues/21)
- その他、bulletproof-reactの紹介
  - [Reactベストプラクティスの宝庫！「bulletproof-react」が勉強になりすぎる件](https://zenn.dev/manalink_dev/articles/bulletproof-react-is-best-architecture)
  - [本気で考えるReactのベストプラクティス！bulletproof-react2022](https://zenn.dev/t_keshi/articles/bulletproof-react-2022)

### [2023-04-10 javascriptでimport文周りを綺麗に保つTips](https://zenn.dev/dev_shun/articles/6210867c8a2528)

- 気持ちは分かるがここまでやらんくても良いかなと思わないでもない

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