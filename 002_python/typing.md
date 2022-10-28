# typing

型ヒントを記述するためのモジュール。標準機能だがPython 3.5以降で有効。

## Literal

Python 3.8以降で導入された、特定の複数の文字列のみを許容する型。

```python
import typing as T.

status: T.Literal["enabled", "disabled"] = "enabled"
```

参考記事
- [[小ネタ] Pythonの型ヒントで特定の文字列のみ受け入れる型を定義する | DevelopersIO](https://dev.classmethod.jp/articles/python-typing-literal/)