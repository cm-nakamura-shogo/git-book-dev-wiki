# Azure OpenAI Service

## 参考

### [2023-06-20 Azure OpenAI Service “on your data” でChatGPTに自社データを組み込む – CloudNative Inc. BLOGs](https://blog.cloudnative.co.jp/17535/)

- GUI上での簡単な操作で自社データをChatGPTに組み込むことができるように
- 精度を高めるには、データセットの整備、Fine-tuningやPrompt engineeringをキッチリ実施していく必要
- Blob Storageに規定類を格納しておき、質問をするとChatGPTで格納した規定類の中から関連する項目をAzure Cognitive Searchを使って検索し、検索結果を踏まえてユーザーに回答するという構成

### [2023-06-20 独自ナレッジをノーコードでChatGPTに連携！Azure Open AI「Add your data」](https://zenn.dev/microsoft/articles/azure-openai-add-your-data)

- 実際にWebアプリとして公開することも試しており、Flaskでデプロイされているなどの情報あり
- アプリの中にデータソースやプロンプトはなく隠蔽されていそうとのこと
- プロンプトはアプリの環境変数で変更できるらしい

### [2023-06-20 Azure OpenAIで独自データ追加機能(Add your data)を試してみた - Qiita](https://qiita.com/tmiyata25/items/75a370154c28ee6c6983)

- 一番画像的にはわかりやすいかも
- チャンク分割された様子も伺える

### [2023-06-22 生成AI用Cognitive Searchの言語アナライザーを日本語にしたい - Qiita](https://qiita.com/tmiyata25/items/e8866dfed6dd4b9a02ad)

- Cognitive Searchを自分で構築すれば色々解決するらしいが、そこまでしなくて対処するワークアラウンドが記載されている
