# StudyLLM

LLMの勉強用リポジトリ

## 大規模言語モデル入門

[大規模言語モデル入門](https://amzn.asia/d/2ewzg0r)

### はじめに

以下で、基本のライブラリをinstall。

```shell
poetry add "transformers[ja,sentencepiece,torch]"
```

|カテゴリ|モデル|タスク|スコアの見方|
|---|---|---|---|
|感情分析|llm-book/bert-base-japanese-v3-marc_ja|テキストのpositive/negativeの判定|スコアが高いほどlabelの可能性が高い|
|言語推論|llm-book/bert-base-japanese-v3-jnli|言語モデルの意味理解能力を評価する|スコアが高いほどlabelの可能性が高い|
|意味的類似度|llm-book/bert-base-japanese-v3-jsts|二つのテキストの類似性を計算|高いほど似てる|
|文埋め込み|llm-book/bert-base-japanese-v3-unsup-simcse-jawiki|文章をベクトルに埋め込む<br>埋め込んだベクトルのコサイン類似度で類似度を測れる。||
|固有表現認識|llm-book/bert-base-japanese-v3-ner-wikipedia-dataset|テキストの固有表現（固有名詞？）を抽出する||
|文章要約|llm-book/t5-base-long-livedoor-news-corpus|文章を要約する||




## References

[大規模言語モデル入門](https://amzn.asia/d/2ewzg0r)
[大規模言語モデル入門Ⅱ〜生成型LLMの実装と評価](https://amzn.asia/d/coRwOc8)