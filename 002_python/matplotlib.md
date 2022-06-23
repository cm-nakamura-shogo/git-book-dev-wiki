# matplotlib

## font設定

- 一覧取得

```python
from matplotlib import font_manager
fonts = set([f.name for f in font_manager.fontManager.ttflist])
print(sorted(fonts))
```

- ノートブック内などで都度設定する方法

```python
plt.rcParams['font.family'] = 'HackGen'
```