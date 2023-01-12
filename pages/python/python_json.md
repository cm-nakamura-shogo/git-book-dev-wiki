# json

jsonをパースしたりする標準ライブラリ

## ensure_ascii=False

JSONは仕様的には日本語はエンコードされるべきであるが、編集として日本語を使用したいケースがある。

その場合は、ensure_ascii=Falseとしてdumpsする必要がある。

```python
json.dumps(hogehoge_dict, ensure_ascii=False)
```