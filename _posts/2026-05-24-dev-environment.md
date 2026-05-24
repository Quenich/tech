---
title: "ブログ運用に使っている開発環境まとめ【Windows 11】"
date: 2026-05-24 02:00:00 +0000
categories: [環境構築]
tags: [Windows, VS Code, Claude Code, Git, GitHub, Jekyll, Ruby]
---

このブログの構築・運用に使っている環境をまとめます。

## OS・シェル

| 項目 | 内容 |
|------|------|
| OS | Windows 11 Home |
| シェル | Git Bash（MINGW64） |

Git をインストールすると Git Bash が付属します。PowerShell よりも Linux コマンドに近い操作ができるため、Jekyll の操作に向いています。

---

## インストール済みツール

| ツール | バージョン | 用途 |
|--------|-----------|------|
| Git | 2.54.0 | バージョン管理・GitHub へのプッシュ |
| Ruby | 3.3.11 | Jekyll の実行環境 |
| Jekyll | 4.4.1 | 静的サイトジェネレーター |
| Node.js | 24.16.0 | Chirpy テーマのビルドツール |
| VS Code | 1.121.0 | コードエディター・記事執筆 |

---

## エディター：VS Code

[https://code.visualstudio.com/](https://code.visualstudio.com/)

記事の執筆とファイル編集に使用しています。Markdown のプレビュー機能が内蔵されており、記事を書きながらリアルタイムで見た目を確認できます。

**便利な使い方：**

```bash
# ターミナルからフォルダごと開く
code C:/Users/<ユーザー名>/tech
```

---

## AI アシスタント：Claude Code

[https://claude.ai/code](https://claude.ai/code)

Anthropic が提供する AI コーディングアシスタントです。ターミナル上で動作し、コードの生成・編集・説明を自然言語で指示できます。

このブログの構築作業もほぼ Claude Code との対話で進めました。

**主な用途：**
- 記事の Markdown 作成
- 設定ファイルの編集
- エラーの解決
- コマンドの調べ方

---

## バージョン管理：Git + GitHub

| ツール | 用途 |
|--------|------|
| Git | ローカルでのバージョン管理 |
| GitHub | リポジトリのホスティング・CI/CD |

ブログの記事・設定はすべて Git で管理しています。`git push` するだけで GitHub Actions が自動でビルド＆デプロイします。

**基本的な流れ：**

```bash
git add .
git commit -m "記事追加"
git push
```

---

## ホスティング：GitHub Pages

[https://pages.github.com/](https://pages.github.com/)

静的サイトの無料ホスティングサービスです。GitHub のリポジトリと連携しており、プッシュするだけで自動公開されます。

**特徴：**
- 完全無料（独自ドメインも使用可能）
- HTTPS 自動対応
- GitHub Actions による自動デプロイ

---

## ブログフレームワーク：Jekyll + Chirpy テーマ

| ツール | 用途 |
|--------|------|
| Jekyll | Markdown → HTML への変換 |
| Chirpy | ブログ向けテーマ（目次・検索・タグ機能付き） |

Chirpy テーマは技術ブログ向けに作られており、以下の機能が標準搭載されています：

- ダークモード / ライトモード切り替え
- 記事内目次（TOC）の自動生成
- カテゴリ・タグ管理
- 全文検索
- PWA 対応（オフラインでも閲覧可能）

---

## ローカルプレビューの起動

```bash
cd C:/Users/<ユーザー名>/tech
bundle exec jekyll serve --future
```

`http://localhost:4000/tech/` でプレビューできます。

---

## まとめ

すべて無料で使えるツールだけで構成しています。サーバー代ゼロ、管理画面なし、記事は Markdown で書いて `git push` するだけというシンプルな運用です。
