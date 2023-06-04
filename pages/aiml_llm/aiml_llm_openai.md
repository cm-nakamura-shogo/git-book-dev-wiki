# LLM : OpenAI

### [2023-03-09 OpenAI 言語モデルごとのエンコーディング一覧](https://zenn.dev/microsoft/articles/3438cf410cc0b5)

- エンコーディングというかトークナイザの話といった方が誤解が無さそう。
- とりあえずほとんどの最新のやつはcl100k_baseを使っている。

### [2023-04-16 npakaさん : OpenAI APIのファインチューニングの学習データのガイドライン](https://note.com/npaka/n/n021a59452dc8)

- いずれ必要になるかもしれないファインチューニングの知識

### [2023-04-23 tiktokenでトークンについて掘り下げた記事](https://nikkie-ftnext.hatenablog.com/entry/how-chatgpt-tokenize-japanese-text-tackling-with-tiktoken)

- 1漢字（ユニコード）が２つのトークンに分割されているのは知らなかった
- 使われ方が似ている文字が近くの文字コードに来ているとは限らないから、これは少し斬新だなという感想

### [2023-04-25 ChatGPTのWeb版がオプトアウトをより簡易に提供](https://openai.com/blog/new-ways-to-manage-your-data-in-chatgpt)

- 30日保存はAPIと同様なので注意。
- 不正使用を監視するために必要な場合に使われるとのこと。
- また、ChatGPT Businessもアナウンスされているが、単純にデフォルトでオプトアウトという形らしい。
- 弊社ブログ
  - [https://dev.classmethod.jp/articles/chatgpt-web-chat-history-off/](https://dev.classmethod.jp/articles/chatgpt-web-chat-history-off/)

### [2023-04-26 OpenAI の Embeddings API はイケてるのか、定量的に調べてみる - Qiita](https://qiita.com/akeyhero/items/ce371bfed64399027c23)

- ２つの類似度計算では教師有モデルのBERTやLUKEの方が良いらしいが、これらは全てのペアに対して都度計算が必要なのでEmbeddingsにもメリットがある
- 他のEmbeddingsと比較するという点では、PKSHAの SimCSEがより良い結果らしい。これは参考になる。

### [2023-04-26 OpenAIのブランドガイドラインが公開された](https://dev.classmethod.jp/articles/about-openai-brand-guidelines/)

- 明記する必要のあることがいくつかありそう
- マークについても言及がある

### [2023-05-12 OpenAIがWeb browsingとPluginsのbeta版をもうすぐロールアウト](https://help.openai.com/en/articles/6825453-chatgpt-release-notes)

- 来週中にすべてのPlusユーザーに展開される予定

### [2023-05-18 OpenAIのOrganization機能の利用方法をまとめ](https://dev.classmethod.jp/articles/openai-organization-how-to/)

- 端的に言うと、APIの利用料をまとめて請求できるようになる機能
- WebのUIから利用するChatGPTのPlusアカウントの請求をまとめて行うことは現状できない
