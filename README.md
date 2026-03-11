# kiro-websearch-policy

Kiro の Web 検索・Fetch 機能に対して、信頼性・品質・セキュリティのポリシーを適用する Agent Skill + Hook のセットです。

## 特徴

- **ホワイトリストベースの情報源管理** — 信頼できるドメイン（AWS公式、Google Cloud公式、Anthropic公式など）を優先し、個人ブログやSEO記事を排除
- **採用判定アルゴリズム** — 検索結果を「✅ 採用可」「⚠️ 条件付き採用可」「❌ 不採用」に自動分類
- **プロンプトインジェクション防御** — 外部コンテンツ内の悪意ある指示（コマンド実行誘導、システムプロンプト上書き等）を検出・無視
- **出典の明記を強制** — すべての情報にインラインリンク形式での出典記載を義務付け
- **Hook によるリマインド** — Web 検索ツール使用前にポリシー遵守を自動チェック

## ディレクトリ構成

```
kiro-websearch-policy/
├── README.md
├── LICENSE
├── web-search-policy/          # Agent Skill
│   └── SKILL.md
└── hooks/                      # Kiro Hooks
    └── web-search-policy-check.json
```

## インストール

### Skill

以下のいずれかのディレクトリに `web-search-policy/` フォルダをコピーしてください。

| スコープ | コピー先 |
|---|---|
| グローバル（全ワークスペース共通） | `~/.kiro/skills/` |
| ワークスペース固有 | `.kiro/skills/` |

### Hook

以下のディレクトリに `hooks/web-search-policy-check.json` をコピーしてください。

| コピー先 |
|---|
| `.kiro/hooks/` |

## Skill の概要

`web-search-policy/SKILL.md` は以下のルールを定義しています。

| カテゴリ | 内容 |
|---|---|
| 情報源の優先順位 | AWS公式MCP → ホワイトリストドメイン → 準信頼ドメイン → 一般検索（要報告） |
| ホワイトリスト | `aws.amazon.com`, `docs.aws.amazon.com`, `cloud.google.com`, `www.anthropic.com` 等 |
| 準信頼ドメイン | `techcrunch.com`, `www.infoq.com`, `openai.com`, `blog.google` |
| 出典・引用 | インラインリンク必須、30語以上の逐語引用禁止 |
| セキュリティ | HTTPS必須、プロンプトインジェクション防御、取得コンテンツの指示無視 |

## Hook の概要

`hooks/web-search-policy-check.json` は、Web 検索ツール（`web` タイプ）の使用前に自動トリガーされ、ポリシー遵守をリマインドします。

## カスタマイズ

- **ホワイトリストの編集** — `web-search-policy/SKILL.md` の「ルール > 1. 信頼できるドメインのホワイトリスト」セクションでドメインを追加・削除できます
- **Hook のプロンプト変更** — `hooks/web-search-policy-check.json` の `then.prompt` を編集してチェック内容をカスタマイズできます

## ライセンス

MIT License
