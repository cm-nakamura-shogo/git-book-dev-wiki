# 数学について

## 【ベイズ統計その①】条件付き確率と Bayes の定理【時間の流れを意識せよ！】

- 参考
  - [https://www.youtube.com/watch?v=mX_NpDD7wwg](https://www.youtube.com/watch?v=mX_NpDD7wwg)

### 確率とは

- 部分 / 全体。
- Uを全体、Aを事象とすると以下。

$$ P(A) = \frac{A}{U} $$

- 例としては、サイコロで、事象Aを偶数がでるとすると
 
$$ U = \{1,2,3,4,5,6\} $$

$$ A = \{2,4,6\} $$

### 条件付き確率

- 条件付き確率。たとえば、Aが起こる場合にBが起こる確率。

$$ P(B|A) = \frac{A \land B}{A} $$

- 右辺の分子分母を全体 $$ U $$で割ると

$$ P(B|A) = \frac{\frac{A \land B}{U}}{\frac{A}{U}} $$

- つまり以下。

$$ P(B|A) = \frac{P(A \land B)}{P(A)} $$

- ここから以下も正しい。

$$ P(A \land B) = P(B|A)P(A)$$

- AとBを逆にしてももちろん成立する。

$$ P(A|B) = \frac{P(A \land B)}{P(B)} $$

### ベイズの定理

$$ P(A|B)=\frac{P(B|A)P(A)}{P(B)}$$

- 証明は簡単で、反転させた式で$$ P(A \land B) $$を消せば成り立つ。

### 順行と逆行

- 問題
  - 袋Xに赤３、白５
  - 袋Yに赤１、白３
  - 確率1/2でX,Yを選んで袋を選び、玉を取り出す。
  - 袋Xをえらぶ事象をA、赤玉を引く事象をBとする。
- この時の$$ P(A),P(B),P(A|B),P(B|A),P(A \land B) $$を求めることを考える。
- このとき以下は問題より直接求まる。

$$ P(A) = 1/2 $$

$$ P(B|A) = 3/8 $$

- 計算により以下も求まる。

$$ P(B) = 1/2 \times 3/8 + 1/2 \times 1/4 = 5/16 $$

$$ P(A \land B) = 1/2 \times 1/8 = 3/16 $$

- 以下は条件付き確率の式から求まる。

$$ P(A∣B) = \frac{P(A \land B)}{P(A)} = 3/5 $$

- 最後の$$ P(A|B) $$のみ、「赤玉を引いたとしたときに、袋がXだった確率」の逆行となっている。

### ベイズの定理の意味

- 以下のベイズの式は、左辺が逆行、右辺が順行となっている点がポイント。

$$ P(A|B)=\frac{P(B|A)P(A)}{P(B)}$$

- 統計的推論では、結果から状態などを推測するため、逆行する。
- これを順行から求められるのが大事なポイントであり、ベイズの定理の有用さ。
- もっというと、順行・逆行は因果関係という話（時間とは限らない）。

## 【ベイズ統計その②】この推定、もっとももっともらしいってよ…！【最尤推定のお話だよ！】

- 参考
  - [https://www.youtube.com/watch?v=5iSZqYh9wOs](https://www.youtube.com/watch?v=5iSZqYh9wOs)

### 推定とは

- 現象から支配パラメータを予想する。
  - 現象: 100回コインを投げて、30回表となった
  - 推測: 3/10が表の出る確率と予想
  - この3/10が支配パラメータの推測結果

### 最尤推定

- 表が出るという確率をp(支配パラメータ)とする。
- n回投げてk回表が出た。(現象)
- この現象の確率は以下で表すことができる。

$$ {}_n \mathrm{C}_k p^{k} (1-p)^{n-k} $$

- しかしこの視点は、神の視点である。
- 庶民の視点は現象が先。
  - n回投げてk回表が出た。(現象)
  - 表が出る真の確率を$$ p_o$$ (支配パラメータ)としてこれを求める方法を考える。
  - もしこの確率がpである場合、現象は$$ {}_n \mathrm{C}_k p^{k} (1-p)^{n-k} $$というで発生する。
  - この$$ {}_n \mathrm{C}_k p^{k} (1-p)^{n-k} $$を尤度(likekihood)という。
  - 尤度を$$ L(p) $$とする。

- 最尤推定とは
  - 尤度$$ L(p) $$が最大になるpを$$ \hat{p} $$とすると、$$ \hat{p} $$が$$ p_o$$ とする推定法のこと
- 式で表すと以下

$$ \hat{p} = \argmax{L(p)} $$

### 最尤推定の例１：コイン

- サイコロの場合
- 尤度は以下。

$$ L(p) = {}_n \mathrm{C}_k p^{k} (1-p)^{n-k} $$

- 対数をとっても最大値は変わらないので、対数を取る。

$$ \log{L(p)} = l(p) = k\log{p} + (n-k)\log{(1-p)} + \mathrm{const.} $$

- なお、$$ {}_n \mathrm{C}_k $$は適当な定数のため、そのように置いた。
- この式を微分する。

$$ l^{'}(p) = \frac{k}{p} + \frac{n-k}{1-p}$$

- この式が0のとき、極値を持つ。

$$ \frac{k}{p} - \frac{n-k}{1-p} =0 \Leftrightarrow p = \frac{k}{n} $$

- (この証明は厳密ではないので注意。極値と最大値は異なるため)

### 最尤推定の例２：サイコロ

- n回のうち、各目が出る回数は$$ k_1,k_2, \cdots ,k_6 $$であった。（現象）
- このサイコロの各目が出る回数$$ p_1,p_2, \cdots ,p_6 $$を考える。
- 尤度は以下。2項定理の一般化。

$$ L(p) = \frac{n!}{k_{1}!k_{2}! \cdots k_{6}!} p_1^{k_1}p_2^{k_2} \cdots p_6^{k_6} $$

- 対数を取る。

$$ \log{L(p)} = l(p) = k_1 \log(p_1) + \cdots + k_6 \log(p_6) + \mathrm{const.} $$

- ここで、$$ p_1,p_2, \cdots ,p_6 $$の合計は1であることを使って、$$ p_6 $$を削除する。

$$ l(p) = k_1 \log(p_1) + \cdots + k_6 \log(1 - p_1 - \cdots - p_5)$$

- これを$$ p_1 $$で微分すると

$$ \frac{\partial l}{\partial p_1} = \frac{k_1}{p_1}-\frac{k_6}{p_6}$$

- その他の偏微分についても以下のように成り立つ。

$$ \frac{\partial l}{\partial p_i} = \frac{k_i}{p_i}-\frac{k_6}{p_6}$$

- 最尤推定値の場合、全ての偏微分が0であるため

$$ \frac{k_1}{\hat{p_1}} = \frac{k_2}{\hat{p_2}} = \cdots = \frac{k_6}{\hat{p_6}} $$

- これが成り立つのは以下のとき。

$$ \hat{p_i} = \frac{k_i}{n} $$

### 最尤推定の課題

- 観測したサンプルが少ない場合は信頼度が低い。
  - コインを３回なげて２回表の場合、2/3で表と言っていい？
- 逆説的にいうと、正しい値を得るためには、無限回に指向が必要。

## 【ベイズ統計その③】宇宙一わかりやすいベイズ推定【本気の解説】

- 参考
  - [https://www.youtube.com/watch?v=I3le5FVPcnw](https://www.youtube.com/watch?v=I3le5FVPcnw)

### 最尤推定の課題と対策

- 課題は支配パラメータを一様分布と仮定している。
  - 例えばコインの場合、支配パラメータ$$ p_o $$は0.5付近にある。
  - これは経験則で与えられ、事前分布と呼んだりもする。

### コインの例

- 以下はどちらが表になりやすいか？という問題
  - コインAは3回投げて2回表
  - コインBは100回投げて60回表
