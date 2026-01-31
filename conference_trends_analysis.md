# ICSE・APSEC 研究トレンド分析 (2023-2025)

静的解析・プログラミング言語関連の研究テーマ傾向調査

---

## 1. 概要

### 対象学会
| 学会 | 正式名称 | ランク | 特徴 |
|------|---------|--------|------|
| **ICSE** | IEEE/ACM International Conference on Software Engineering | トップ (A*) | SE分野の最高峰、1975年設立、2025年で50周年 |
| **APSEC** | Asia-Pacific Software Engineering Conference | 地域会議 (B-C) | アジア太平洋地域の主要SE会議、30年の歴史 |

---

## 2. 主要トレンド (2023-2025)

### 🔥 最も顕著なトレンド: **LLM × ソフトウェア工学**

2024年のICSEでは「AI/LLMのソフトウェア工学への応用」が圧倒的な主要テーマでした。2200人以上の参加者（63カ国）のうち、多くの発表がこのテーマに関連していました。

#### LLM関連の研究カテゴリ

| カテゴリ | 割合 | 代表的研究 |
|---------|------|-----------|
| コード生成 | 16.5% | LLM-based code completion, synthesis |
| バグ検出 | 11.7% | 静的解析 + LLM、脆弱性検出 |
| ソフトウェア保守 | 10.7% | 自動修正、リファクタリング |

---

## 3. ICSE トレンド詳細 (2023-2025)

### 3.1 静的解析 + LLM の融合

**ICSE 2025で開催されたSTATICワークショップ**が象徴的です。研究者と産業界が静的解析技術について議論する場として設立されました。

#### 代表的な論文テーマ

**1. LLMによるプログラム修正 (Program Repair)**
- **RepairAgent** (ICSE 2025): 自律的なLLMベースの修正エージェント。従来手法で修正できなかった39件のバグを修正。コストは1バグあたり約14セント
- **D4C** (ICSE 2025): LLMの出力をプログラム修正に最適化。Defects4Jで180件のバグを修正（サンプリング10回のみ）
- **MANIPLE** (ICSE 2025): プロンプトに含める「事実」の最適選択問題を定義

**2. 静的解析によるLLM支援**
- **Planning LLM for Static Detection of Runtime Errors** (ICSE 2025): LLMは静的なコード表現で動作するため、動的な挙動の推論が苦手という課題に対処
- **Monitor-Guided Decoding** (NeurIPS 2023): 静的解析とLLMを組み合わせたコード補完

**3. 脆弱性検出**
- **Vulnerability Detection with Code Language Models** (ICSE 2025): コードLMの脆弱性検出能力を体系的に評価。Claude 3.5, GPT-4o等を含む

### 3.2 年別トピック推移

#### ICSE 2023
- LLM黎明期：ChatGPTの登場直後
- 主なテーマ：
  - 事前学習済みモデルのコードへの応用
  - 自動プログラム修正
  - テスト生成
  - コード類似度検出

#### ICSE 2024
- LLM全盛期：AI/LLMが会議全体の主要テーマに
- 主なテーマ：
  - **UniLog**: LLMによる自動ロギング
  - **Large Language Models for Test-Free Fault Localization**
  - 静的解析ツールの価値の再検証

#### ICSE 2025
- エージェント時代の始まり
- 主なテーマ：
  - **自律エージェント** (RepairAgent等)
  - 静的解析とLLMの統合手法
  - 実用的な脆弱性検出

---

## 4. APSEC トレンド詳細 (2023-2025)

### 4.1 開催情報

| 年 | 開催地 | 参加者 |
|----|--------|--------|
| 2023 | ソウル (韓国) | 300人以上（23カ国） |
| 2024 | 重慶 (中国) | - |
| 2025 | マカオ (中国) | 12月2-5日予定 |

### 4.2 主要トピック

APSECではICSEのトレンドを追従しつつ、以下の特徴があります：

#### Technical Track のトピック
1. **Testing/Verification/Validation** - テスト・検証・妥当性確認
2. **Program Analysis** - プログラム解析
3. **Program Synthesis** - プログラム合成
4. **Program Repairs** - プログラム修正
5. **Formal Methods** - 形式手法
6. **Model-driven Engineering** - モデル駆動開発

#### SEIP (Software Engineering in Practice) Track の焦点
- **AI駆動ソフトウェア工学**
- **自律システムのソフトウェア安全性** (自動運転等)
- **機械学習システムの検証・妥当性確認**
- **サイバーフィジカルシステム**

### 4.3 代表的な採択論文

