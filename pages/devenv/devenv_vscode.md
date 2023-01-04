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
  - Japanese Language Pack : 日本語化。時々英語に戻るので以下で設定する。
  	```
	既定の UI 言語をオーバーライドするには、Configure Display Language コマンドを使用して、VS Code の表示言語を明示的に設定します。
	Ctrl+Shift+P を押して "コマンド パレット" を表示し、display と入力して Configure Display Language コマンドをフィルターして表示します。
	Enter キーを押すと、インストールされている言語の一覧がロケールごとに表示され、現在のロケールが強調表示されます。
	UI 言語を切り替えるには、別の "ロケール" を選択してください。
	```

- 視認性
  - Brancket Pair Colorizer2 : カッコを色分けしてくれる。VSCodeのデフォルトで色分けされるようになったので、今はdepricated。
  - indent-rainbow : インデントを色分けしてくれる。
  - Rainbow CSV : CSVの視認性向上。
  - Trailing Space : 空白を可視化する。
  - Error Lens : エラーの内容をエディタで見えるようにしてくれる（マウスオーバーする必要がない）

- Git
  - Git Graph : 変更履歴がツリーで見れる。
  - GitLens : ブランチ同士の差分確認で主に使う。実はあまり使いこなせたことが無い。

- Python
  - Python : Python開発の基本。
  - Pylance : 構文チェックや候補を頭良く表示する。今はPythonプラグインを入れると勝手に入る気がする。
  - Python Docstring Generator : Pythonのdocstringを自動生成できる。
  - isort : importをPEP8準拠にしてくれる拡張機能

- Markdown
  - Markdown PDF ... MarkdownをPDF変換する。
  - Markdown Preview Enhanced ... Markdownの表示が見やすくなる。
  - Draw.io ... 図を書ける。*.drawio.svgで保存すれば、markdownに埋め込める。
  - PlantUML ... UMLを記述できる。図として出力し、markdownに埋め込める。
    - 出力先はデフォルトはoutになるが、以下の設定で変更できる。
    ```json
    "plantuml.exportOutDir": "plantuml"
    ```
  - Paste Image ... クリップボードからmarkdownに画像を張り付けられる。
    - 以下に使い方と推奨設定があるのでご参考。
      - https://zenn.dev/ktechb/articles/968ff79f8f9c46a26ee5

- フォーマッター
  - Prettier ... 自動整形ツール。あまりメリットをまだ感じられていないが、嬉しいのだろうか。

- リモート系
  - Remote SSH ... VSCodeからサーバーにSSH接続できる。
  - Remote Containers
  - Remote WSL

- フロントエンド
  - Auto Close Tag ... htmlタグを自動で閉じる。
  - Auto Rename Tag ... htmlタグを自動でリネームできる。
  - JavaScript (ES6) code snippets ... JavaScript用
  - ES7 React/Redux/GraphQL/React-Native snippets ... React開発用
  - ESlint ... linter
  - Vetur ... Vue開発用

- クラウド
  - Azure Account / Azure App Service / Azure Resources

## Snippetの使い方

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

### カーソル移動

|||
|:---|:---|:---|
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