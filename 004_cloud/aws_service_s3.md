# Amazon S3

## 手動操作した場合のライフサイクルポリシー

例えば下記のようなライフサイクル設定をしているとして、

- 60 days Standard -> Standard-IA
- 120 days Standard-IA -> Glacier (FR)

そしてcat.jpgをアップロードし、10日後に手動でStandard-IAに移行した場合、10+120日後にGlacierに移動される。
最終更新日のみが使用されるため。