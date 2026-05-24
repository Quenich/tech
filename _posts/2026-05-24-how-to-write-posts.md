---
title: "ブログ記事の書き方・公開手順【GitHub Pages + Jekyll】"
date: 2026-05-24 01:00:00 +0000
categories: [ブログ, チュートリアル]
tags: [GitHub Pages, Jekyll, Markdown, 記事作成]
---

ブログの環境構築が完了したら、あとは記事を書いてプッシュするだけです。日常的な運用手順をまとめます。

## ファイルの作成場所

記事はすべて `_posts/` フォルダに作成します。

| ブログ | フォルダのパス |
|--------|---------------|
| 個人ブログ | `C:/Users/<ユーザー名>/<ユーザー名>.github.io/_posts/` |
| 技術ブログ | `C:/Users/<ユーザー名>/tech/_posts/` |

---

## ファイル名のルール

```
YYYY-MM-DD-タイトル.md
```

**例：**
```
2026-05-24-my-first-post.md
2026-06-01-jekyll-tips.md
```

- 日付は `年-月-日` の形式
- タイトル部分はハイフン区切り、スペース不可
- 拡張子は `.md`

---

## 記事の冒頭（Front Matter）

ファイルの先頭に必ず以下を書きます：

```markdown
---
title: "記事のタイトル"
date: YYYY-MM-DD 00:00:00 +0000
categories: [カテゴリ]
tags: [タグ1, タグ2]
---
```

| 項目 | 説明 |
|------|------|
| `title` | 記事のタイトル |
| `date` | 公開日時（UTC で指定） |
| `categories` | カテゴリ（1〜2個推奨） |
| `tags` | タグ（複数可） |

> **日付の注意**: `date` は UTC（世界標準時）で指定します。日本時間（JST）は UTC+9 なので、日本時間の深夜0時に公開したい場合は `前日 15:00:00 +0000` と書くか、`00:00:00 +0000` にします。

---

## 本文の書き方（Markdown）

```markdown
## 見出し2

### 見出し3

通常のテキストはそのまま書きます。

**太字** と *斜体* と `インラインコード`

- リスト項目1
- リスト項目2

1. 番号リスト1
2. 番号リスト2

> 引用文はこのように書きます

---（水平線）
```

**コードブロック：**

````markdown
```bash
echo "コードブロックはバッククォート3つで囲む"
```
````

**リンクと画像：**

```markdown
[リンクテキスト](https://example.com)

![画像の説明](/assets/img/sample.png)
```

---

## 公開手順

### 個人ブログに投稿する場合

```bash
cd C:/Users/<ユーザー名>/<ユーザー名>.github.io
git add .
git commit -m "記事追加: 記事タイトル"
git push
```

### 技術ブログに投稿する場合

```bash
cd C:/Users/<ユーザー名>/tech
git add .
git commit -m "記事追加: 記事タイトル"
git push
```

プッシュ後、数分で自動的にビルド＆公開されます。

---

## 公開確認

GitHub Actions のビルド状況：

- 個人ブログ: `https://github.com/<ユーザー名>/<ユーザー名>.github.io/actions`
- 技術ブログ: `https://github.com/<ユーザー名>/tech/actions`

緑のチェックマークが付いたら公開完了です。

---

## 下書き（非公開）として保存する

公開前に下書きとして保存したい場合は `_drafts/` フォルダに置きます。

```
_drafts/my-draft-post.md
```

`_drafts/` 内のファイルは本番環境では公開されません。ローカルで確認するには：

```bash
bundle exec jekyll serve --drafts --future
```

---

## ローカルでプレビューする

公開前にローカルで確認する場合：

```bash
# 個人ブログ
cd C:/Users/<ユーザー名>/<ユーザー名>.github.io
bundle exec jekyll serve --future

# 技術ブログ
cd C:/Users/<ユーザー名>/tech
bundle exec jekyll serve --future
```

ブラウザで `http://localhost:4000` を開いて確認します。
