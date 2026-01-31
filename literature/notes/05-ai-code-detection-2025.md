# AI生成コード検出の最新動向（2025年）

## 概要

LLM生成コードを識別・検出する研究群。透かし（watermarking）、スタイル分析、構造的特徴の3つのアプローチが主流。

## 主要論文

### Detection of LLM-Paraphrased Code (LPcode) (Feb 2025)

- **URL**: <https://arxiv.org/abs/2502.17749>
- **要点**:
  - LLMによるコードのパラフレーズ（盗用目的）を検出
  - **コーディングスタイル特徴**（命名規則、インデント、コメント）で識別可能
  - LLM特定（どのLLMが生成したか）も可能
  - 従来手法より**1,343倍高速**
- **示唆**: スタイル特徴はCCFinderSWのトークン解析と組み合わせ可能か

### AI Code in the Wild (Dec 2025)

- **URL**: <https://arxiv.org/abs/2512.18567>
- **要点**:
  - GitHub Top 1000リポジトリ（2022-2025）を大規模分析
  - AI生成コードは**glueコード・テスト・リファクタリング・ドキュメント**に集中
  - コアロジック・セキュリティ関連は人間が担当
  - 高精度検出パイプラインを構築
- **示唆**: AI生成コードの「棲み分け」が明確。検出対象を絞れる

### The Hidden DNA of LLM-Generated JavaScript (Oct 2025)

- **URL**: <https://arxiv.org/html/2510.10493>
- **要点**:
  - **データフローとn-gramにモデル固有の指紋**が残る
  - 表面的な字句特徴ではなく構造的特徴で識別
  - モデルごとの「癖」が存在
- **示唆**: トークンベース解析で捉えられる可能性あり

### DetectCodeGPT (ICSE 2025)

- **URL**: <https://github.com/YerbaPage/DetectCodeGPT>
- **要点**:
  - ゼロショットでの機械生成コード検出
  - 学習データ不要
- **示唆**: ベースライン比較に有用

### An Empirical Study on Automatically Detecting AI-Generated Source Code (Nov 2024)

- **URL**: <https://arxiv.org/abs/2411.04299>
- **要点**:
  - Fine-tuned ChatGPTで80%以上の精度（一部データセット）
  - **高temperatureで生成されたコードの方が検出しやすい**
  - 全体的に既存検出器の有効性は限定的
- **示唆**: 温度パラメータが検出に影響。実験設計で考慮必要

### AIGCodeSet: A New Annotated Dataset (Dec 2024, updated May 2025)

- **URL**: <https://arxiv.org/abs/2412.16594>
- **要点**:
  - AI生成コード検出用のアノテーション付きデータセット
  - 研究用リソースとして公開
- **示唆**: 実験に利用可能

## 研究ギャップ

1. トークンベース手法でのLLM生成コード分析は未開拓
2. 生成コード同士のクローン関係の分析が不足
3. コーディングスタイル特徴の体系的な分類が必要
