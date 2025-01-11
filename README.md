# StudyLLM

LLMの勉強用リポジトリ

## 大規模言語モデル入門

[大規模言語モデル入門](https://amzn.asia/d/2ewzg0r)

### はじめに

以下で、基本のライブラリをinstall。

```shell
poetry add "transformers[ja,sentencepiece,torch]"
```

#### 各タスクに対するモデルまとめ

|カテゴリ|モデル|タスク|スコアの見方|
|---|---|---|---|
|感情分析|`llm-book/bert-base-japanese-v3-marc_ja`|テキストのpositive/negativeの判定|スコアが高いほどlabelの可能性が高い|
|言語推論|`llm-book/bert-base-japanese-v3-jnli`|言語モデルの意味理解能力を評価する|スコアが高いほどlabelの可能性が高い|
|意味的類似度|`llm-book/bert-base-japanese-v3-jsts`|二つのテキストの類似性を計算|高いほど似てる|
|文埋め込み|`llm-book/bert-base-japanese-v3-unsup-simcse-jawiki`|文章をベクトルに埋め込む<br>埋め込んだベクトルのコサイン類似度で類似度を測れる。||
|固有表現認識|`llm-book/bert-base-japanese-v3-ner-wikipedia-dataset`|テキストの固有表現（固有名詞？）を抽出する||
|文章要約|`llm-book/t5-base-long-livedoor-news-corpus`|文章を要約する||

#### transformersの基本的な使い方

|タスク|モデル|
|---|---|
|トークナイザ|`AutoTokenizer.from_pretrained("abeja/gpt2-large-japanese")`|
|文章生成|`AutoModelForCausalLM.from_pretrained("abeja/gpt2-large-japanese")`|

#### 基本用語

- トークン
  - モデルが使用する基本的な単位
- トークナイゼーション
  - トークンに分割する処理
- トークナイザ
  - トークン単位に分割する実装
- 分布仮説
  - ある単語の意味は周辺に出現する単語によって表せる
- 事前学習
  - 実際に解きたいタスクを学習する前に別のタスクでモデルを学習すること
- 下流タスク
  - 事前学習したモデルを適用する先のタスク、実際に解きたいタスク
- 転移学習
  - 解きたいタスクを別のタスクで学習したモデルで解くこと
- 自己教師あり学習
  - 入力から自動的に予測するラベルを生成して学習する

## References

[大規模言語モデル入門](https://amzn.asia/d/2ewzg0r)
[大規模言語モデル入門Ⅱ〜生成型LLMの実装と評価](https://amzn.asia/d/coRwOc8)