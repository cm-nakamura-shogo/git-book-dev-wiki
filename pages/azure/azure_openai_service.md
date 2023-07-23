# Azure OpenAI Service

## Contents

- [Azure-Samples/jp-azureopenai-samples](https://github.com/Azure-Samples/jp-azureopenai-samples)

## Articles

- [2023-06-20 Azure OpenAI Service “on your data” でChatGPTに自社データを組み込む – CloudNative Inc. BLOGs](https://blog.cloudnative.co.jp/17535/)
  - GUI上での簡単な操作で自社データをChatGPTに組み込むことができるように
  - 精度を高めるには、データセットの整備、Fine-tuningやPrompt engineeringをキッチリ実施していく必要
  - Blob Storageに規定類を格納しておき、質問をするとChatGPTで格納した規定類の中から関連する項目をAzure Cognitive Searchを使って検索し、検索結果を踏まえてユーザーに回答するという構成
- [2023-06-20 独自ナレッジをノーコードでChatGPTに連携！Azure Open AI「Add your data」](https://zenn.dev/microsoft/articles/azure-openai-add-your-data)
  - 実際にWebアプリとして公開することも試しており、Flaskでデプロイされているなどの情報あり
  - アプリの中にデータソースやプロンプトはなく隠蔽されていそうとのこと
  - プロンプトはアプリの環境変数で変更できるらしい
- [2023-06-20 Azure OpenAIで独自データ追加機能(Add your data)を試してみた - Qiita](https://qiita.com/tmiyata25/items/75a370154c28ee6c6983)
  - 一番画像的にはわかりやすいかも
  - チャンク分割された様子も伺える
- [2023-06-22 生成AI用Cognitive Searchの言語アナライザーを日本語にしたい - Qiita](https://qiita.com/tmiyata25/items/e8866dfed6dd4b9a02ad)
  - Cognitive Searchを自分で構築すれば色々解決するらしいが、そこまでしなくて対処するワークアラウンドが記載されている
- [2023-06-27 GPTシステム開発を加速するAzureサービスの活用 - Speaker Deck](https://speakerdeck.com/hirosatogamo/20230627-gptsisutemukai-fa-wojia-su-suruazuresabisunohuo-yong)
  - 以下の内容について言及
    - Plugin
    - Prompt Enginnering
    - LLMOps（運用面）
  - 個人的には以下の内容が印象的でした。
    - p.32 Prompt テクニック
    - p.35~ 近日公開予定の Azure Machine Learning - Prompt flow（様々な言語モデルとデータソースを使用するAIワークフロー作成機能）の紹介
    - p.40,41,44 各用途で使うAzureサービスの図
  - MSのBuild に参加していて、MSの方に教えてもらった内容共有です。
    - Azureのadd your dataの機能って、WebにはDeployできるけどエンドポイント提供する予定はある？
      - 製品のロードマップには入っているため将来的には実施予定。ただ、先になりそう。
    - Fine-tuningのつかいどころは？
      - 簡単なタスクを安く実施したいというビジネスニーズへの対応が使い方
      - 精度向上を行いたい場合は、追加情報の付与→Embeddingが今のところは一番いい
    - ベクトル化した情報を検索する場合の最適な検索方法やデータの事前準備ってなにかある？
      - ベクトル検索だけではなくて、Cognitive Searchはキーワード検索と組み合わせていてオススメなので、試してみてね
- [2023-06-28 Azure OpenAIで自社データを取り込んだChatbotを実現する。 | DevelopersIO](https://dev.classmethod.jp/articles/azure-openai-add-your-data/)
  - 特に既出の情報
- [2023-07-04 Azure Open AIの「Add your data」で出来ること出来ないこと](https://zenn.dev/microsoft/articles/azure-openai-add-your-data-procon)
- [2023-07-05 Azure OpenAIを使ったチャットボットWebアプリをAzure App Serviceでホストしてみた | DevelopersIO](https://dev.classmethod.jp/articles/azure-openai-chatbot/)
  - 構築時の参考に
- [2023-07-05 Azure OpenAIを使ったチャットボットWebアプリをAzureに閉じたネットワーク環境に構築する方法 | DevelopersIO](https://dev.classmethod.jp/articles/azure-openai-chatbot-in-closed-network/)
  - 構築時の参考に
- [2023-07-07 Prompt Flowが使えるようになったから、もうLangChainとか自分でホストしなくていい世界になったのかもしれない。 | DevelopersIO](https://dev.classmethod.jp/articles/azureml-prompt-flow-ktkr/)
  - Azure使いならまあありなのかも
  - GUIなのでLangChainなどより更にカスタマイズがむずいのでマネージド寄り。
- [2023-07-07 Azure Machine LearningでModel Catalogが使えるようになりました。 | DevelopersIO](https://dev.classmethod.jp/articles/azureml-model-catalog-ktkr/)
- [2023-07-18 Azure Cognitive SearchとCognitive Servicesの深堀り：実践的に画像タグ付けと説明文の生成を試してみた | DevelopersIO](https://dev.classmethod.jp/articles/azure-cognitive-serch-cognitive-services-image-tagging)
  - Cognitive Servicesてのがあるのか
- [2023-07-21 Azure OpenAI にもFunction Callingの機能がきたんですって！](https://dev.classmethod.jp/articles/azure-openai-function-calling-ktkr/)
  - まあそりゃそうよなという記事
  - 公式
    - [Function calling is now available in Azure OpenAI Service - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/function-calling-is-now-available-in-azure-openai-service/ba-p/3879241)