# browser

## レンダリングの仕組み

- 60fpsに対応するには、js含めて毎秒16ms以内に収まれば良い

### フロー

- フローは、Parse > Style > Layout > Paint > Composite
- Parseでは、HTMLはDOM Treeに、CSSは Style Rulesに構文解析(パース)される
- Styleでは、DOM TreeとStyle Rulesの関連付けを行い、Render Treeを作成する(各要素はRendererと呼ばれる)
- Layoutでは、要素の位置と大きさなどを計算し、Layout Treeを作成する。
  - 最初はルートのRendererからレイアウト計算を順に行う
  - jsなどで変更があった場合は、その要素と子要素、兄弟要素の再計算が行われる。(Incremental Layout)
  - ブラウザ自体の幅が変えられた場合などは、Global Layoutが行われる
- Paintでは、要素の重なりを考慮し表示順を意識して描写できるようにする。この命令をPaint Recordsと呼ぶ。またモダンブラウザではここで、Layer Treeも作成する。
  - Layerの分離は変更の際の計算量を少なくするために有効
- Compositeでは、Paint Recordsを元に各レイヤーのピクセル単位で色を当て込む。

### スレッド構成

- レンダリングのスレッド構成は以下のようになっている。
  - Main Thread ... ParseからPaintまでを実行。加えてJavaScriptも実行する
  - Compositor Thread ... Raster Threadにレイヤのラスタライズ(ビットマップ化)を依頼し、一枚のレイヤを合成する。
  - Raster Thread ... 4つのスレッドでCompositor Threadからの依頼で処理をする。

### 変更と影響度合い

- 高さの変更は、Style以降のフローが再計算されて最も重い。
- 色はPaint以降が呼ばれ、軽いがMain Threadが使用される。
- transformやopacityは、compositeのみが実行され、Compositor Threadで実行される。
  - 実際はレンダリングエンジンによって微妙に異なり、WebkitではtransformプロパティでもLayoutから再計算される。

### レンダリングエンジン

- レンダリングエンジンは、ブラウザアプリ毎に異なる
- 主な違いは以下
  - Safari ... Webkit
  - Chrome ... Blink
  - Firefox ... Gecko
  - Edge ... EdgeHTML(今はChroniumベースとなったため、Blink)
- ただし、iOSのみWebkit以外のレンダリングエンジンは使用できない。
  - そのため、ChromeにiOSではWebkitを使用している。

### 参考記事

- [フロントエンジニアなら知っておきたいブラウザレンダリングの仕組みをわかりやすく解説！ | Tech Blog](https://blog.leap-in.com/lets-learn-how-to-browser-works/)
- [Webブラウザ、レンダリングエンジン、JavaScriptエンジンを整理して図視化してみた - Qiita](https://qiita.com/umashiba/items/8cb47825624c5cb043d6)
