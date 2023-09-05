# Amazon Lex

## Articles

- [2023-06-08 Lexの裏側でLLMをSageMakerで動かす事例っぽい](https://aws.amazon.com/jp/blogs/machine-learning/exploring-generative-ai-in-conversational-experiences-an-introduction-with-amazon-lex-langchain-and-sagemaker-jumpstart/)
- [2023-07-18 LLMを使った会話型FAQ機能でAmazon Lexを強化](https://aws.amazon.com/jp/blogs/machine-learning/enhance-amazon-lex-with-conversational-faq-features-using-llms/)

## Updates

- [2023-06-06 Amazon Lex Model Building V2向けにAPIアップデート](https://awsapichanges.info/archive/changes/756306-models-v2-lex.html)
- [2023-08-18 Amazon Lexがコンファメーション・スロット・タイプに対応](https://aws.amazon.com/jp/about-aws/whats-new/2023/08/amazon-lex-confirmation-slot-type/)
  - ユーザーからの "Yes "と "No "の回答を効果的に取得できるようにする、Amazon LexのConfirmationスロットタイプの一般提供を発表
  - これまでは、開発者はユーザーからの確認と拒否の応答をキャプチャするためにカスタムスロットを作成する必要がありました。
  - そのため、確認の表現に使用するカスタムスロットに、複数の口語的なフレーズのバリエーションを追加する必要がありました。
  - 例えば、"Yes "のバリエーションをキャプチャするために、開発者は "Yeah"、"That's right"、"Correct "などの複数の同義語を追加していました。
  - 今回の発表により、開発者は確認のためのプロンプトにConfirmation組み込みスロットタイプを直接使用できるようになりました。
