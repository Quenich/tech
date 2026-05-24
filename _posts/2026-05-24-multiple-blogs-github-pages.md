---
title: "GitHub Pages で複数のブログを無料で運用する方法"
date: 2026-05-24 00:00:00 +0000
categories: [ブログ, チュートリアル]
tags: [GitHub Pages, Jekyll, 複数ブログ, 運用]
---

GitHub Pages では1つのアカウントで複数のブログを運用できます。「個人ブログ」と「技術ブログ」を分けて管理したい場合などに便利です。

## GitHub Pages の仕組み

GitHub Pages には2種類のサイトがあります。

| 種類 | リポジトリ名 | URL |
|------|-------------|-----|
| ユーザーページ | `<ユーザー名>.github.io` | `https://<ユーザー名>.github.io` |
| プロジェクトページ | 任意の名前（例: `tech`） | `https://<ユーザー名>.github.io/tech` |

- **ユーザーページ**は1アカウントに1つだけ作成できます
- **プロジェクトページ**は無制限に作成できます

---

## 構成例

| ブログ | リポジトリ名 | URL |
|--------|-------------|-----|
| 個人ブログ | `<ユーザー名>.github.io` | `https://<ユーザー名>.github.io` |
| 技術ブログ | `tech` | `https://<ユーザー名>.github.io/tech` |
| 旅行ブログ | `travel` | `https://<ユーザー名>.github.io/travel` |

---

## セットアップ手順

### Step 1: Chirpy テンプレートから新しいリポジトリを作成

1. [https://github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter) を開く
2. **"Use this template"** → **"Create a new repository"** をクリック
3. リポジトリ名を任意の名前（例: `tech`）にする
4. **Public** を選択して **"Create repository"** をクリック

---

### Step 2: ローカルにクローン

**重要**: 既存のブログフォルダの外にクローンしてください。

```bash
# ホームディレクトリに移動してからクローン
cd C:/Users/<ユーザー名>
git clone https://github.com/<ユーザー名>/tech.git
cd tech
bundle install
```

> **注意**: 既存のブログフォルダの中にクローンすると、リポジトリが入れ子になってしまいます。必ずホームディレクトリ（`C:/Users/<ユーザー名>/`）直下にクローンしてください。

---

### Step 3: `_config.yml` を編集

プロジェクトページ用の設定として `url` と `baseurl` を正しく設定することが重要です。

```yaml
lang: ja
timezone: Asia/Tokyo

title: "技術ブログ"
tagline: "サブタイトル"
description: >-
  ブログの説明文

url: "https://<ユーザー名>.github.io"   # ユーザーページのURL
baseurl: "/tech"                        # リポジトリ名を指定

github:
  username: <ユーザー名>

social:
  name: "あなたの名前"
  email: your@email.com
  links:
    - https://github.com/<ユーザー名>
```

> **ポイント**: `url` はユーザーページのルート URL、`baseurl` はリポジトリ名（`/tech` など）を指定します。

---

### Step 4: GitHub Pages の公開設定

1. `https://github.com/<ユーザー名>/tech/settings/pages` を開く
2. **Source** を **"GitHub Actions"** に変更して Save

---

### Step 5: プッシュして公開

```bash
cd C:/Users/<ユーザー名>/tech
git add .
git commit -m "技術ブログ初期設定"
git push
```

数分後に `https://<ユーザー名>.github.io/tech` で公開されます。

---

## フォルダ構成

複数のブログを管理する場合、以下のようにフォルダを整理しておくと分かりやすいです：

```
C:/Users/<ユーザー名>/
├── <ユーザー名>.github.io/    ← 個人ブログ
│   └── _posts/
├── tech/                      ← 技術ブログ
│   └── _posts/
└── travel/                    ← 旅行ブログ（例）
    └── _posts/
```

各フォルダは独立した Git リポジトリです。それぞれ別々に `git push` して管理します。

---

## 記事を追加する

各ブログの `_posts/` フォルダに記事を追加してプッシュするだけです。

```bash
# 個人ブログに投稿
cd C:/Users/<ユーザー名>/<ユーザー名>.github.io
git add . && git commit -m "記事追加" && git push

# 技術ブログに投稿
cd C:/Users/<ユーザー名>/tech
git add . && git commit -m "記事追加" && git push
```

---

## よくある注意点

### リポジトリを入れ子にしない

既存のブログフォルダの中に別のブログをクローンすると、Git の管理が複雑になります。必ず別々のフォルダに分けてください。

### `baseurl` の設定を忘れずに

プロジェクトページでは `baseurl` を設定しないと、CSS や画像が正しく読み込まれません。

```yaml
url: "https://<ユーザー名>.github.io"
baseurl: "/<リポジトリ名>"
```

### ローカルプレビュー時のURL

`baseurl` を設定している場合、ローカルプレビューのURLが変わります：

```
http://localhost:4000/<リポジトリ名>/
```
