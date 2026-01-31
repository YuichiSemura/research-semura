# LLMによるクローン検出（LLMを検出器として使う）

## 概要

LLMをクローン検出器として使用する研究群。従来のトークンベース/ASTベース手法とは異なり、LLMの意味理解能力を活用。

## 主要論文

### An Empirical Study of LLM-Based Code Clone Detection (2025)

- **URL**: <https://arxiv.org/abs/2511.01176>
- **要点**:
  - 5つのLLM（o3-mini含む）を7つのデータセットで評価
  - o3-miniがCodeNet関連でF1=0.943達成
  - BigCloneBench関連では性能低下 → **汎化性能に課題**
  - 応答一貫性は90%以上
- **示唆**: データセット依存性が高い。実用には複数ベンチマークでの評価が必要

### Assessing the Code Clone Detection Capability of LLMs (2024)

- **URL**: <https://arxiv.org/abs/2407.02402>
- **要点**:
  - GPT-3.5 vs GPT-4をBigCloneBench + GPTCloneBenchで評価
  - GPT-4が一貫して優位
  - **LLM生成コードのクローン検出は得意**（人間のより高精度）
  - Type-4（意味的クローン）は依然苦手
- **示唆**: LLM生成コードには検出しやすい特徴がある？

### The Struggles of LLMs in Cross-lingual Clone Detection (2024)

- **URL**: <https://arxiv.org/abs/2408.04430>
- **要点**:
  - 5つのLLM × 8プロンプトで多言語クローン検出を評価
  - **embeddingモデルがLLMを上回る**（1〜20%pt差）
  - LLMは「クローン」の意味を理解していない可能性
- **示唆**: 多言語対応にはCCFinderSWのようなトークンベースが有効か

### HyClone (2025)

- **URL**: <https://arxiv.org/abs/2508.01357>
- **要点**:
  - LLMは構文差異に惑わされて意味的クローンを見逃す
  - テストケース実行で機能的等価性を検証するアプローチ
- **示唆**: 静的解析だけでは限界。動的解析との組み合わせ

## 研究ギャップ

1. トークンベースクローン検出（CCFinderSW的）をLLM生成コードに適用した研究がない
2. LLM生成コード同士のクローン検出は未開拓
3. 検出精度とコスト（API呼び出し）のトレードオフ分析が不足