**APSEC 2023:**
- "An Empirical Study on the Stability of Explainable Software Defect Prediction"
- "Improving Code Refinement for Code Review Via Input Reconstruction and Ensemble Learning"

**APSEC 2024:**
- "Analyzing and Detecting Toxicities in Developer Online Chatrooms"
- その他、LLMを活用したコード解析関連

---

## 5. 静的解析・プログラミング言語研究の具体的トレンド

### 5.1 ホットトピック (投稿推奨)

| トピック | 熱度 | 説明 |
|---------|------|------|
| **LLM + 静的解析のハイブリッド** | ⭐⭐⭐⭐⭐ | 最も注目度が高い。静的解析の結果をLLMに入力、またはLLMの出力を静的解析で検証 |
| **LLMベースのプログラム修正** | ⭐⭐⭐⭐⭐ | ICSE 2025で複数の論文が採択 |
| **コード脆弱性検出** | ⭐⭐⭐⭐ | セキュリティ意識の高まりと共に増加 |
| **テスト自動生成** | ⭐⭐⭐⭐ | LLMによるテストケース生成 |
| **コード理解・要約** | ⭐⭐⭐ | ドキュメント自動生成等 |

### 5.2 技術的アプローチ

**よく使われる手法:**
- Transformer アーキテクチャ
- Graph Neural Networks (コード構造解析)
- 強化学習 (RLVR: Reinforcement Learning from Verifiable Rewards)
- In-Context Learning
- Chain-of-Thought Prompting

**よく使われるベンチマーク:**
- Defects4J (Java バグデータセット)
- BugsInPy (Python バグデータセット)
- BigVul, Devign (脆弱性データセット)

---

## 6. 投稿戦略の提案

### APSEC向け (現実的な投稿先として)

**推奨テーマ:**
1. **LLMを活用した静的解析の改善**
   - 既存の静的解析ツールの誤検知削減
   - 解析結果の説明生成

2. **プログラム修正の自動化**
   - 特定のバグパターンに特化した修正
   - 日本語コメント/ドキュメントを含むコードの処理

3. **機械学習システムの品質保証**
   - APSECのSEIPトラックで重視されているテーマ

4. **形式手法 × LLM**
   - 形式仕様の自動生成
   - モデル検査との統合

### 差別化のポイント

- **日本/アジアのコンテキスト**: 日本語を含むコード、日本の開発プラクティス
- **産業応用**: 実際のプロジェクトでの評価
- **ツール実装**: 使えるツールとしての公開

---

## 7. 参考文献・リンク

### 学会公式サイト
- [ICSE 2025](https://conf.researchr.org/home/icse-2025)
- [ICSE 2024](https://conf.researchr.org/home/icse-2024)
- [APSEC 2025](https://conf.researchr.org/home/apsec-2025)
- [APSEC 2024](https://conf.researchr.org/home/apsec-2024)
- [APSEC 2023](https://conf.researchr.org/home/apsec-2023)

### 関連論文リスト
- [AwesomeLLM4SE](https://github.com/iSEngLab/AwesomeLLM4SE) - LLM for SE論文の包括的リスト
- [Awesome-Code-LLM](https://github.com/codefuse-ai/Awesome-Code-LLM) - コードLLM研究のキュレーションリスト
- [ML4SE](https://github.com/saltudelft/ml4se) - 機械学習×SE論文・データセット・ツール集

### ワークショップ
- [STATIC 2025](https://conf.researchr.org/home/icse-2025/static-2025) - 静的解析ワークショップ
- [LLM4Code 2026](https://llm4code.github.io/) - LLM for Codeワークショップ

### 参考統計
- 2028年までに企業のソフトウェアエンジニアの90%がAIコードアシスタントを使用予定 (Gartner)
- 2025年時点で90%以上の開発チームがAIツールを使用

---

## 8. まとめ

### 2023-2025年の全体的な流れ

```
2023: LLM黎明期
  ↓ ChatGPTの登場でコード生成に注目集まる
2024: LLM全盛期
  ↓ SE研究の主流がLLM応用に
2025: エージェント時代
  → 自律的なAIエージェントによるプログラミング支援
```

### 静的解析研究者へのインプリケーション

1. **純粋な静的解析研究は減少傾向** - LLMとの組み合わせが必須に
2. **静的解析の新たな役割** - LLMの出力検証、LLMへのコンテキスト提供
3. **形式手法との融合** - LLMの弱点（論理的推論）を形式手法で補完

---

*作成日: 2026年1月31日*
*調査対象期間: 2023年〜2025年*
