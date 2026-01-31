# LLMのmemorization・訓練データ抽出

## 概要

LLMが訓練データを「記憶」し、出力として再現してしまう問題。著作権・プライバシーの観点から重要。コードも対象。

## 主要論文

### Extracting Training Data from Large Language Models (2021) ⭐基礎論文

- **URL**: <https://arxiv.org/abs/2012.07805>
- **著者**: Carlini et al. (Google Brain)
- **要点**:
  - GPT-2から訓練データを抽出する攻撃を実証
  - 抽出できたもの: **コード**、PII（名前、電話番号、メール）、IRCログ、UUID
  - モデルサイズが大きいほど記憶しやすい
- **示唆**: LLM生成コードにはオリジナルの訓練データが含まれる可能性

### The Landscape of Memorization in LLMs (2025) ⭐SoK

- **URL**: <https://arxiv.org/abs/2507.05578>
- **要点**:
  - memorization研究の体系的調査
  - メカニズム、測定方法、緩和策を整理
  - **モデルサイズとmemorization量は対数線形関係**
- **示唆**: 大規模LLM（GPT-4等）ほどコード記憶のリスク高

### MemHunter (2024)

- **URL**: <https://arxiv.org/abs/2412.07261>
- **要点**:
  - 小さなLLMで「記憶誘発プロンプト」を自動生成
  - 既存手法より**40%多く訓練データを抽出**
  - データセットスケールでの検出が可能
- **示唆**: memorization検出の自動化が進んでいる

### Malicious and Unintentional Disclosure Risks (2025) ⭐コード特化

- **URL**: <https://arxiv.org/abs/2503.22760>
- **要点**:
  - コード生成LLMにおける情報漏洩リスクを分析
  - 「意図しない開示」と「悪意ある開示」を区別
- **示唆**: コード生成特有のリスクモデルが必要

### Special Characters Attack (2024)

- **URL**: <https://arxiv.org/abs/2405.05990>
- **要点**:
  - 特殊文字を使った攻撃で訓練データ抽出
  - コード、Webページ、PIIが抽出可能
- **示唆**: アライメント済みモデルでも攻撃可能

## 研究への応用

1. **クローン検出との接続**: memorizedコード = 訓練データからのクローン
2. **CCFinderSWの応用**: LLM出力と訓練データ候補のクローン検出
3. **出自追跡**: どの訓練データソースに由来するか特定
