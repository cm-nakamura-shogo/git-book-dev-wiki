# VSCode

## 日本語フォント設定

- HackGen
  - 色々試したが、HackGenが英文字がつぶれなくてかなり良い。
    - https://github.com/yuru7/HackGen/releases

- 以下は検討したが、英文字がつぶれてカクカクしてしまう。(解像度のせいかもしれんが)
  - Myrica
    - Myrica / MyricaMを以下よりダウンロード。
      - https://myrica.estable.jp/

    - zip解凍し、ttcファイルをダブルクリックしていインストール。

  - Ricty Diminished
    - https://github.com/edihbrandon/RictyDiminished

- 設定反映
  - VSCodeのフォントを設定し、VSCodeを再起動。

## プラグイン

- 基本
  - [Japanese Language Pack](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ja)
    - 日本語化。時々英語に戻るので以下で設定する。
      ```
      既定の UI 言語をオーバーライドするには、Configure Display Language コマンドを使用して、VS Code の表示言語を明示的に設定します。
      Ctrl+Shift+P を押して "コマンド パレット" を表示し、display と入力して Configure Display Language コマンドをフィルターして表示します。
      Enter キーを押すと、インストールされている言語の一覧がロケールごとに表示され、現在のロケールが強調表示されます。
      UI 言語を切り替えるには、別の "ロケール" を選択してください。
      ```

- 編集補助
  - [Insert Numbers](https://marketplace.visualstudio.com/items?itemName=Asuka.insertnumbers)
    - マルチカーソルで文字列をフォーマット指定して連番を入力できる。
  - [change-case](https://marketplace.visualstudio.com/items?itemName=wmaurer.change-case)
    - 選択範囲を特定のchaseに変更する。
    - snake_caseやkebab-caseなど。

- 視認性
  - [indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)
    - インデントを色分けしてくれる。
  - [Rainbow CSV](https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv)
    - CSVの視認性向上。
  - [Trailing Space](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
    - 空白を可視化する。
  - [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)
    - エラーの内容をエディタで見えるようにしてくれる（マウスオーバーする必要がない）
  - Brancket Pair Colorizer2
    - カッコを色分けしてくれる。
    - VSCodeのデフォルトで色分けされるようになったので、今はdepricated。

- Git
  - [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
    - 変更履歴がツリーで見れる。
  - [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
    - ブランチ同士の差分確認やファイル別の変更履歴の確認に主に使っている。
    - フルの機能は実は使いこなせてない気もしている。

- Python
  - [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
    - Python開発の基本。
  - [autoDocstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring)
    - Pythonのdocstringを自動生成できる。
  - [isort](https://marketplace.visualstudio.com/items?itemName=ms-python.isort)
    - importをPEP8準拠にしてくれる拡張機能
  - Pylance
    - 構文チェックや候補を頭良く表示する。
    - 今はPythonプラグインを入れると含まれるため個別に入れなくてよい。

- Markdown
  - [Markdown PDF](https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf)
    - MarkdownをPDF変換する機能
  - [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
    - Markdownのプレビュー表示が見やすくなる。
  - [Draw.io Integration](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)
    - drawioの図を書ける。
    - *.drawio.svgで保存すれば編集も可能で、そのままmarkdownにも埋め込める。
  - [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)
    - UMLを記述できる。図として出力し、markdownに埋め込める。
    - 出力先はデフォルトはoutになるが、以下の設定で変更できる。
      ```json
      "plantuml.exportOutDir": "plantuml"
      ```
    - ある程度GitHubなどの描画側で対応しているところが出始めてるので、使わずに済む将来が来ると良いなと思っている。
  - [Paste Image](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image)
    - クリップボードからmarkdownに画像を張り付けられる。
    - Snipping Toolとの連携で結構良い。
    - 以下に使い方と推奨設定があるのでご参考。
      - https://zenn.dev/ktechb/articles/968ff79f8f9c46a26ee5

- フォーマッター
  - [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
    - 自動整形ツール。
    - あまりメリットをまだ感じられていないが、チーム開発では嬉しいらしい。
    - TS界隈の開発者は使ってるのをよく見るが、Pythonで使ってる人をあまり見たことがない。

- リモート系
  - [Remote SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
    - VSCodeからサーバーにSSH接続できる。
    - サーバー上のフォルダもVSCodeでオープンすることが可能
  - [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
    - 上記のWSL版
    - 実はあまり詳しくない。
  - [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
    - コンテナ開発で使うやつ。実はあまり詳しくない。

- フロントエンド
  - [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)
    - htmlタグを自動で閉じる。
  - [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)
    - htmlタグを自動でリネームできる。
  - [JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)
    - JavaScript開発用（詳細よくわかってない）
  - [ES7+ React/Redux/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
    - React開発用（詳細よくわかってない）
  - [ESlint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
    - linter
  - [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur)
    - Vue開発用（詳細よくわかってない）

- Azure関連
  - [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)
  - [Azure App Service](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice)
  - [Azure Resources](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureresourcegroups)

## コードスニペットの使い方

- Visual Studio Codeに定型文（スニペット）を登録する方法
  - https://slash-mochi.net/?p=1978

- VSCodeのUser Snippetを活用しよう！
  - https://qiita.com/282Haniwa/items/82828c6a566e3e7e047d

- snippetの例(styled componentなコンポーネントクラス)
```json
{
	// Place your snippets for javascriptreact here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"description": "Log output to console"
	// }
	"react component": {
		"prefix": "react component",
		"body":[
			"import React from 'react'",
			"import styled from 'styled-components'",
			"",
			"// Props",
			"type ComponentProps = {",
			"  className: string",
			"} & $1Props",
			"",
			"// DOM",
			"const Component: React.VFC<ComponentProps> = props => (",
			"  <div className={props.className}>",
			"  </div>",
			")",
			"",
			"// Style",
			"const StyledComponent = styled(Component)`",
			">",
			"`;",
			"",
			"// Props",
			"type $1Props = {",
			"}",
			"",
			"// Container",
			"export const $1: React.FC<$1Props> = props => {",
			"",
			"  return (",
			"    <StyledComponent",
			"      className=\"rootContainer\"",
			"    />",
			"  )",
			"}",
		],
		"description": "react component template",
	},
}
```

## ショートカット

意外と網羅できてないショートカットを自分なりに整理する。

### ウィンドウ移動

|||
|:---|:---|
|Ctrl + 数字|複数ウィンドウを移動|
|Ctrl + Tab|タブ移動|

### カーソル移動

|||
|:---|:---|
|Ctrl + 左右|単語毎カーソル移動|
|Ctrl + Home|行頭移動|
|Ctrl + End |行末移動|

### マルチカーソル

いくつかやり方がある。

- マウスを使用する方法
  - Alt + マウスクリック
  - マウス中芯ボタンクリックのドラッグ
  - Shift + Alt + マウスの右クリックドラッグ
- マウスなしで実行可能な方法
  - Alt + Ctrl + 上下
  - 単語選択 ⇒ Ctrl + D （検索しながらカーソルを増やせる）

### 編集操作

|||
|:---|:---|
|Alt + 上下|行移動|

### 参考

- [VSCodeのマルチカーソル練習帳 - Qiita](https://qiita.com/TomK/items/3b1f5be07d708d7bd6c5)
