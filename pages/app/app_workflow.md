# Digdag

* [公式](https://github.com/treasure-data/digdag#develop-digdag-ui)
* [GUIから理解するDigdagチュートリアル | DevelopersIO](https://dev.classmethod.jp/articles/digdag-tutorial-gui/)
* [Digdag 入門 | GMOインターネットグループ研究開発本部（次世代システム研究室）](https://recruit.gmo.jp/engineer/jisedai/blog/introduction-to-digdag/)


## requireオペレータ

requireオペレータは、別のワークフローの完了を要求している。

その際、ポーリングしてリトライをしているため、リトライのカウントが増えている。

ポーリング感覚は、最初はExponential Backoffとなっており、10秒以降は10秒固定となっている。

- 参考記事
  - [Digdagにおけるrequireオペレータ使用時のretry挙動を理解する | DevelopersIO](https://dev.classmethod.jp/articles/digdag-require-retry-count/)
