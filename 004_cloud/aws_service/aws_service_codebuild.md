# AWS CodeBuild

## Docker Hubのpullが失敗する場合

非VPCなCodeBuildの場合、東京リージョンでは8つのグローバルIPが使いまわされている。

Docker Hubの匿名ユーザは6時間あたり100pullまでのため、これでは多くの場合、ビルドに失敗する。

そのためビルド処理内でDocker Hubログインする手順が解決策としてある。

- [“Too Many Requests.” でビルドが失敗する…。AWS CodeBuild で IP ガチャを回避するために Docker Hub ログインしよう！という話 | DevelopersIO](https://dev.classmethod.jp/articles/codebuild-has-to-use-dockerhub-login-to-avoid-ip-gacha/)