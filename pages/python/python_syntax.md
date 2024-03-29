# syntax(文法)

## チートシート

- [Comprehensive Python Cheatsheet](https://github.com/gto76/python-cheatsheet)

## リスト内包表記とif

- 普通のリスト内包表記
```python
sample_list = [0,1,2,3,4,5,6]
sample_list_2 = [ i*2 for i in sample_list]
sample_list_2
# OUT: [0, 2, 4, 6, 8, 10, 12]
```

- if/elseとの組み合わせ（配列サイズ不変）
```python
sample_list = [0,1,2,3,4,5,6]
sample_list_3 = [ i*2 if i%2==1 else 0 for i in sample_list]
sample_list_3
# OUT: [0, 2, 0, 6, 0, 10, 0]
```

- 抽出
```python
sample_list = [0,1,2,3,4,5,6]
sample_list_4 = [ i*2 for i in sample_list if i%2==1]
sample_list_4
# OUT: [2, 6, 10]
```

## 再帰処理

```python
def exec_lower_recurisive(text_input, text_output_recursive=[]):
    for element in text_input:
        if isinstance(element, list):
            text_output_sub = []
            exec_lower_recurisive(element, text_output_sub)
            text_output_recursive.append(text_output_sub)
        else:
            output = element.lower()
            text_output_recursive.append(output)

text_input = ["AAA", "BBB", "CCC", ["DDD", "EEE"] ]
text_output_recursive = []
exec_lower_recurisive(text_input, text_output_recursive)

print(text_output_recursive)
# OUT: ['aaa', 'bbb', 'ccc', ['ddd', 'eee']]
```

## setの使い方

- pythonのsetの使い方
  - https://uxmilk.jp/14834

## pythonでhtmlの特殊文字をエスケープする

- https://docs.python.org/ja/3/library/html.html

## フォルダ設計

- https://rinatz.github.io/python-book/

## flagという標準モジュール

- Python標準ライブラリのFlagがシンプルで使いやすいという話
  - https://myenigma.hatenablog.com/entry/2021/11/14/195705

## pythonの静的解析

- https://data.gunosy.io/entry/linter_option_on_pyproject

## python早見帳

- https://chokkan.github.io/python/

## クラスのメソッドのアンスコ1個と2個のprefixについて

- [Pythonのアンダースコア2個で始まる名前は非公開だけでなくマングリング機構を利用してサブクラスに継承しないために使う - Qiita](https://qiita.com/shiracamus/items/5331cd89b202953403dd)
  - 基本はアンスコ1個でOK
  - 継承先のサブクラスで上書きされたくない場合は、アンスコ2個付ける。
    - これを呼び出せるのは、継承元側のみのメソッド内になるが。
  - 用途はあまり思い浮かばないので基本はアンスコ1個でOK。

## 辞書型の操作

### 特定キーの有無

```python
dict1 = {"a":1, "b":2}
if "a" in dict1:
    print("exist")
```

### マージ

dictを使う。updateでも可能だが、破壊的変更となるため要注意。

```python
dict1 = {"a":1, "b":2}
dict2 = {"c":3, "d":4}

dict3 = dict(dict1, **dict2)
```


