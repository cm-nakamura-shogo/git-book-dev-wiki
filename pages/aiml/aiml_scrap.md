# note

## NeuralODE

層の方向を連続化してResNetを一つの常微分方程式で表す研究

- [Neural ODEの紹介 - Qiita](https://qiita.com/yu_og/items/13501755e22f5f035dc8)
- [Normalizing Flow入門 第7回 Neural ODEとFFJORD - tatsyblog](https://tatsy.github.io/blog/posts/2021/2021-01-11-normalizing_flow%E5%85%A5%E9%96%80_%E7%AC%AC7%E5%9B%9E/)

## 一般

- 敵対的学習を使う場合、活性化関数を修正した方が良いかもしれないという話
  - https://ai-scholar.tech/articles/adversarial-perturbation/smooth-adversarial-training
* Poincare Embeddings
  * [異空間への埋め込み！Poincare Embeddingsが拓く表現学習の新展開 - ABEJA Tech Blog](https://tech-blog.abeja.asia/entry/poincare-embeddings)
  * 双曲空間に埋め込めば非常に低次元で表現できる埋め込みベクトル。

## バイオ系

- PyMOLが使われることが多いようだ。
  - https://hira-labo.com/archives/209
  - https://hira-labo.com/archives/1882
  - https://hira-labo.com/archives/1544

## Kaggle

- KaggleのH&Mのレコメンド、良コンペだったという噂が聞こえてきます。
  - 候補抽出⇒並べ替えの2stageレコメンドが上位ランク
  - 特徴量の作りこみが大事で、NNは微妙だったようだ
  - https://yng87.github.io/blog/2022/05/kaggle_hm/
  - https://zenn.dev/zerebom/articles/9e6bad764d3f97

## 時系列データ

- SREのためのシステム障害における異常検知
  - https://speakerdeck.com/yuukit/sre-next-2022

## ライブラリ

- cuml
  - sklearnをGPUで高速にしたnvidiaのライブラリ
  - https://github.com/rapidsai/cuml

## CV

- ShakeDrop
  - https://qiita.com/yu4u/items/a9fc529c85534eca11e5
  - パラメータの更新方法に関するもの。

## PythonでOCR(Tesseract + PyOCR)

- https://rightcode.co.jp/blog/information-technology/python-tesseract-image-processing-ocr

## pdftoppm(PDFを画像に変換)

- https://atmarkit.itmedia.co.jp/ait/articles/1903/08/news039.html

## 参考

- Alammar氏によるTransformerのvisual解説
  - http://jalammar.github.io/illustrated-retrieval-transformer/


# TabPFN

- https://arxiv.org/abs/2207.01848v3

```
12層、埋め込みサイズ512、フィードフォワード層の隠れサイズ1024、4頭注目のPFN Transformerのみを考慮しました。我々は、線形ウォームアップとコサインアニーリング（Loshchilov and Hutter, 2017）を備えたAdam optimizer（Kingma and Ba, 2015）を使用した。各トレーニングについて、3つの学習率{.001, .0003, .0001}のセットをテストし、最終的なトレーニング損失が最も低いものを使用しました。結果として得られたモデルは25.82Mのパラメータを含んでいる。

最終的なモデルは、512データセットのバッチサイズで18 000ステップの学習を行いました。つまり、我々のTabPFNは、9 216 000の合成されたデータセットで学習される。この学習は、8つのGPU（Nvidia RTX 2080 Ti）で20時間かかります。各データセットは1024の固定サイズであり、一様にランダムに学習と検証に分割しました。一般に、学習曲線は1000万データセット程度で平坦になる傾向があり、一般に非常にノイズが多いことが確認されました。おそらく、これは我々の事前処理で多種多様なデータセットが生成されるためと思われます。

TabPFNは、学習サイズが1024を超えるデータセットには向いていません。予測に時間がかかったり、信頼性が落ちたりする可能性がある。10kサンプル以上のデータセットを実行しないことをお勧めします。マシンがクラッシュする可能性があります（TabPFNの2次関数的なメモリスケーリングのため）。フィット関数にoverwrite_warning=Trueを渡して、実行するかどうか確認してください。

TabPFNは、合成データセットで事前学習されたオープンソースのTransformerベースのモデルです。TabPFNは、多くの小規模なデータセットにおいて、木ベースのモデルよりもうまく動作することが示されています。現在、1000行未満、100特徴、10クラス以下の小規模データセットでの分類で動作しています。
```

## ARIMA

- 時系列解析に出てくるARIMAモデルとSARIMAモデルを徹底解説
  - https://bigdata-tools.com/arima-sarima-model/