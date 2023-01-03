# HuggingFace

## Dataset

様々なソースを扱うことが可能。

### csvファイルからDatasetDictを作成する例

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from datasets import Dataset, DatasetDict, ClassLabel

train_base_df = pd.read_csv("train.csv")
train_df, valid_df = train_test_split(train_all_df, test_size=0.1, 
    stratify=train_base_df["label"], random_state=SEED)

# reset_indexしないとindexが特徴量として認識される
train_df = train_df.reset_index(drop=True)
valid_df = valid_df.reset_index(drop=True)

dataset_dict = DatasetDict({
    "train": Dataset.from_pandas(train_df),
    "valid": Dataset.from_pandas(valid_df),
})

# ClassLabelクラスに変換
class_label = ClassLabel(num_classes=2, names=["normal", "hate"])
dataset_dict = dataset_dict.cast_column("label", class_label)
```

- 参考
  - 基本的な使い方は以下を参照
  - [Huggingface Datasets 入門 (2) - データセットの読み込み｜npaka｜note](https://note.com/npaka/n/n17ecbd890cd6#9ZILg)
  - DatasetDictにすればまとめて処理することも可能となる。
    - [Huggingface datasets を使って オリジナルデータでNER - Qiita](https://qiita.com/CivFractal/items/f2f7d8972fa14b152ad4)
  - ラベル部分はClassLabelにしておくと後々便利である。
    - [How to create custom ClassLabels? - 🤗Datasets - Hugging Face Forums](https://discuss.huggingface.co/t/how-to-create-custom-classlabels/13650)

### トークナイザ処理

dataset_dictに対してmapでtokenizerで処理すればinput_ids(トークン系列)やattention_maskが得られる。

```python
from transformers import AutoTokenizer

model_name = "cl-tohoku/bert-base-japanese-whole-word-masking"
max_length = 77

# トークナイザ
tokenizer = AutoTokenizer.from_pretrained(model_name)
def tokenize(batch):
    return tokenizer(batch["text"], padding="max_length", max_length=max_length, truncation=True)
dataset_dict = dataset_dict.map(tokenize, batched=True, batch_size=None)
```

トークナイザの学習時は注意が必要。

- [新しく日本語BERTのトークナイザを学習するときは limit_alphabet に気をつけよう](https://zenn.dev/hellorusk/articles/4513d7aac5b2cd)

### 隠れ次元のベクトルを得る方法

Datasetクラスをうまくイテレーションする方法が分からないため、普通にrangeでforを回す。

modelへの入力時にはtensorに変換が必要で、若干煩雑となる。

modelは、AutoModelForSequenceClassificationなどではなく、普通にAutoModelの方で、ヘッドレスなものを使用する。

出力は、pooler_outputから得る。

pooler_outputの他にlast_hidden_stateがあるがその違いは、pooler_outputは、last_hidden_stateの系列先頭を線形層(入出力同じノード)とtanhを通したものである。

また、last_hidden_stateは、複数あるself-attentionの最終層という意味である。(系列の最後という意味ではないので注意)

```python
import torch
from tqdm import tqdm
from transformers import AutoModel

model_name = "cl-tohoku/bert-base-japanese-whole-word-masking"
model = AutoModel.from_pretrained(model_name)
model.eval()

batch_size = 100
vectors = torch.empty((0, 768))

train_ds = dataset_dict["train"]

with torch.no_grad():
    for i in tqdm(range(0, len(train_ds), batch_size), ascii=True):
        output = model(
            torch.tensor(train_ds[i:i+batch_size]['input_ids']),
            torch.tensor(train_ds[i:i+batch_size]['attention_mask']),
        )
        vectors = torch.concat([vectors, output.pooler_output], axis=0)
```

- 参考記事
  - [【備忘録】PyTorchで黒橋研日本語BERT学習済みモデルを使ってみる - Seitaro Shinagawaの雑記帳](https://snowman-88888.hatenablog.com/entry/2020/08/21/055414)

### モデルのconfig確認

以下で確認できる。ヘッド数や層数、隠れ状態数なども確認可能。

```python
model_name = "cl-tohoku/bert-base-japanese-whole-word-masking"
model = AutoModel.from_pretrained(model_name)
model.config
```

出力は以下

```
BertConfig {
  "_name_or_path": "cl-tohoku/bert-base-japanese-whole-word-masking",
  "architectures": [
    "BertForMaskedLM"
  ],
  "attention_probs_dropout_prob": 0.1,
  "classifier_dropout": null,
  "hidden_act": "gelu",
  "hidden_dropout_prob": 0.1,
  "hidden_size": 768,
  "initializer_range": 0.02,
  "intermediate_size": 3072,
  "layer_norm_eps": 1e-12,
  "max_position_embeddings": 512,
  "model_type": "bert",
  "num_attention_heads": 12,
  "num_hidden_layers": 12,
  "pad_token_id": 0,
  "position_embedding_type": "absolute",
  "tokenizer_class": "BertJapaneseTokenizer",
  "transformers_version": "4.23.1",
  "type_vocab_size": 2,
  "use_cache": true,
  "vocab_size": 32000
}
```

### EvalPrediction

compute_metricsを自作する場合にわたってくるクラス。

例えば以下のように使用する。

```python
    def compute_metrics(pred: EvalPrediction):
        labels = pred.label_ids
        preds = pred.predictions.argmax(-1)
        f1 = f1_score(labels, preds)
        recall = recall_score(labels, preds)
        precision = precision_score(labels, preds, zero_division=0)
        return {"f1_score": f1, "recall": recall, "precision": precision}
    
    # ....

    trainer = Trainer(
        model=model,
        args=training_args,
        tokenizer=tokenizer,
        train_dataset=dataset_dict["train"],
        eval_dataset=dataset_dict["valid"],
        compute_metrics=compute_metrics,
    )
```

定義はコードの以下を参照。

- [https://github.com/huggingface/transformers/blob/v4.23.1/src/transformers/trainer_utils.py#L100](https://github.com/huggingface/transformers/blob/v4.23.1/src/transformers/trainer_utils.py#L100)

### SchedulerType

コードの以下でわかる。

- [https://github.com/huggingface/transformers/blob/v4.23.1/src/transformers/trainer_utils.py#L355](https://github.com/huggingface/transformers/blob/v4.23.1/src/transformers/trainer_utils.py#L355)

```python
class SchedulerType(ExplicitEnum):
    LINEAR = "linear"
    COSINE = "cosine"
    COSINE_WITH_RESTARTS = "cosine_with_restarts"
    POLYNOMIAL = "polynomial"
    CONSTANT = "constant"
    CONSTANT_WITH_WARMUP = "constant_with_warmup"
```

デフォルトは、`"linear"`なので注意が必要。

### MTEB

[https://huggingface.co/blog/mteb](https://huggingface.co/blog/mteb)

- 埋め込むベクトルを生成可能な事前学習モデルを評価するための大規模ベンチマークに使える。
- 112の言語、8つのタスク、58個のデータセットで評価する。
- 個別に使えると、ブログに書くときはかどるかも。
