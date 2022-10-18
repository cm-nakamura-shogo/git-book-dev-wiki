# sklearn

## pipeline

- sklearnのpipelineに自分で定義した関数を流し込む - Qiita
  - https://qiita.com/kazetof/items/fcfabfc3d737a8ff8668

## data

- train_test_splitのindex番号を記憶する方法
  - 引数`indices`にindex番号を指定すればOK

```python
X_train, X_test, Y_train, Y_test, indices_train, indices_test = train_test_split(X, Y, indices, test_size=0.33)
```

- 参考
  - https://qiita.com/haru1977/items/7aaf1eaeb0747fe613be

## マルチラベルをバイナリエンコード

category encodersで対応できないので、scikit-learniでやる必要がある。

一つのセルに対して複数データがセットある状態が入力。

```python
import pandas as pd
df = pd.DataFrame(
    {"col1": [["aaa","bbb","ccc"], ["aaa"],["ccc","ddd"]]}
)
df
```
![](./img/scikitlearn_2022-10-18-22-44-17.png)

これを以下のコードでバイナリエンコード可能

```python
from sklearn.preprocessing import MultiLabelBinarizer
mlb = MultiLabelBinarizer()
df = pd.DataFrame(mlb.fit_transform(df['col1']), columns=mlb.classes_)
df
```
![](./img/scikitlearn_2022-10-18-22-46-18.png)

- 参考記事
  - [Types of Encoder - Michael Fuchs Python](https://michael-fuchs-python.netlify.app/2019/06/16/types-of-encoder/#multilabelbinarizer)
  - [pandas.DataFrameのマルチラベルを簡単にバイナライズする方法 - Qiita](https://qiita.com/maechanneler/items/b6a06a9e296f02af0801)