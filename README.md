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


- トークナイぜーション
  - トークン
    - モデルが使用する基本的な単位
  - トークナイゼーション
    - トークンに分割する処理
  - トークナイザ
    - トークン単位に分割する実装
- 事前学習
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
  - 事前学習済み言語モデル
    - 文脈化単語埋め込みを計算するTransformerを大規模コーパスでの自己教師あり学習で事前学習したもの（が最近は定番）。Transformerの出力からタスク固有の出力に変換するものをヘッドという。
- チューニング
  - ファインチューニング
    - 事前学習されたモデルを下流タスクのデータセットで微調整すること
  - プロンプトエンジニアリング
    - ファインチューニングせずに、事前学習された大規模言語モデルをプロンプトを通じて制御し下流タスクを解くこと
    - one-shoe学習
      - プロンプトで例示を一つ与える
    - zero-shot学習
      - プロンプトで例示を与えない
    - few-shot学習
      - プロンプトで複数の例示を与える
  - アラインメント
    - 人間社会にとって理想的な回答になるよう調整すること
    - HHH（役立つこと、正直であること、無害であること）
    - 指示チューニング
      - 指示と理想解答を組みにしてファインチューニングする
    - RLHF
      - 人間の好みに対して直接的に最適化するアライメント手法
    - alignment tax
      - RLHFのようにアライメント後に特定のタスクで性能が低下すること

### Language Moddel

|モデル名|モデル|概要|
|---|---|---|
|GPT2|`abeja/gpt2-large-japanese`|Transformerで次トークンの確率を予測。事前学習とfine turningの目的関数を和にして一度に学習すると性能向上。|
|BERT|`cl-tohoku/bert-base-japanese-v3`|マスク言語モデリング＋次文予測の二つのタスクで事前学習。|
|RoBERTa|`FacebookAI/roberta-base`|マスク言語モデリングは寄与しなかったので、次文予測のタスクのみで事前学習。|
|SpanBERT||マスク言語モデリングの穴埋めをトークン単位ではなく、連続したトークン単位（スパン単位）に変更|
|DeBERTa|`"microsoft/deberta-v3-base"`|kaggleでよく使われるらしい|
|T5|`retrieva-jp/t5-large-long`|"感情分析:この映画は面白い"のようにタスクを接頭語に入れるtext-to-text形式。|
|multilingual BERT||BERTの多言語ver|
|XLM-RoBERTa||RoBERTaの多言語ver|
|mT5||T5の多言語ver|

### トークナイぜーション

|手法|解説|
|---|---|
|バイト対符号化|一文字ずつからだんだん隣り合う言葉同士を結合するイメージ<br>1.一文字ずつに分ける<br>2.隣接した回数が多いものを探す<br>3.探したものを組みにして語彙に追加<br>4.2,3を繰り返す|
|WordPiece|基本はバイト対符号化と同じだが、隣り合う頻度ではなく、結合前のワードの頻度も加味したスコアで実施する|

日本語は、形態素解析などで単語に分割してからこれらを使うことが多い。

## References

- [大規模言語モデル入門](https://amzn.asia/d/2ewzg0r)
- [大規模言語モデル入門Ⅱ〜生成型LLMの実装と評価](https://amzn.asia/d/coRwOc8)