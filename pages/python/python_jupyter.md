# jupyter

## 起動コマンド

- localhostアクセスする場合に必要な最低限のコマンド

```shell
jupyter lab --port=8888 --ip=0.0.0.0 --allow-root --NotebookApp.token=''
```

## markdownの表を全体左に寄せる。

- 冒頭に以下のhtmlを書く。
```
%%html
<style>
table {float:left}
</style>
```

## コンソールコマンドに変数を渡す方法

- https://qiita.com/piruty/items/9c4f87cc2240e1028b31

## nbdime

* jupyter環境上でnotebook同士の差分を良い感じに表示してくれる。
* gitとの連携も可能(だが、labではうまくextensionが認識されなかった...)

* install
```
$ pip install nbdime
```

* nbdime単体で使う場合はこんな感じで、GUIが立ち上がる。なお編集はできない。
```
$ nbdiff-web notebook1.ipynb notebook1.ipynb
```

* 参考
  * [Jupyter Notebook ファイルのままdiffをとったり、マージしたり出来るツール nbdime - Qiita](https://qiita.com/nannoki/items/490c8d999ed400f78197)

## nbconvert

### notebookをmarkdownに変換する

以下により同名のmarkdownファイルが作成される。

```sh
jupyter nbconvert --to markdown sample.ipynb
```

## JupyterHub

- [AmazonLinux2にJupyterHubを構築する | DevelopersIO](https://dev.classmethod.jp/articles/al2-jupyterhub/)