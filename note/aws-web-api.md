
結局何をどこに置くのが最適か分かっていない。

いまMSAでは以下を検討している。

- Amplify + APIGW + ECS(Fargate)

これ以外の選択肢について考察。

## Next.js on App Runner

App Runnerは、Next.jsをきちんとSSRで動かすには有用だと思うが、バックエンドにPythonなどを立てることを想定していない気がする。

JavaScriptで全部書くのならアリなのかもしれない。

将来的に以下のように出来たらよいが難しいのかも。。。

- Front: App Runner(Next.js) in Public
- Back: App Runner(Python) in Private

認証はNext.js上で行い、APIはPrivate Subnetで守る想定。

いや以下なら結構良いのかもしれない。

- Front: App Runner(Next.js) in Public
- Back: ECS Fargate(Python) in Private

以下参考

- [AWS App Runner VPC - AWS Copilot CLI](https://aws.github.io/copilot-cli/ja/blogs/apprunner-vpc/)

## Next.js on ECS

FargateにNext.jsを置く例も稀にある。

- [Next.jsをECS/Fargateにデプロイする（Docker環境構築編） #AWS - Qiita](https://qiita.com/kenji7157/items/79998e3b458f3d28ac58)

静的サイトをわざわざサーバーに置く点がデメリットかもしれない。

この構成の場合

- Front: ELB + ECS(Next.js) in Public
- Back: ECS(Python) in Private

という感じになるか？スケーラビリティを置いて置く場合はありなのかもしれない

認証はNext.js上で行い、APIはPrivate Subnetで守る想定。

## Next.js on Amplify

現在検討中の構成。

- Front: Amplify(Next.js) in Public
- Back: APIGW + ECS(Python) in Public

この構成の場合、BackもPublicとなる。

認証はAmplifyとAPIGWで共有し、Cognitoを使っている。

デプロイは少し手間らしいので、開発環境は考えないといけないらしい。

あとAmplifyの認証にGoogleが使用できるか少し調査が必要。
