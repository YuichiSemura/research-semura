# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## リポジトリ概要

博士論文に向けた研究テーマ探索・管理用リポジトリ。ソフトウェアプロジェクトではなく、文献調査・アイデア管理が主目的。

**研究者背景**: CCFinderSW（多言語対応クローン検出ツール）の開発経験

**メインテーマ候補**: LLM生成コードにおけるクローン問題

- LLM生成コードのクローン検出
- コードの出自（provenance）追跡
- 著作権・ライセンス問題

## ディレクトリ構造

```
research-semura/
├── literature/
│   ├── papers.bib           # BibTeX文献管理
│   └── notes/               # 論文要約メモ（01-xxx.md形式）
├── ideas/                   # 研究テーマ別アイデアメモ
├── experiments/             # 実験用コード・データ（将来）
└── conference_trends_analysis.md  # 学会動向分析
```

## 作業パターン

### 文献ノート追加

`literature/notes/`に連番でファイル作成（例: `10-new-paper.md`）

### 研究アイデア更新

`ideas/`内の該当ファイルに追記。「次のアクション」セクションのチェックリスト管理を維持

### 引用追加

`literature/papers.bib`にBibTeX形式で追加

## 現在の研究テーマ

1. **LLM生成コードのクローン検出** (`ideas/clone-detection-llm.md`)
   - CCFinderSWの拡張としてLLM生成コード検出機能を追加する構想
   - LPcode/DetectCodeGPTの知見を活用

2. **低リソース言語のLLMコード生成** (`ideas/low-resource-programming-languages.md`)
   - MultiPL-Eベンチマークの拡張
   - マイナー言語でのLLM性能改善手法
