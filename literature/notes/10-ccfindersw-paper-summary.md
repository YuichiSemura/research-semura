# CCFinderSW: Clone Detection Tool with Flexible Multilingual Tokenization

## 論文情報

- **タイトル**: CCFinderSW: Clone Detection Tool with Flexible Multilingual Tokenization
- **発表**: APSEC 2017 (24th Asia-Pacific Software Engineering Conference), pp. 654-659
- **著者**: Yuichi Semura, Norihiro Yoshida, Eunjong Choi, Katsuro Inoue
- **所属**: 大阪大学 大学院情報科学研究科
- **DOI**: 10.1109/APSEC.2017.80
- **GitHub**: <https://github.com/YuichiSemura/CCFinderSW>

## アブストラクト

これまで、ソースコード中のコードクローンを検出するための多くのツールが開発されてきた。既存のクローン検出ツールは**限られた数のプログラミング言語のみをサポート**しており、追加の言語を扱うための簡単な拡張メカニズムを提供していない。しかし、**産学連携の経験から、多くの実務者が様々な言語で書かれたソースコードを分析する必要がある**ことがわかった。本論文では、実務者からの要望に応じて追加言語を扱う**拡張メカニズムを持つクローン検出ツールCCFinderSW**を提案する。

## 背景と動機

### 問題意識

1. **既存ツールの言語サポートの限界**
   - 従来のクローン検出ツールは対応言語が限定的
   - 新しい言語への対応には字句解析器（レキサー）の実装が必要
   - この実装には多大な時間と労力がかかる

2. **産業界のニーズ**
   - 産学連携の経験を通じて、実務者が多様な言語のソースコード分析を必要としていることが判明
   - 様々なプログラミング言語で書かれたコードを統一的に分析したい

3. **既存手法の課題**
   - CCFinder、CCFinderXは優れたツールだが、言語追加の拡張が困難
   - 各言語専用の字句解析器が必要で、メンテナンスコストが高い

### 研究目標

**より簡単な拡張メカニズム**を持ち、プログラミング言語間の字句的な差異を設定ファイルとして入力できるクローン検出ツールの開発。

## 技術的アプローチ

### クローン検出プロセス（4段階）

1. **字句解析（Lexical Analysis）**
   - コメント除去
   - トークン化
   - 識別子の区別（型・変数関連の識別子を置換）

2. **変換（Transformation）**
   - 識別子の正規化
   - Type-2クローン検出のための前処理

3. **検出（Detection）**
   - n-gramアルゴリズムを採用
   - 高速なクローンペア検出を実現

4. **整形（Formatting）**
   - 検出結果の出力

### 柔軟な多言語対応

- **オプションファイル方式**: 各言語専用の字句解析機構を持たず、設定ファイルで言語ごとにカスタマイズ
- **ユーザーによるカスタマイズ**: オプションファイルはユーザーが修正可能
- **設定可能な項目**:
  - コメント構文
  - 識別子名のルール
  - 予約語（キーワード）

### n-gramによる高速検出

- 統計的自然言語処理で頻用されるn-gramを採用
- 連続する文字列の出現頻度を調査
- スケーラビリティ問題に対処

### ANTLR文法ファイルの活用

- パーサジェネレータANTLRの文法ファイルを利用した多言語検出
- **43言語中39言語を正しく解析可能**

## 検出可能なクローンタイプ

| タイプ | 定義 | CCFinderSW対応 |
|--------|------|----------------|
| Type-1 | 空白・レイアウト・コメント以外は同一 | 対応 |
| Type-2 | 識別子・リテラル・型名の差異を許容 | 対応 |
| Type-3 | 文の挿入・削除・変更を含む | **非対応** |
| Type-4 | 意味的に等価だが構文的に異なる | 非対応 |

## 制限事項

1. **Type-3クローン非対応**: 字句解析の変更のみをサポートするため、構文的な差異を含むクローンは検出不可
2. **コメント構文の制約**: 正規表現で表現できないコメント構文を持つ言語はサポート不可
3. **制御依存性の欠如**: CFG（制御フローグラフ）に基づく分析は行わない

## CCFinderファミリーの系譜

```
CCFinder (TSE 2002)
    ↓
CCFinderX (インタラクティブ環境)
    ↓
CCFinderSW (APSEC 2017) ← 本論文
    - 柔軟な多言語トークナイザ
    - ポータブルで様々な環境で実行可能
    - Javaで実装
```

## 動作要件

- Java Runtime Environment (>= 8)
- クロスプラットフォーム対応

## 参考文献

- [IEEE Xplore](https://ieeexplore.ieee.org/document/8305997/)
- [Semantic Scholar](https://www.semanticscholar.org/paper/CCFinderSW:-Clone-Detection-Tool-with-Flexible-Semura-Yoshida/b058b83c837938b9054353161a06ce0df41b8f6a)
- [ResearchGate](https://www.researchgate.net/publication/323566622_CCFinderSW_Clone_Detection_Tool_with_Flexible_Multilingual_Tokenization)
- [大阪大学 研究DB](https://sel.ist.osaka-u.ac.jp/lab-db/betuzuri/archive/1104/1104.pdf)
