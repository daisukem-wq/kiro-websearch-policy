# kiro-websearch-policy

KiroのWeb検索機能で信頼できる情報源を優先するためのSkill。

## 概要

Web検索時にホワイトリストドメインを優先し、情報の信頼性を確保します。

## インストール

```bash
# グローバルインストール（全ワークスペースで使用）
cp -r web-search-policy ~/.kiro/skills/

# ワークスペース固有
cp -r web-search-policy .kiro/skills/
```

## カスタマイズ

`web-search-policy/SKILL.md`の「ルール」セクションでホワイトリストを編集できます。

## ライセンス

MIT License