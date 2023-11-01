

## OAuth, OIDCの前提

これは前提に見ておくとよい。

- [OAuth & OIDC 入門編 by #authlete - YouTube](https://www.youtube.com/watch?v=PKPj_MmLq5E)

以下は参考に。

- [OCHaCafe#5 - 避けては通れない！認証・認可 | PPT](https://www.slideshare.net/oracle4engineer/ochacafe5)
- [マイクロサービスの認証・認可とJWT / Authentication and Authorization in Microservices and JWT - Speaker Deck](https://speakerdeck.com/oracle4engineer/authentication-and-authorization-in-microservices-and-jwt)
- [O'Reilly Japan - OAuth 2.0をはじめよう](https://www.oreilly.co.jp/books/9784873115580/)
- [OAuth 2.0 全フローの図解と動画 - Qiita](https://qiita.com/TakahikoKawasaki/items/200951e5b5929f840a1f)

## User pool作成

大枠以下の設定で作成

- User pool名 : cm-nakamura-user-pool
- ドメイン名 : https://cm-nakamura-user-pool.auth.ap-northeast-1.amazoncognito.com
- Hosted UI : 使用する
- 認証フロー : USER_SRP_AUTH, ALLOW_REFRESH_TOKEN_AUTH
- OAuth 付与タイプ : 認証コード付与
- クライアント名 : sample-client

「認証コード付与」はいわゆるいわゆる認可コードフロー（RFC 6749, [4.1. Authorization Code Grant](https://tools.ietf.org/html/rfc6749#section-4.1)）と思われる

各フローについては以下を参照

- [OAuth 2.0 全フローの図解と動画 - Qiita](https://qiita.com/TakahikoKawasaki/items/200951e5b5929f840a1f)

USER_SRP_AUTHについての詳細配下を参照

- [Cognito の USER_SRP_AUTH を Python で理解したい - 魂の生命の領域](https://kesumita.hatenablog.com/entry/cognito-srp-auth-python)

認証フローを調べてて以下がでてきたが、あきらかに認可フローの話をしている？

- [Amazon Cognito user pools の認証フロー | 豆蔵デベロッパーサイト](https://developer.mamezou-tech.com/blogs/2023/01/23/amazon-cognito/)

## ユーザの作成

マネコンからユーザを作成できるので`nakamura.shogo@classmethod.jp`で作成。

パスワードが記載されたメールが届く。

## テスト

その後、以下のようなURLにアクセス

- https://cm-nakamura-user-pool.auth.ap-northeast-1.amazoncognito.com/login?response_type=code&client_id=2ssgm0mf04sf7081eg8t5uegd7&redirect_uri=https://www.google.com

上記で届いたパスワードでログインする。

redirect_uriは、そのclient_idで登録したものと一致しておく必要があるようだ。

## Hosted UIのカスタマイズ

Hosted UIを使用するからと言ってカスタマイズできないという話ではないらしい。（実際、Amplifyを使うと画面が変わったりする）

マネジメントコンソールからCSSを設定することができる。

## Hosted UIを使う意味

UIが準備されるというだけではなく、OAuth / OIDCに一部準拠していることも特徴。

逆にHosted UIを使わない場合、どのようなフローになるのかまだわかっていない。

Hosted UIの動作は以下が参考となる。

- [AmplifyでCognitoのHosted UIを利用した認証を最低限の実装で動かしてみて動作を理解する | DevelopersIO](https://dev.classmethod.jp/articles/learn-authentication-using-cognitos-hosted-ui-with-amplify/#toc-17)

触ってみるなら以下も

- [Cognitoで学ぶ認証・認可 in AWS - Qiita](https://qiita.com/saki-engineering/items/b327f93fe7f027913bd7)

## USER_SRP_AUTHについて

Black Beltの資料によれば、直接アクセストークンがクライアント側で得られる。

アクセストークンが盗まれることがないか少し心配である

- [20200630_AWS_BlackBelt_Amazon_Cognito_ver2.pdf](https://pages.awscloud.com/rs/112-TZM-766/images/20200630_AWS_BlackBelt_Amazon_Cognito_ver2.pdf)

とりあえずp.49にあるようなフローで判断すると、外部IdPは使わないのでUIを独自にしたいのであれば「Cognito Identity Provider API」を使うしかなさそう。


## 参考

- [2019-10-17 OAuth 2.0 の勉強のために認可サーバーを自作する - Qiita](https://qiita.com/TakahikoKawasaki/items/e508a14ed960347cff11)
- [2023-05-03 最適な認証基盤を構築する (Amazon Cognito調査編) | つかびーの技術日記](https://tech-blog.tsukaby.com/archives/1551)
