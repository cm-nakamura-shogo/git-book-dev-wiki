# Pandas

## 列を並び変える。

- 並び変えたカラムを[]に入れるだけで良い。

```python
columns = df.columns.tolist()
columns = columns[-1:] + columns[:-1] # reorder example
df = df[columns] # do reorder!!
```

## group集計して統計量を計算する。

- 既に準備されている統計計算をする場合

```python
# user_idで集計して、年齢の統計量を計算する例
age_stats_df = rowdata_df.groupby("user_id")["age"].agg(["mean"])

# 上記では、goupbyしたカラムがindexになってしまうので、嫌な場合はreset_index()する。
age_stats_df = rowdata_df.groupby("user_id")["age"].agg(["mean"]).reset_index()
```

- 自作でpersentileなどを計算したい場合

```python
# 自作関数を作る
def percentile(n):
    def percentile_(x):
        return np.percentile(x, n)
    percentile_.__name__ = 'percentile_%s' % n
    return percentile_

age_stats_df = rowdata_df.groupby("user_id")["age"].agg([percentile(80)]).reset_index()
```

- 時系列データを集計する場合
  - 時刻情報がある場合、その列をindexにすることで、resampleが使えて集計できる。
  - 購入量の時系列データのイメージで以下は'M'で月ごとの結果を集計する例。
```python
timedomain_df.set_index("recorded_at", drop=True).sort_index().loc[:,["purchase_count"]].resample('M').agg(['sum', 'mean', "max"])
```

## 行を挿入する。

- seriesをappendする。

```python
import pandas as pd

df = pd.DataFrame([], columns=['A', 'B', 'C'])
row_data = pd.Series(['0', '1', '2'], index=df.columns)

df = df.append(row_data, ignore_index=True)
df = df.append(row_data, ignore_index=True)
```

- dictをappendする。
```python
df = df.append({'A': 0, 'B': 1, 'C': 2}, ignore_index=True))
df = df.append({'A': 0, 'B': 1, 'C': 2}, ignore_index=True))
```

## 列毎の欠損数を求める。

```py
df.isnull().sum()
```

## applyの使用法まとめ

- 以下ノートブック参照
  - [pandas_apply_examples.ipynb](./notebooks/pandas_apply_examples.ipynb)


## query記法を使った条件抽出

- カラム名に空白のある場合はバッククォートを使う。

```python
df_receipt.query('`sales ymd` == 20181103')
```

- placeholderは、f-stringでもかけるが、@の方が汎用性が高い。

```python
user_id = "1000"
df.query('user_id == @user_id')
```

## 時刻系のデータをquery記法で処理

```python
timedelta_val = timedelta(days=1)
df.query('yyyymmdd_diff > @timedelta_val')

date_val = datetime(2022,6,15)
df.query('yyyymmdd > @date_val')
```

たとえばtimedeltaを数値として扱いたい場合などは、`datetime.timedelta`と併せて使う。

```python
from datetime import timedelta
df['yyyymmdd_diff'] / timedelta(days=1)
```

## read_csvで型指定

- dictで各列の型を指定できる。

```python
read_dtype = {
  'yyyymmdd': 'str'
  , 'column1': 'int'
  , 'column2': 'float'
}
df = pd.read_csv("sample.csv", dtype=read_dtype)
```

- 日付等は以下のように後変換する。

```python
df['yyyymmdd'] = pd.to_datetime(df['yyyymmdd'])
```

## 抽出して新しい列を作る

```python
df = pd.DataFrame([
    ['aaa','aaa.pptx'],
    ['bbb','bbb.pptx'],
    ['ccc','ccc.pptx'],
], columns=['name', 'file'])

df['file'].str.extract("(.*)\.pptx")
```

## rank: 順位を付ける

```python
# 値が高い順(降順)、同値は小さい順位(上位)に合わせる
df['column_name'].rank(ascending=False, method='min')
```
## unique: 出現する種類を把握する

```python
df['column_name'].unique()
```

## value_counts: 内訳を知る

```python
df.value_counts('column_name')
```

その他のオプション
- `normalize=True`で比率を計算できる。
- `bins=30`で連続値も集計できる。
- `dropna=True`でNaNを無視できる。

## sort_values: 並べ替え

```python
# 値が高い順(降順)
df.sort_values('column_name', ascending=False)
```

## isnull(): 欠損値かどうかを調べる

```python
df.isnull()
df['column_name'].isnull()
```

## dropna(): 欠損値を削除する

- 通常は一つでも欠損がある場合は削除される。

```python
df.dropna()
```

- どこかの列に基づきたい場合は、subsetで指定する。

```python
df.dropna(subset=['column1'])
```

## locとilocの違い

- locはindex(いわゆるDataFrameのIndex), column名でアクセスする。
- ilocは本当のindex番号で縦横ともにアクセスする。
  - なのでilocを使えば、reset_index(drop=True)しなくてもアクセスしたいものにアクセスできるかもしれない

## merge: joinしたいとき

- だいたいこんな感じの書き方におさまる。

```python
df\
  .merge(df2[['column1', 'column2']], how='inner', on='column1')\
  .merge(df3[['column1', 'column3']], how='left', on='column1')\
```

- 複数をキーにjoinしたい場合は、`on=['column1', 'column2']`とすればOK。

- join後に重複するカラム名は、`suffixes=['_left', '_right']`と指定すれば末尾に目印をつけられる。

## groupby + agg: 集約したいとき

- だいたいこんな感じの書き方におさまる。

```python
def my_func(x):
    return np.std(x)

stats_df = df.groupby('column1').agg(
    new_column1 = ('org_column2', 'mean'),
    new_column2 = ('org_column2', 'std'),
    new_column3 = ('org_column3', my_func),
).reset_index()
```

## grouby + transform: 集約したものを各行に割り当てる

- 集約となるmeanやsumは、transformにより行を元のDFに拡張することができる。

```python
df['column2_mean'] = df.groupby(['column1'])['column2'].transform("mean")
```

## groupby + shift, rank: 集約でない場合のgroupby + 各行割り当て

- transformとかも選択肢にでてくるけど、使わなくても行ける。
- 集約ではなく、shiftやrankなどの場合はこの方法が使える。

```python
df.groupby('column1')['column2'].shift(-1)
```

## idxmin: 最小値の時のPandas Indexを得る

```python
df['column1'].idxmin()
```

## drop_duplicates: 重複を削除する

- 残すものをコントロールするためには、事前にsort_valuesしておく感じの使い方となる。

```python
df.drop_duplicates(subset=['column1', 'column2'], keep='first') # 最初を残す
df.drop_duplicates(subset=['column1', 'column2'], keep='last') # 最後を残す
df.drop_duplicates(subset=['column1', 'column2'], keep=False) # 残さない
```

## duplicated: 重複の判定

- ほぼdrop_duplicatedと同じ。

```python
df.duplicated(['column1','column2'], keep='last')
```

- 抽出の場合はこうする

```python
df[df.duplicated(['column1','column2'], keep='last')]
```
