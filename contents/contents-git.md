# contents-git

## はじめに

Gitはコード等のバージョン管理のデファクトとなっていますので基本の使い方を抑えましょう。

## セットアップ

Windowsの場合は、Git for Windowsをインストールしてください。

（ついでにGit for Bachも入るので便利です）

- https://gitforwindows.org/

Macユーザはbrewとか使ってインストールすればいいようです。

- https://qiita.com/suke_masa/items/4bed855628f7414293f8

## コンテンツ

- MIXIさんの動画とスライド
    - [Git研修【MIXI 23新卒技術研修】 - YouTube](https://www.youtube.com/watch?v=lWkO8bQ9pSo)
    - [Git研修【MIXI 23新卒技術研修】 - Speaker Deck](https://speakerdeck.com/mixi_engineers/2023-git-training)
- その他
    - [VScodeだけでGit操作を完結させるのだ～～ッ!!](https://zenn.dev/praha/articles/db1c4bcc4ef48c)

## 進め方

MIXIさんの動画は結構よいです。基本は1h10minまで見ればOKです。

以下のポイントについて言及されててとても良いです。

- fast foward mergeとは
- mergeとrebaseのメリット・デメリット、それぞれの用途
    - merge
        - 👍push済みのコミットログを強制的に書き換える必要が無い
        - 😔不要なコミットがPRに表示される
    - rebase
        - 😔ブランチがpush済みの場合コミットログの強制書き換えが必要
            - ブランチに共同作業者がいる場合は危険（変更が消える）
            - 安全のために--force-with-leaseや--force-if-includesなどが追加されてきた経緯
        - 👍PRで見るコミット履歴がキレイになる
- branch運用の解説
    - Git Flowなど
- Gitの仕組みがもっと知りたい方は1h10min以降も見てみてください。
    - Whyはあまりないので結構厳しいかも

その後、VSCode + Git操作を抑えておきましょう。

MIXIさんのコンテンツではコマンド操作が重きを置かれていましたが、日常的にはGUIで操作するのも便利です。

以下にVSCodeを使ってGUIでGit操作する例が記載されているので参考にされてください。

- [VScodeだけでGit操作を完結させるのだ～～ッ!!](https://zenn.dev/praha/articles/db1c4bcc4ef48c)
