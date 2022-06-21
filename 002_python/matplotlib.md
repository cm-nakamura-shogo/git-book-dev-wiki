# matplotlib

## font設定

- 一覧取得

```python
fonts = set([f.name for f in matplotlib.font_manager.fontManager.ttflist])
print(sorted(fonts))
```

- ノートブック内などで都度設定する方法

```python
plt.rcParams['font.family'] = 'HackGen'
```