# CCFinderSWの引用状況分析

## 基本情報

- **論文**: CCFinderSW: Clone Detection Tool with Flexible Multilingual Tokenization
- **発表**: APSEC 2017
- **著者**: Semura, Yoshida, Choi, Inoue
- **GitHub**: <https://github.com/YuichiSemura/CCFinderSW>

## 引用の傾向

### 1. ベースライン比較として使用

多くの研究でCCFinderSWはトークンベースクローン検出のベースラインとして使用されている。

#### SolaSim (ICPC 2024)

- **URL**: <https://dl.acm.org/doi/10.1145/3643916.3644406>
- **内容**: Solanaスマートコントラクトのクローン検出
- **CCFinderSWへの言及**:
  - Type-1/2クローンのみ対応、**Type-3に弱い**と指摘
  - 「diffツールであり、コントラクトレベルの類似度比較には不向き」
  - CFG/MIRの制御依存性を捉えられない
  - ただし、copy-and-paste操作が多いエコシステムでは有効性あり
- **示唆**: Type-3対応の拡張が研究機会

#### GraphBinMatch (May 2024)

- **内容**: グラフベースの多言語バイナリ・ソースコードマッチング
- **CCFinderSWへの言及**: トークンベース手法の代表として比較

#### CloneBAS (Oct 2023)

- **内容**: AST + Simhashベースのクローン検出
- **CCFinderSWへの言及**: トークンベース手法との比較

### 2. 多言語対応の参照

CCFinderSWの「柔軟な多言語トークナイザ」は複数の論文で参照されている。

- 文法規則を正規表現に変換するアプローチが評価されている
- **制限**: コメント構文が正規表現で表現できない言語はサポート不可

### 3. CCFinderファミリーの文脈

#### A Retrospective on Developing Code Clone Detector CCFinder and Its Impact (IEEE TSE, March 2025)

- **URL**: <https://ieeexplore.ieee.org/document/10817125/>
- **著者**: Kamiya, Kusumoto, Inoue
- **内容**: CCFinderがなぜ広く引用され続けるかの振り返り
- CCFinder → CCFinderX → CCFinderSW の系譜を整理
- クローン検出研究コミュニティへの影響を分析

## 引用研究での指摘（課題）

| 課題 | 指摘元 | 対応可能性 |
|------|--------|-----------|
| Type-3クローン非対応 | SolaSim | 意味的類似度の追加 |
| コントラクトレベル比較不可 | SolaSim | 集約アルゴリズムの追加 |
| CFG/制御依存性の欠如 | SolaSim | 静的解析との統合 |
| 特定言語のコメント構文非対応 | 複数 | 正規表現の拡張 |

## 研究機会

1. **LLM生成コードへの適用**: 引用研究にLLM生成コード分析はない → 未開拓領域
2. **Type-3対応拡張**: 多くの研究で指摘される弱点 → 改善余地あり
3. **スマートコントラクト対応**: Solana以外（Ethereum等）への適用
4. **多言語embedding統合**: トークンベース + embeddingのハイブリッド

## 最近の引用論文リスト

| 年月 | 論文 | 用途 |
|------|------|------|
| 2025/01 | Sedgi Omer, Asmaa Y. Hammo | - |
| 2024/10 | Git Commit Logs分析 (Yokomori, Inoue) | クローン不整合検出 |
| 2024/06 | SolaSim (Wang et al.) | ベースライン比較 |
| 2024/05 | GraphBinMatch (Tehrani et al.) | ベースライン比較 |
| 2023/10 | CloneBAS (He et al.) | ベースライン比較 |
