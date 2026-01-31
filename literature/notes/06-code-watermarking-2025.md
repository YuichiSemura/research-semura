# コード透かし（Watermarking）の最新動向（2025年）

## 概要

LLM生成コードに透かしを埋め込み、出自を追跡する研究群。堅牢性（robustness）が主要課題。

## 主要論文

### STONE: Syntax-Aware Watermarking (Feb 2025)

- **URL**: <https://arxiv.org/abs/2502.18851>
- **要点**:
  - 従来手法の問題: 構文トークン（キーワード等）が高エントロピー → ロジック破壊のリスク
  - **非構文トークンのみに透かしを埋め込む**
  - Python/C++/Javaで平均**7.69%改善**（CWEM指標）
- **示唆**: 構文を考慮した透かしが必要。CCFinderSWのトークン分類が応用可能か

### RoSeMary: ML/Crypto Codesign (Feb 2025)

- **URL**: <https://arxiv.org/abs/2502.02068>
- **要点**:
  - ML + 暗号技術のハイブリッド
  - **ゼロ知識証明**で署名を明かさず検証可能
  - 攻撃耐性あり
- **示唆**: 暗号的アプローチは堅牢だが実装コストが高い

### Practical and Effective Code Watermarking (NeurIPS 2025)

- **URL**: <https://github.com/TimeLovercc/code-watermark>
- **要点**:
  - 出自追跡（provenance tracking）フレームワーク
  - 実用的な実装を公開
- **示唆**: 実装参照可能

### Is The Watermarking Of LLM-Generated Code Robust? (2024)

- **URL**: <https://arxiv.org/abs/2403.17983>
- **要点**:
  - **透かしは簡単に除去可能**
  - 変数名変更、デッドコード挿入で**TPR < 50%に低下**
  - 難読化で**AUROC ≈ 0.5**（ランダム同等）
  - 3つの最新手法、2つのLLM、4つのベンチマークで検証
- **示唆**: 透かしの脆弱性は深刻。代替アプローチが必要

### ACW: Efficient and Universal Watermarking (Feb 2024)

- **URL**: <https://arxiv.org/abs/2402.07518>
- **要点**:
  - プラグアンドプレイ、学習不要
  - 意味保存・冪等変換を選択的に適用
  - 複数LLMで動作
  - コード最適化に耐性あり
- **示唆**: 汎用性は高いが、難読化には弱い可能性

## 研究ギャップ

1. 難読化攻撃への根本的な対策がない
2. 透かし検出とクローン検出の統合アプローチがない
3. 透かしなしでの出自追跡（事後検出）の研究が必要
