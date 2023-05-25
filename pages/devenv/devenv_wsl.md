# WSL

## install

- https://docs.microsoft.com/ja-jp/windows/wsl/install-manual#step-3---enable-virtual-machine-feature

## aptが遅い場合

```
$ sudo sed -i.org -e "s/\/\/archive\.ubuntu\.com/\/\/jp\.archive\.ubuntu\.com/g" /etc/apt/sources.list
```

## 良く使うコマンド

- 今のWSL一覧を確認
```powershell
> wsl -l -v
> wsl --list --verbose
```

- 稼働中のWSLのバージョンを2に変更
```powershell
> wsl --set-version Ubuntu-20.04 2
```

- デフォルトバージョンをWSL2に変更
```powershell
> wsl --set-default-version 2
```

- デフォルトのWSLをUbuntu-20.04に変更
```powershell
> wsl --set-default Ubuntu-20.04
```

- WSLのシャットダウン
```powershell
> wsl --shutdown
```

## Pythonセットアップ

pyenvを落としてくる。

```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

pyenvのビルド

```
sudo apt install -y gcc make
cd ~/.pyenv && src/configure && make -C src
```

pyenvの環境変数設定

```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
```

ここでターミナルを再起動

pipを入れる

```
sudo apt install python3-pip
```

以下でPythonの依存ライブラリをインストール

- [https://github.com/pyenv/pyenv/wiki#suggested-build-environment](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)

```
sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```


```
pyenv install --list | grep "3.10"
pyenv install 3.10.11
pyenv versions
```

pipenvを入れる

```
sudo apt install python3-testresources
pip3 install pipenv
```

ターミナル再起動

```
pipenv --version
>> pipenv, version 2023.5.19
```

とはええ感じに

参考

- [pyenvとpoetryでディレクトリ毎にPython環境を切り替える手順＋ノウハウまとめ | DevelopersIO](https://dev.classmethod.jp/articles/pyenv-and-poetry/)
- [Pipenvを使ったPython開発まとめ - Qiita](https://qiita.com/y-tsutsu/items/54c10e0b2c6b565c887a)

## AWS CLI

以下に従う

- [AWS CLI の最新バージョンをインストールまたは更新します。 - AWS Command Line Interface](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)

## Terraform

以下に従う

- [Install | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/downloads)