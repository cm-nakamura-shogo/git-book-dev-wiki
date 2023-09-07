

## Books

- [2022-10-12 情報セキュリティの敗北史](https://www.amazon.co.jp/dp/4826902433)
  - 概念を先に理解しておくのはとても良さそう。
  - 書評
  - [https://note.com/ichi_twnovel/n/nbeb9923a8c94](https://note.com/ichi_twnovel/n/nbeb9923a8c94)

## Contents

- [全員がOAuth2.0を理解しているチームの作り方](https://dev.classmethod.jp/articles/devio2021-learning-oauth/)
- [マイクロサービスの認証・認可とJWT / Authentication and Authorization in Microservices and JWT - Speaker Deck](https://speakerdeck.com/oracle4engineer/authentication-and-authorization-in-microservices-and-jwt)
  - JWTどころかOAuth2、OpenID Connectについても分かりやすい
  - OAuth2は認可プロトコルの話で、認可コードグラントが推奨方式。認証目的であればOpenID Connectを使用する。
  - OAuth2ではアクセストークンが認可サーバーから発行されるが、認可コードグラント方式では認可コードを使ってクライアントがアクセストークンを取得する
  - OpenID ConnectにはIDトークンが含まれ、iss:誰が(IdP)、sub:誰を(ex. エンドユーザ)、aud:誰のために(Relying Party)などの認証に必要な項目を含む
  - アクセストークンとIDトークンの違いはaudが異なり、アクセストークンはリソースサーバーが、IDトークンはクライアント(Relying Party)がそれぞれaudとなる
  - 認可コードフローにより、アクセストークンとIDトークンをクライアント(Relying Party)で取得する
