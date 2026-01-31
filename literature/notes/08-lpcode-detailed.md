# LPcode: LLM-Paraphrased Code Detection via Coding Style Features

## 基本情報

- **論文タイトル**: Detection of LLM-Paraphrased Code and Identification of the Responsible LLM Using Coding Style Features
- **著者**: Shinwoo Park, Hyundong Jin, Jeong-won Cha, Yo-Sub Han
- **発表**: Engineering Applications of Artificial Intelligence, Vol. 162, December 2025
- **arXiv**: <https://arxiv.org/abs/2502.17749>
- **GitHub**: <https://github.com/Shinwoo-Park/detecting_llm_paraphrased_code_via_coding_style_features>

## 研究の動機

LLMを悪用して他人のコードを「パラフレーズ」（機能を保ったまま書き換え）し、知的財産権を侵害する可能性がある。このような行為を検出する研究は限られている。

## 2つのタスク

| タスク | 内容 | 難易度 |
|--------|------|--------|
| **Task 1** | LLM生成コードが人間のコードのパラフレーズかどうか判定（二値分類） | 比較的容易 |
| **Task 2** | どのLLMがパラフレーズに使われたか特定（多クラス分類） | 困難 |

## LPcodeデータセット

### 構成

| 言語 | Human | ChatGPT | Gemini-Pro | WizardCoder | DeepSeek-Coder | 計 |
|------|-------|---------|------------|-------------|----------------|-----|
| C | 457 | 457 | 457 | 457 | 457 | 2,285 |
| C++ | 385 | 385 | 385 | 385 | 385 | 1,925 |
| Java | 1,494 | 1,494 | 1,494 | 1,494 | 1,494 | 7,470 |
| Python | 1,935 | 1,935 | 1,935 | 1,935 | 1,935 | 9,675 |
| **合計** | | | | | | **21,355** |

### データ収集方法

1. **人間コード**: GitHub（2019年1月〜2020年1月）からApache/BSD/MITライセンスのコードを収集
2. **LLMパラフレーズ**: 4つのLLM（GPT-3.5, Gemini-Pro, WizardCoder-33B, DeepSeek-Coder-33B）に「機能を保ったままパラフレーズ」を指示
3. **前処理**: 構文検証、重複削除、機密データ匿名化

## コーディングスタイル特徴（10個）

### 1. 命名規則 (Naming Consistency) - 4特徴

| 特徴 | 説明 |
|------|------|
| 関数名の命名一貫性 | snake_case / camelCase / PascalCase の頻度分布 |
| 変数名の命名一貫性 | 同上 |
| クラス名の命名一貫性 | 同上 |
| 定数名の命名一貫性 | 同上 |

### 2. コード構造 (Code Structure) - 3特徴

| 特徴 | 説明 |
|------|------|
| インデント一貫性 | 最頻インデント長 / 全インデントパターン数 |
| 関数長 | 関数あたりの平均行数 |
| ネスト深度 | ループ・条件分岐の平均ネストレベル |

### 3. 可読性 (Readability) - 3特徴

| 特徴 | 説明 |
|------|------|
| **コメント比率** | コメント行数 / 総行数（**最重要特徴**） |
| 関数名長 | 関数名の平均文字数 |
| 変数名長 | 変数名の平均文字数 |

## ANOVA統計分析の結果

### 最も有意な差を示す特徴

| 言語 | 最重要特徴 | F統計量 |
|------|-----------|---------|
| **全言語共通** | コメント比率 | 最高 |
| C | 関数長 | - |
| C++ | クラス命名一貫性 | - |
| Java | 変数命名一貫性 | - |
| Python | 関数長 | - |

### LLMと人間の違い

- **LLM**: 構造化された反復的なコメントスタイル。一貫性が高い
- **人間**: 開発者によって大きく異なる。コメントなし〜詳細な説明まで様々

## LPcodedec検出手法

### 特徴

1. **説明可能性**: 10個の数値特徴は解釈可能（ブラックボックスではない）
2. **効率性**: 大規模embedding不要。10個の数値特徴のみ使用

### 分類器

- Random Forest / XGBoost / LightGBM などで学習
- 特徴量エンジニアリングが鍵

## 実験結果

### Task 1: パラフレーズ検出（F1スコア）

| 言語 | LPcodedec | Tree Edit Distance | 高速化 |
|------|-----------|-------------------|--------|
| C | 87.52% | - | - |
| C++ | 88.39% | - | - |
| Java | 91.13% | - | - |
| Python | 93.16% | - | - |
| **平均改善** | +2.64% | baseline | **1,343x** |

### Task 2: LLM特定（F1スコア）

| 言語 | LPcodedec | TF-IDF baseline | 高速化 |
|------|-----------|-----------------|--------|
| C | 43.13% | - | - |
| C++ | 39.36% | - | - |
| Java | 45.19% | - | - |
| Python | 42.41% | - | - |
| **平均改善** | +15.17% | baseline | **213x** |

※ Task 2は依然として困難（F1 < 50%）

## CCFinderSWへの示唆

### 直接応用可能な点

1. **コメント比率**: CCFinderSWのトークナイザでコメントトークンをカウント可能
2. **命名規則分析**: 識別子トークンの抽出・分類が可能
3. **インデント一貫性**: 字句解析レベルで計測可能

### 拡張アイデア

- CCFinderSWのトークン列にLPcodedecの特徴量を追加
- クローン検出と同時にLLM生成判定を行う統合ツール
- Type-3クローンの検出精度向上にコーディングスタイル特徴を活用

## 制限事項

1. Task 2（LLM特定）の精度が低い（F1 < 50%）
2. 4つのLLMのみ評価（Claude, Llama等は未検証）
3. 難読化・最適化への耐性は未評価

## 関連リンク

- [arXiv論文](https://arxiv.org/abs/2502.17749)
- [GitHubリポジトリ](https://github.com/Shinwoo-Park/detecting_llm_paraphrased_code_via_coding_style_features)
- [ScienceDirect (出版版)](https://www.sciencedirect.com/science/article/abs/pii/S0952197625024856)
