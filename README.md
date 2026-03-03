# reading-memo-action

GitHub Issuesに書いた読書メモを、IssueがclosedになったタイミングでMarkdown要約ファイルに変換してくれるGitHub Actionsワークフローです。

「本」ラベルがついたIssueが閉じられると、GitHub Models (gpt-4o) を使って内容を整理・構造化し、`book-summary/123.md` のようなファイルとしてリポジトリにコミットします。最後にIssueへリンク付きコメントも自動投稿します。

## 主な特徴

- **トリガー**: 「本」ラベル付きのIssueが **closed** になったときのみ動作
- **AIモデル**: GitHub Models の `gpt-4o` を使用
- **出力形式**:
  ```markdown
  # 書籍タイトル
  > Source: https://github.com/ユーザー名/リポジトリ名/issues/123

  ## 概要（メモ全体から読み取れる書籍の主題を簡潔に）

  ## 読書メモ（章やテーマごとに整理。引用とページ番号を保持）

  ## まとめ（メモから読み取れる要点の箇条書き）


## 事前準備

Personal Access Tokenを準備。
Models: Read Only
Contains: Read and write
Issues: Read Only

Repository secretsにSUMMARIZE_PATを登録。

## カスタマイズしたい場合

- 使うモデルを変えたい → model: "gpt-4o" の部分を変更
- 出力フォルダを変えたい → book-summary を好きな名前に
- 温度を調整 → temperature: 0.0〜1.0の間で調整できます
- 別のラベルで動かしたい → if: の条件を変更
