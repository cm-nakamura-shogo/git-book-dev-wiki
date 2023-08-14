# フロントエンド

## Books

- [2023-04-24 フロントエンド開発のためのテスト入門](https://www.amazon.co.jp/dp/B0BWR5GHMP/)
- [2022-04-22 プロを目指す人のためのTypeScript入門](https://gihyo.jp/book/2022/978-4-297-12747-3)
  - まあまあええらしい。入門～中級向け。
  - 書評
    - [「プロを目指す人のためのTypeScript入門」読書感想文 - Qiita](https://qiita.com/Yametaro/items/e3edba38d0fdc337e041)
- [2022-09-09 りあクト！ TypeScriptで始めるつらくないReact開発 第4版](https://klemiwary.com/blog/riakuto-4ed-release)
  - BOOTHで話題になっている

## Contents

- [JavaScript Primer](https://jsprimer.net/)
  - JavaScriptの入門コンテンツ

## Articles

- [2018-06-04 世のフロントエンドエンジニアにApollo Clientを布教したい - Qiita](https://qiita.com/seya/items/26c8a0dc549a10efcdf8)
- [2021-05-01 [JS] Fetch APIでFormDataをPOSTするときにContent-Typeを指定しないようにしよう。 - Qiita](https://qiita.com/YOCKOW/items/0b9635c62840998708f7)
  - content-typeには、`boundary=`も書いてあるのが正しいので、`multipart/form-data`だけ指定するとboundaryがサーバー側でわからなくなる。
  - ただしくは、`multipart/form-data; boundary=----hogehogehoge`が正なので。
  - これはJSの話だが他の言語でもあるかもしれないので注意。
- [2021-01-17 CSS in JS としてのChakra UI のススメ](https://zenn.dev/remon/articles/8d6f840a1d10e8)
- [2021-12-05 Utility-FirstなCSS,UIフレームワークを比較してみた(TailwindCSS, Chakra UI, MUI)](https://zenn.dev/kiyokiyoabc/articles/f688f2cee95f04)
  - Chakra UIとTailwindってケンカするんか？
  - この界隈やっぱよくわからん…
- [2022-02-16 N予備校とWebフロントエンドの新陳代謝 / iCARE Dev Meetup #30 - Speaker Deck](https://speakerdeck.com/berlysia/icare-dev-meetup-number-30)
  - 状態管理からAPIリクエストのキャッシュへ
- [2023-03-23 ZOZOTOWNのWebホーム画面をNext.jsでリプレイスして得た知見](https://techblog.zozo.com/entry/replacing-zozo-with-nextjs-knowledge)
  - SSRがあるとサーバーが必要になるという話
  - 基礎をチュートリアルやった後に読むと理解が深まる
- [2023-03-24 とってもやさしいフロントエンド入門](https://zenn.dev/sharefull_blog/articles/eeff318b5cecb4)
  - すごい入門。
  - これを読んだ後Next.jsチュートリアルで良いかと。
- [2023-04-10 javascriptでimport文周りを綺麗に保つTips](https://zenn.dev/dev_shun/articles/6210867c8a2528)
  - 気持ちは分かるがここまでやらんくても良いかなと思わないでもない
- [2023-04-15 俺たちのフロントエンド”大”自慢大会](https://dev.classmethod.jp/articles/20230414-findy-classmethod-frontend-event/)
  - 最も興味をひかれたのはbulletproof-reactかな
  - CRA前提なので、Next.jsの場合は、pages/featuresを持ってくる
  - 公式もそう言っている
    - [https://github.com/alan2207/bulletproof-react/issues/21](https://github.com/alan2207/bulletproof-react/issues/21)
  - その他、bulletproof-reactの紹介
    - [Reactベストプラクティスの宝庫！「bulletproof-react」が勉強になりすぎる件](https://zenn.dev/manalink_dev/articles/bulletproof-react-is-best-architecture)
    - [本気で考えるReactのベストプラクティス！bulletproof-react2022](https://zenn.dev/t_keshi/articles/bulletproof-react-2022)
- [2023-04-16 Next.js App Router (app ディレクトリ) の逆引き辞典](https://zenn.dev/yumemi_inc/articles/next-13-app-overview)
- [2023-04-17 (Next13 /app) React Server Components 時代の状態管理術【前編】](https://zenn.dev/rgbkids/articles/039333a5e74712)
- [2023-04-18 モノレポでstorybookを作成してAmplifyにデプロイ](https://dev.classmethod.jp/articles/storybook-amplify/)
  - 興味のある組み合わせだが、あまりわからない。
- [2023-04-21 【React】useMemo の使い時をまとめる](https://zenn.dev/chot/articles/react-when-to-use-memo)
  - ようするに親コンポーネントが再レンダリングされた場合に、子コンポーネントはキャッシュから計算する処理みたい
  - 子コンポーネントでuseMemoを使えばそのような動作となり、useMemoが依存する値が変化したときしか再計算しない
  - で、その前提で使いどころの基準を解説している
- [2023-04-22 React Tailwindのコンポーネントを生成するAIサービス](https://twitter.com/carlosknopel/status/1649450389190721537)
  - 実装はLangChainで実施されている
  - 日本語でも動くので、Tailwindの書き方調べるの面倒なときにええかも
- [2023-04-25 TypeScript開発に欠かせない？Zodライブラリの基本 | DevelopersIO](https://dev.classmethod.jp/articles/basic_usage_zod/)
  - お、Zod確かによさそう。
- [2023-04-25 React+ViteプロジェクトにStorybook（v7）を導入する | DevelopersIO](https://dev.classmethod.jp/articles/react-vite-storybook/)
- [2023-04-28 レスポンシブデザインで Tailwind CSS と CSS custom properties を併用する体験が良過ぎる](https://zenn.dev/amon/articles/9e8b7d220d2661)
- [2023-05-09 React Application Architecture for Production〜これ一冊で全てが網羅〜](https://zenn.dev/hrbrain/articles/437d0b7492ac47)
- [2023-05-11 Next.js 13のappディレクトリの基礎(Layout, Suspense, Data Fetching...) | アールエフェクト](https://reffect.co.jp/react/next-js-13-app/)
  - app routerについて
- [2023-05-15 ブログサイトを Next.js App Router に移行したので学びを書く | stin's blog](https://blog.stin.ink/articles/update-blog-site-with-next-app-router)
  - これもapp routerについて
- [2023-05-30 TypeScriptとVitestでユニットテストしてみた！ | DevelopersIO](https://dev.classmethod.jp/articles/ts-and-vitest-unittest/)
- [2023-06-16 Webアプリを個人開発した時に使用した便利なJavaScriptのライブラリを5つ紹介する - Qiita](https://qiita.com/hayaharu3220/items/1569d466db5f61fd5e8a)
- [2023-06-21 Panda CSS - Chakra UI の Zero Runtime CSS フレームワーク](https://zenn.dev/cybozu_frontend/articles/panda-is-coming)
  - 独自記法を除けば結構良さそう
  - 自分でカスタマイズできるRecipesなどは体験良さそうだった
- [2023-06-23 次世代のCSS in JS、Panda CSSをNext.js Appルーターで使用する](https://zenn.dev/a_da_chi/articles/725ba2cd4ce358)
  - React Server Componentsに対応するために独自開発したゼロランタイムCSS in JSとのこと
- [2023-06-27 【TypeScript】超実践的テクニック集【Reactなし】 - Qiita](https://qiita.com/ment_RE/items/9387b47dbef6433f6637)
- [2023-06-29 React/Next によるアプリケーション開発のこれから - Speaker Deck](https://speakerdeck.com/koba04/next-niyoruapurikesiyonkai-fa-nokorekara)
  - Next.js 13の話がまとまっている
- [2023-07-13 CSS・TypeScriptの相性が抜群。vanilla-extractが最高のCSS開発体験をくれた](https://zenn.dev/moneyforward/articles/vanilla-extract)
- [2023-07-20 Next.jsのいろいろなレンダリング方法を確認する | DevelopersIO](https://dev.classmethod.jp/articles/nextjs-rendering/)
  - かなり詳しくまとまっている
- [2023-07-26 技術選定の参考にbulletproof-reactを見てみる | DevelopersIO](https://dev.classmethod.jp/articles/bulletproof-react-library-selection/)
