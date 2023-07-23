# LLM : サービス

おもにSaaSっぽい活用サービスをまとめている

## Articles

- [2023-03-14 DocsBot AI を使ってみた](https://zenn.dev/howdy39/articles/a4a6f07a95a023)
  - 任意のドキュメントを食わせて検索可能なSaaS
  - 社内的にやりたいことと、似ている例
- [2023-03-30 Evolving Zoom IQ, our AI smart companion, with new features and a collaboration with OpenAI](https://blog.zoom.us/zoom-iq-smart-companion/)
  - zoomがリアルタイムでミーティング内容をまとめて、遅れてきた人にサマリー表示して、質問にも答えてくれるらしい。
- [2023-04-10 GPT関連の参考になるアプリケーション](https://qiita.com/sonesuke/items/03c979177adccb7758f2)
  - アーキテクチャが整理されててよい。
  - ライブラリの活用方法で悩んだら見ると良いかも。
- [2023-04-13 LLMを高速に学習できるDeepSpeed-ChatをMicrosoftが公開](https://zenn.dev/howdy39/articles/a4a6f07a95a023)
  - OPT-13Bが7.5時間で$1,920（約25万円）単位とのこと
- [2023-04-13 YeagerAI: Langchain Agentクリエイター](https://twitter.com/yeagerai/status/1646194523242995713)
  - プロンプトでAgentを作ってしまうということ？
- [2023-04-13 LangChainをGUIで扱えるFlowiseAIがリリース](https://twitter.com/FlowiseAI/status/1646176565691023360)
  - LangFlowより高機能なのかな？
- [2023-04-14 Google Colab で BabyAGI を試す](https://note.com/npaka/n/n97152182c98a)
  - タスク駆動型自律エージェントのフレームワークです。ゴールに基づいてタスクの作成、優先順位付け、および実行を行う。
  - 無限ループで自動でトークンを消費するのでそこは注意。
  - GPT-4がやっぱ強い。
- [2023-04-14 AutoGPTやAgentGPTやら自律的にタスクを解く](https://twitter.com/jerryjliu0/status/1646172524173209600?s=12&t=0nszgXsDXAd-L4WiCutIWg)
  - AutoGPTは環境構築が必要だが、AgentGPTというWebサービス版がある。
- [2023-04-15 Streamlitで実装されたQAチェーンを評価するauto-evaluatorの紹介](https://blog.langchain.dev/auto-eval-of-question-answering-tasks/)
  - OpenAIモデルだけでなく、RetrieverやEmbeddingに使うモデルも変更しながら評価が可能なツールとなっている
- [2023-04-24 GPT4Toolsの公開](https://gpt4tools.github.io/)
  - Toolsに画像処理をいくつかいれてあり、それをユーザのクエリから選ぶ感じで対話的に画像処理をするツール
  - 前の出力を次の入力とすることができるので、編集を対話的に実施できる感じみたい
- [2023-05-04 StarCoder: コード生成用の最先端のLLM (Hugging Face)](https://huggingface.co/blog/starcoder)
  - ベンチマークでは、OpenAIのcode-cushman-001 (12B)モデルも凌駕している
  - VSCodeの拡張機能「HF Code Autocomplete」として使える（APIキーとかは必要そう）
    - [HF Code Autocomplete - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=HuggingFace.huggingface-vscode)
  - npakaさん
    - [StarCoder - コードのためのLLM｜npaka｜note](https://note.com/npaka/n/n242eadbf2cd2)
- [2023-05-07 NVIDIA製OSSのLLMにガードレールを設定するNeMo Guardrails (DevIO)](https://dev.classmethod.jp/articles/nemo-guardrails-overview/)
  - 裏側はLangChainってのがLangChainの先行具合を語っているな
- [2023-05-07 SalesforceがSlackGPTをローンチ](https://thebridge.jp/2023/05/salesforce-launches-slackgpt-embracing-generative-ai-for-enterprise-workflows)
  - AI 機能はまだ新しい Slack プラットフォームの一部として開発・テストされている
  - 未読のメッセージが多数ある場合、ユーザはクリックするだけで議論された内容の要約を得ることができ、要約とアクションアイテムを求めることで、逃した打ち合わせに追いつくことができる
  - Claudeという見慣れないLLMの姿も
- [2023-05-08 食べログがChatGPTプラグインを提供開始](https://prtimes.jp/main/html/rd/p/000000903.000001455.html)
- [2023-05-10 ZendeskがOpenAIと提携しZendesk AIを発表](https://www.zendesk.co.jp/newsroom/press-releases/zendesk-ai/)
  - devio
    - [[速報] #Zendesk が #OpenAI と提携しAI関連の新サービス Zendesk AIを発表しました | DevelopersIO](https://dev.classmethod.jp/articles/zendesk-ai-announces/)
- [2023-05-10 GitLabとGoogle CloudはAI分野での提携を発表](https://www.publickey1.jp/blog/23/gitlabgoogle_cloudaiai.html)
  - GitHub Copilot Xの後追い
- [2023-05-11 ChatGPT Code Interpreterのデモ動画](https://twitter.com/yutatatatata/status/1656460958309707776)
  - すごいし個人的には便利だと思う
  - 動画をみてると分析観点のフィードバックを指示であたえるには、結局専門知識いるので、誰でもできるようになるわけではなさそう。
  - 自分でやったことある人しか使いこなせないやーつな気もする
- [2023-05-13 AnnotationGPTは凄そう (piqcyさん)](https://twitter.com/icoxfog417/status/1657282631804014595)
- [2023-05-25 Voyager: An Open-Ended Embodied Agent with Large Language Models](https://voyager.minedojo.org/)
  - LLMを使ったゲームエージェントのようだ。それをVoyagerと呼んでいる
- [2023-06-15 WizardCoder-15B](https://twitter.com/hardmaru/status/1669898590435835906)
  - StarCoderなど既存のコード補完より良いと主張している
  - [米Microsoftら、“コーディング専用”大規模言語モデル「WizardCoder」開発　文章から高品質なコード出力：Innovative Tech - ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2307/21/news066.html)
