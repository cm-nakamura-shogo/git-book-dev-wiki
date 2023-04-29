# AWS Systems Manager

SSMと呼ばれることが多い。

その他いろんな機能があるものの、プライベートなVPCにあるインスタンスに接続するために使われることが多い。

パラメータストアなども良くつかわれる。

## VSCodeのRemote SSH環境構築方法

プライベートなEC2を例といた構成

- [AWS Systems Manager と VS Code Remote SSH を組み合わせて快適なリモート開発環境を作る方法 | DevelopersIO](https://dev.classmethod.jp/articles/how-to-use-vscode-remote-ssh-with-aws-systems-manager/)

## アップデート

### [2023-04-24 Application ManagerがCDKアプリケーションのサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-systems-manager-cloud-development-kit-cdk-applications/)

Application Managerは、Amazon CloudWatchおよびAWS Configとの統合により、コンソールからアプリケーションの運用状況、メトリクス、およびコンプライアンスを監視できる機能。

これがCDKのアプリケーションでも使用可能となった。