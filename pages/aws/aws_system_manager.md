# AWS Systems Manager

SSMと呼ばれることが多い。

その他いろんな機能があるものの、プライベートなVPCにあるインスタンスに接続するために使われることが多い。

パラメータストアなども良くつかわれる。

## 参考

### [2020-03-30【AWS Systems Manager】パッチマネージャーの パッチベースライン と パッチグループ の概念を勉強する | DevelopersIO](https://dev.classmethod.jp/articles/patchmanager-baseline-and-group/)

### [2023-01-09 VSCodeのRemote SSH環境構築方法](https://dev.classmethod.jp/articles/how-to-use-vscode-remote-ssh-with-aws-systems-manager/)

プライベートなEC2を例といた構成

## アップデート

### [2023-04-24 Application ManagerがCDKアプリケーションのサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/aws-systems-manager-cloud-development-kit-cdk-applications/)

Application Managerは、Amazon CloudWatchおよびAWS Configとの統合により、コンソールからアプリケーションの運用状況、メトリクス、およびコンプライアンスを監視できる機能。

これがCDKのアプリケーションでも使用可能となった。