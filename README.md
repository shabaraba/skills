# skills

Claude Code や Command Code などで使うエージェントスキル集。

## インストール

```bash
pnpm dlx skills add shabaraba/skills
pnpm dlx skills add shabaraba/skills --skill <スキル名>
```

## 収録スキル

| スキル | 内容 | 出典 |
| --- | --- | --- |
| feature-dev | コードベース理解から設計、実装、レビューまでの機能開発ワークフロー | claude-plugins-official の feature-dev を改変 |
| code-review | PR のレビュー。`--comment` で GitHub に投稿 | claude-plugins-official の code-review を転記 |
| simplify | 変更差分の再利用・単純化・効率の改善 | 独自に作成 |

## 出典とライセンス

feature-dev と code-review は [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) のプラグインを元にしており、Apache License 2.0 に従います。変更点は次のとおりです。

- feature-dev: プラグインのコマンドとエージェント定義を、1つのスキルと `references/` に再構成した
- code-review: スキルの frontmatter を付けた以外は、コマンド本文と同じ

simplify は Claude Code 組み込みコマンドの説明文を元に、独自に書いたものです。組み込み版とは内容が異なります。

## 構成

```
skills/
└── <スキル名>/
    └── SKILL.md
```
