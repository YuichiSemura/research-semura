# LLM生成コードの検出・透かし

## 概要

LLMが生成したコードを識別する技術。透かし（watermark）埋め込みと、事後検出（post-hoc detection）の2アプローチ。

## 主要論文

### ACW: Watermarking for LLM-Generated Code Detection (2024)

- **URL**: <https://arxiv.org/abs/2402.07518>
- **要点**:
  - **学習不要**で汎用的な透かし手法
  - 意味保存・冪等なAST変換を選択的に適用
  - 変換の有無が暗黙の透かしとして機能
  - コードの有用性を維持しつつ、最適化に対して頑健
- **示唆**: AST操作ベースは言語非依存にできる可能性（CCFinderSWと相性良い）

### Is the Watermarking of LLM-Generated Code Robust? (ICLR 2024)

- **URL**: <https://arxiv.org/abs/2403.17983>
- **要点**:
  - **透かしの頑健性を初めて検証**
  - ASTをランダムに書き換える攻撃で透かし除去可能
  - 二値分類器アプローチも議論（LLM生成 vs 人間）
- **示唆**: 透かしは除去可能。事後検出の方が現実的か

### STONE: Syntax-Aware Code Watermarking (2025)

- **URL**: <https://arxiv.org/abs/2502.18851>
- **要点**:
  - 高エントロピートークン（キーワード等）は構文的に重要
  - 構文トークン以外にのみ透かしを埋め込む
  - コードの正確性を維持
- **示唆**: 透かし設計には言語の構文知識が必要

### Detection of LLM-Paraphrased Code (2025)

- **URL**: <https://arxiv.org/abs/2502.17749>
- **要点**:
  - **コーディングスタイル特徴**でLLM生成コードを識別
  - どのLLMが生成したかも特定可能
- **示唆**: LLMにはスタイル的な癖がある → 検出可能

### SoK: Watermarking for AI-Generated Content (2024)

- **URL**: <https://arxiv.org/abs/2411.18479>
- **要点**:
  - AI生成コンテンツ透かしの体系的調査
  - Zero-shot検出 vs Training-based検出
  - Zero-shot: 統計的特徴を利用
  - Training-based: 人間 vs AI のデータで分類器を訓練
- **示唆**: 両アプローチの比較研究が有効

## 研究への応用

1. **クローン検出との融合**: LLM生成コード検出 + クローン検出 = 訓練データ由来の特定
2. **CCFinderSWの拡張**: トークン列の統計的特徴でLLM生成を判定
3. **スタイル分析**: LLM特有のコーディングパターンを定量化
