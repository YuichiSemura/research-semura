# DetectCodeGPT: Zero-Shot Detection of Machine-Generated Code

## 基本情報

- **論文タイトル**: Between Lines of Code: Unraveling the Distinct Patterns of Machine and Human Programmers
- **著者**: Yuling Shi, Hongyu Zhang, Chengcheng Wan, Xiaodong Gu
- **発表**: ICSE 2025 (47th International Conference on Software Engineering)
- **arXiv**: <https://arxiv.org/abs/2310.05103>
- **GitHub**: <https://github.com/YerbaPage/DetectCodeGPT>

## 研究の動機

既存のテキスト向けAI生成検出手法（DetectGPT等）をコードにそのまま適用しても効果が低い。コード特有の統計的性質（構文制約、スタイル規則）を考慮した専用手法が必要。

## 主要な貢献

1. **ゼロショット検出**: 特定のLLM出力での事前学習不要
2. **ブラックボックスLLM対応**: ChatGPT, GPT-4等のAPI経由モデルにも適用可能
3. **スタイリスティックトークンの活用**: 空白・改行等の「見えない」パターンを利用

## 手法の概要

### 背景: DetectGPT（テキスト向け）

- LLM生成テキストは、モデルの対数確率関数の**負の曲率領域**に存在する傾向
- テキストを摂動（perturbation）させ、確率変化のパターンで判定
- 問題: コードには適用困難（構文制約があるため摂動が難しい）

### DetectCodeGPTのアプローチ

```
[入力コード] → [スタイリスティックトークンの摂動] → [確率計算] → [判定]
```

#### Step 1: スタイリスティックトークンの特定

コードの機能に影響しないトークンを摂動対象として選択：

| トークン種類 | 例 |
|-------------|-----|
| 空白 (whitespace) | スペース、タブ |
| 改行 (newline) | `\n` |
| コメント | `// ...`, `/* ... */` |
| 空行 | - |

#### Step 2: 摂動と確率計算

1. スタイリスティックトークンを挿入・削除・変更
2. 代理モデル（surrogate model）で各トークンの確率を推定
3. 摂動前後の確率変化パターンを分析

#### Step 3: 判定

- **LLM生成コード**: 摂動に対して確率が大きく変化
- **人間のコード**: 摂動に対して確率変化が小さい

### なぜスタイリスティックトークンか？

| 観察 | 説明 |
|------|------|
| LLMの傾向 | 学習データの統計的パターンに従い、高確率のトークンを選択 |
| 人間の傾向 | 個人のスタイル・習慣に従い、統計的に「最適」とは限らない選択 |
| 差異が現れる場所 | **スタイリスティックトークン**に顕著（機能には影響しないため自由度が高い） |

## コード特性の分析

論文では、人間とLLMのコードを複数の観点から分析：

### 1. コード長 (Code Length)

- LLM生成コードは長さの分布が異なる
- 特定の長さに集中する傾向

### 2. 言語法則 (Linguistic Laws)

| 法則 | 人間のコード | LLM生成コード |
|------|-------------|--------------|
| Zipf's Law | 適合 | やや異なる |
| Heaps' Law | 適合 | やや異なる |

### 3. トークン分布

- トークン頻度パターンに差異
- 特にスタイリスティックトークンで顕著

### 4. トークンカテゴリ比率

- キーワード、識別子、リテラル等の比率が異なる

### 5. コードの自然性 (Naturalness)

- LLMコードは「自然言語的」な性質が強い
- 人間のコードはより多様

## 実験設定

### データセット

| データセット | 用途 |
|-------------|------|
| CodeSearchNet | 人間のコード収集 |
| The Vault (The Stack前処理版) | 大規模コードコーパス |
| CodeContest | 競技プログラミングコード |
| APPS | プログラミング問題 |

### 評価対象LLM

- text-davinci-003
- GPT-3.5
- GPT-4

### 代理モデル

- CodeLlama-7b（確率推定用）

## 実験結果

### 検出精度

| モデル | 精度 |
|--------|------|
| text-davinci-003 | 高い |
| GPT-3.5 | 高い |
| GPT-4 | 高い |

※ GPTSniffer（学習ベース手法）より高精度

### 制限事項

- **入力長制限**: 最大512トークン
- 長いコードファイルには直接適用困難

## 関連手法との比較

| 手法 | アプローチ | 学習 | コード対応 |
|------|-----------|------|-----------|
| DetectGPT | 確率曲率 | 不要 | 低 |
| Fast-DetectGPT | 条件付き確率曲率 | 不要 | 低 |
| GPTSniffer | 分類器学習 | 必要 | 中 |
| **DetectCodeGPT** | スタイリスティック摂動 | 不要 | **高** |

## CCFinderSWへの示唆

### 直接応用可能な点

1. **スタイリスティックトークンの分析**: CCFinderSWでコメント・空白パターンを抽出可能
2. **トークン分布の差異**: クローン検出とLLM生成判定の組み合わせ

### 拡張アイデア

- CCFinderSWの前処理でスタイリスティックトークンを**保持**するオプション追加
- トークン列の統計的パターンをクローン類似度に組み込む
- LLM生成コードのクローンペア検出時に、生成元LLMの推定も行う

## 技術的要件

```
Python 3.9.7+
Ubuntu 22.04.1 (推奨)
GPU (確率計算用)
```

## ディレクトリ構成

```
DetectCodeGPT/
├── code-generation/   # LLMコード生成
│   └── generate.py
├── code-analysis/     # パターン分析
│   └── (4つの分析スクリプト)
└── code-detection/    # 検出実行
    └── main.py
```

## 制限事項

1. **512トークン制限**: 長いファイルには分割が必要
2. **代理モデル依存**: CodeLlama-7bの性能に依存
3. **計算コスト**: 摂動と確率計算に時間がかかる
4. **言語**: 主にPythonで評価（他言語は未検証）

## 今後の研究方向

1. 長いコードへの対応（チャンク分割等）
2. 多言語対応の評価
3. 検出回避攻撃への耐性評価
4. リアルタイム検出の実現

## 関連リンク

- [arXiv論文](https://arxiv.org/abs/2310.05103)
- [GitHubリポジトリ](https://github.com/YerbaPage/DetectCodeGPT)
- [HuggingFace Blog](https://huggingface.co/blog/YerbaPage/detectcodegpt)
- [DetectGPT (元手法)](https://arxiv.org/abs/2301.11305)
- [Fast-DetectGPT](https://arxiv.org/abs/2310.05130)
