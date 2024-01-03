
### インストール

以下にそってインストールします。

- https://docs.rancherdesktop.io/getting-started/installation

### 基本用語

コンテナはイメージとインスタンスがあります。

コンテナイメージは作成済みの実行環境の定義ようなもので、実際に動かすにはイメージを元にしてインスタンスを実行します。

### 基本的なコマンド

- pull : イメージを取得します。

```bash
# docker pull <REPOSITORY>:<TAG>
docker pull ubuntu:latest
```

- images : pullやbuild済みのイメージ一覧を確認します。

```bash
docker images
```

- run : イメージからインスタンスを起動します。
    - -i : interactiveオプションです。ホスト側の入力をコンテナに伝えることができます。
    - -t : ttyオプションです。コンテナの出力をホスト側に伝えることができます。
    - -d : daemonオプションです。バックグラウンドで実行ができます。

```bash
# docker run -itd --name <CONTAINER_NAME> <REPOSITORY>:<TAG> bash
docker run -itd --name sample ubuntu:latest bash # 一例
```

- ps : 起動済みのインスタンス一覧を確認します。

```bash
docker ps # running中のものだけ見たい場合
docker ps -a # 停止中のものを含めてみたい場合
```

- exec : 起動中のインスタンスの中に入ります。

```bash
# docker exec -it <CONTAINER_NAME> bash
docker exec -it sample bash
```

- exit : execで入ったのちにログアウトします（dockerコマンドではない）
- logs : 起動中のインスタンスのログを確認します。

```bash
# docker logs <CONTAINER_NAME>
docker logs sample
```

- inspect : 起動中のインスタンスの設定を確認します。

```bash
# docker inspect <CONTAINER_NAME>
docker inspect sample
```

- stop : インスタンスを停止します。

```bash
# docker stop <CONTAINER_NAME>
docker stop sample
```

- rm : インスタンスを削除します

```bash
# docker rm <CONTAINER_NAME>
docker rm sample
```

- rmi : イメージを削除します。

```bash
# docker rmi <REPOSITORY>:<TAG>
docker rmi ubuntu:latest
```

- prune : 未使用のイメージやインスタンスをまとめて削除します。

```bash
docker image prune
docker container prune
```

その他よく使うコマンドは以下を参照ください。

- [よく使うDockerコマンド #Docker - Qiita](https://qiita.com/noralife/items/18301143c20cc5172c56)

### イメージを作る

自分でイメージを作るには以下の手順を踏みます。

- Dockerfileを書く
- docker buildをする

詳細は以下でも

- [はじめてのDockerfile #Docker - Qiita](https://qiita.com/suzu12/items/c4bc47c0df6ec9b9290b)

### Dockerfileの分かりにくい部分

- ADDとCOPYの違い
    - [Dockerfile の ADD と COPY の違いを結論から書く #Docker - Qiita](https://qiita.com/YumaInaura/items/1647e509f83462a37494)
    - [DockerfileにてなぜADDよりCOPYが望ましいのか #Docker - Qiita](https://qiita.com/momotaro98/items/bf34eef176cc2bdb6892)
- CMDとENTRYPOINTの違い
    - [DockerfileのCMDとENTRYPOINTを改めて解説する #Docker - Qiita](https://qiita.com/uehaj/items/e6dd013e28593c26372d)

### docker composeとは

Dockerfileはあくまでイメージの定義を記載できます。

複数のイメージのビルドや実行時の設定をファイルで書きたい場合、docker composeを使います。

詳細は以下でも

- [はじめてのDocker compose #PHP - Qiita](https://qiita.com/suzu12/items/4ec2cc8c1a7c23aa112b)

## その後

他のコンテンツを興味に応じてやってみましょう。