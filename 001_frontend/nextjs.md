# Next.js


## NextAuth

- IdPによる認証機能を実装できるライブラリ。
- Google, GitHubなどのアカウントを使用したログインができる。
- 事前に各IdPのページで、CLIENT IDとCLIENT SECRETを取得する必要がある。

- 参考
  - [NextAuthでNext.jsに認証機能をサクッと実装するサンプルが無かったので作った](https://zenn.dev/thim/articles/7e3fc6a67de764daf50a)
    - hookやcallbacksについて解説あり。
    - IdPはGitHubを使っている。
  - [NextAuth.jsを使ったGoogle認証機能＋データベース(Prisma)の設定の理解](https://reffect.co.jp/react/next-auth)
    - IdPはGoogleを使った例。