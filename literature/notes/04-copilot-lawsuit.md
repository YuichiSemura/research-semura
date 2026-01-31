# GitHub Copilot訴訟・社会的背景

## 概要

2022年にGitHub/Microsoft/OpenAIに対して提起された集団訴訟。オープンソースコードの著作権問題が焦点。

## 訴訟の経緯

### 提訴 (2022年11月)

- 開発者グループがGitHub、Microsoft、OpenAIを提訴
- 当初22の請求項目
- 主張: Copilotがオープンソースコードを帰属表示なしでコピー

### 判決 (2024年7月)

- **DMCA著作権侵害の請求は棄却**
- 理由: Copilot出力と訓練データの間に十分な類似性の証拠がない
- 裁判所: 「Copilotが記憶済みコードを出力するのは稀で、長いコード断片でプロンプトした場合に限る」

## GitHubの主張

- 150文字以上のコード複製は**全体の1%のみ**
- 大多数の提案は「今まで見たことのない」コード
- Duplicate Detection機能を提供（Blockに設定可能）

## 批判・懸念

### オープンソースコミュニティ

- オープンソースコードで訓練しながらライセンスに従わない
- 一部でコードが逐語的に再現される
- 150文字未満でも著作権侵害になりうる

### セキュリティ

- Copilot提案コードの**40%に脆弱性**（ある研究）
- 訓練データの質が出力の質に影響

## 研究への示唆

1. **法的境界の不明確さ**: 何をもって「クローン」「複製」とするか？
2. **検出の必要性**: ライセンス違反リスクの自動検出需要
3. **定量的研究の価値**: 「1%」の根拠を第三者が検証する意義
4. **実用ツールの需要**: 開発者がリスクを評価できるツール

## 参考リンク

- [GitHub Copilot Lawsuit Update](https://www.unite.ai/github-copilot-lawsuit-github-beats-the-case/)
- [Risk Assessment of GitHub Copilot](https://gist.github.com/0xabad1dea/be18e11beb2e12433d93475d72016902)
- [Plagiarism Today Analysis](https://www.plagiarismtoday.com/2021/07/08/github-copilot-and-the-copyright-around-ai/)
