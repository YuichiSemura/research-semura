# LLMによるマイナー・難読プログラミング言語のコード生成問題

## 背景

LLMはPythonやJavaScriptなど主流言語では高い性能を示すが、マイナー言語（Low-Resource Programming Languages: LRPLs）や難読言語（Esoteric Languages）では性能が大幅に低下する。

**問題の規模**
- Rustだけでも350万人のユーザーが影響を受ける
- LLMは言語非依存の問題を解く際、90〜97%の確率でPythonを選択（Pythonへの極端な偏り）
- MultiPL-Eベンチマークにおいて、LRPLsのスコアはPythonと比較して著しく低い

## 研究の問い（候補）

### Q1: マイナー言語でのLLM性能低下の定量的分析

- どの言語でどの程度性能が低下するか？
- 言語の特性（型システム、パラダイム等）と性能の関係
- 訓練データ量と性能の相関

### Q2: 難読言語を用いたLLMの推論能力評価

- 訓練データにほぼ存在しない言語でLLMは推論できるか？
- ドキュメントと例示のみでコード生成は可能か？
- 言語仕様の理解と応用能力の限界

### Q3: 低コストな性能改善手法の比較

- In-context learning vs ファインチューニング
- 合成データ生成による補強
- クロスリンガル転移学習の有効性

### Q4: プログラミング言語設計への示唆

- LLM時代に適した言語設計とは？
- ドキュメントの書き方がLLM性能に与える影響

## ベンチマーク: MultiPL-E

**概要**
- HumanEvalとMBPPを18言語に翻訳した多言語コード生成ベンチマーク
- IEEE Transactions on Software Engineering掲載

**対象言語（19言語）**
- Python（基準）+ 18言語
- 含まれるLRPLs: Rust, R, Haskell, Julia, Lua, Racket等

**主な知見**
- モデルのperplexityと生成コードの正確性は強く相関しない
- 型アノテーションの影響は限定的
- 言語の人気度と性能は相関するが、ニッチ言語でも高性能なケースあり

**リソース**
- GitHub: https://github.com/nuprl/MultiPL-E
- 公式ドキュメント: https://nuprl.github.io/MultiPL-E/

## 関連研究

### サーベイ論文

**A Survey on LLM-based Code Generation for Low-Resource and Domain-Specific Programming Languages**
- 掲載: ACM TSEM (2024)
- 内容: LRPLsとDSLに対するLLMコード生成の包括的サーベイ。改善手法（ファインチューニング、in-context learning）を体系的に整理
- URL: https://arxiv.org/abs/2410.03981

### 難読言語

**In-Context Learning for Esoteric Programming Languages**
- 掲載: NeurIPS 2025
- 対象言語: Minipy, Pyth, Rhokell, 0815
- 主な結果:
  - Pythの精度: 16.67% → 30.82%（self-scaffoldingで改善）
  - MinipyのHumanEval精度: 51% → 65%
- URL: https://openreview.net/forum?id=wj9ccBP4uY

### 改善手法

**Enhancing Code Generation for Low-Resource Languages: No Silver Bullet**
- 掲載: arXiv (2025)
- 内容: 5つの改善戦略（in-context learning 3種 + ファインチューニング 2種）を比較
- 結論:
  - 小規模モデル（~1B）→ ファインチューニングが有効
  - 大規模モデル（30B+）→ in-context learningが安全かつ低コスト
- URL: https://arxiv.org/abs/2501.19085

### Haskell特化

**Investigating the Performance of Language Models for Completing Code in Functional Programming Languages: a Haskell Case Study**
- 掲載: 2024
- 内容: Haskellコード補完の性能評価。ファインチューニングで改善するが、高リソース言語には遠く及ばない

### LLMの言語バイアス

**LLMs Love Python: A Study of LLMs' Bias for Programming Languages**
- 掲載: arXiv (2025)
- 内容: LLMが言語非依存の問題で90〜97%の確率でPythonを選択する傾向を分析
- URL: https://arxiv.org/abs/2503.17181

## 具体的なアプローチ案

### アプローチA: ベンチマーク拡張

- MultiPL-Eに日本発の言語（Ruby等）や難読言語を追加
- より詳細な言語特性と性能の相関分析

### アプローチB: 低コスト改善手法の提案

- 少量のドキュメント+例示でどこまで性能改善できるか
- プロンプトエンジニアリングの体系化

### アプローチC: 言語設計ガイドライン

- LLM時代のプログラミング言語設計指針
- ドキュメント作成のベストプラクティス

## 実現可能性メモ

- 強み: 既存ベンチマーク（MultiPL-E）が利用可能
- 必要なもの: LLM APIアクセス、多言語の評価環境
- 難易度: 中（既存フレームワークの拡張として実施可能）

## 次のアクション

1. [ ] MultiPL-Eを実際に動かして現状把握
2. [ ] サーベイ論文（arXiv:2410.03981）を精読
3. [ ] 対象言語の選定（日本発言語、DSL、難読言語）
4. [ ] 小規模な予備実験のデザイン
