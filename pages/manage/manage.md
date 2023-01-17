# manage

## GitLabでの働き方

- https://learn.gitlab.com/c/gitlab-presentation-developers-summit?x=JBqxmQ
  - カメラはデフォルトオン
  - 1on1は1week / 25分推奨
  - 1on1 ≠ coffee chat
  - coffee chat以外は、アジェンダを準備する
  - 事前にアジェンダを教えた上で、同期参加の決定権は参加者にあり。
  - 同期ミーティングの前に、３回以上非同期を試みる（アジェンダのイメージがわく）
  - JDは、あるべき姿や責任が定義される
  - #thanksチャンネルがある

## 新人教育マニュアル

- https://discord.com/channels/906524238914138172/931386975565541396/937487648493273118


## スタンドアップミーティングのやり方

- スタンダップミーティングは役に立たない」
  - https://qiita.com/e99h2121/items/49742e20983c9ec971d4

## コーチング

- 問題を外から観察する人は、解決策にたどり着けない コーチングの第一人者が語る、ソリューションを作れる人の条件
  - https://logmi.jp/business/articles/325642

## 変更管理

- FRONTEO時代にまとめた変更管理メモ
  - 受け入れる体制があると思えなかったので、そっとお蔵入り。

```
・変更管理のキモ
　・トレーサビリティがあるか？

・トレーサビリティを担保するためにやるべきことを考える
　・今のあなたの作業は、担保されているかを常に意識

・開発側
　・ソースコード　（変更履歴をたどる）
　・設計書　（キモとなる部分、ソースコードで理解が困難な部分を補完）
　・インフラ
　　・製品としてのインフラはdockerでほぼ管理できる。
　　・加えて個別の手順書が必要な部分は作成が必要
　　　・クラウドとか、メール連携とか。
　　　・クラウドは、terraformとかいうツールもあるけど、使ったことはない。
　・保守管理
　　・何をいつアップデートする予定？した？
　・問題管理
　　・どういう問題が発生した？
　　・どういう対応をした？
　　・決してメンバーを攻めてはいけない

・研究側
　・解析サーバー
　　・同じくインフラ管理
　　・製品インフラよりは更新が頻繁かも。
　・ソースコード
　　・ある程度やるべき
　・設計書
　　・研究の場合はむしろここが大事
　　・アルゴリズムの設計は思想そのものなので、ソースコードで全て表現は困難
　　・設計仕様をノートブックに書くのはありかも
　　・そのノートブックは構成管理が必要か
```

## ワーキングアグリーメント

- https://twitter.com/kajinari/status/1281528662404161536?s=20&t=NSf2PXr0B3lpTw_MqxA1cg

## 会議の方法

- [1つでも該当すると、「会議の成功率」は5分の1以下　AIが導き出した、会議の成功を阻む5要素とは - ログミーBiz](https://logmi.jp/business/articles/327251)

## リモートワークや1on1について

- [「toCとtoBの垣根は時間をかけて解消」「評価に“個人への期待”を入れてバランスをとる」　Retty×キャディが語る、事業・エンジニア組織拡大で起きた課題とその向き合い方 - ログミーTech](https://logmi.jp/tech/articles/327987)

## 組織に変化を起こす方法

- [なぜ変化を起こすのが難しいのか？ - 数年以上にわたって難しさに向き合い・考え取り組んできたこと / The reason why changing organization is so hard - What I thought and faced for more than several years - Speaker Deck](https://speakerdeck.com/iwashi86/the-reason-why-changing-organization-is-so-hard-what-i-thought-and-faced-for-more-than-several-years)
  - ちょっとした「うっ」は成長のチャンス
  - 迷ったらつらい方を選ぶ
  - 信頼貯金
  - 発信を続けることにより、いつのまにか片方向の知人が増える
  - エレベーターピッチならぬ懇親会ピッチ
  - 辞める気になって会社に働きかけてみましょう（本当にやれることを全部やっているか？）
  - 社内のすごい人をランチに誘う


## 合意形成

- [「笑顔の合意」のテクニック - 噛み合わない会話と対立を克服するための、エモさを排した実践的なスキルと技法 - - Speaker Deck](https://speakerdeck.com/hageyahhoo/xiao-yan-nohe-yi-notekunituku-nie-mihe-wanaihui-hua-todui-li-woke-fu-surutameno-emosawopai-sitashi-jian-de-nasukirutoji-fa)
  - 怒りの他人事化は面白かった。
