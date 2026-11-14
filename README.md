# skills

Claude Code や Command Code などで使うエージェントスキル集。

## インストール

```bash
pnpm dlx skills add shabaraba/skills
pnpm dlx skills add shabaraba/skills --skill <スキル名>
```

## 収録スキル

| カテゴリ | スキル | 内容 | 出典 |
| --- | --- | --- | --- |
| dev | feature-dev | コードベース理解から設計、実装、レビューまでの機能開発ワークフロー | claude-plugins-official の feature-dev を改変 |
| dev | narrative-commits | 変更を発生理由ごとに分割し、意図を追える順序でコミットする | vibing.nvim プラグイン narrative-commits |
| review | code-review | PR のレビュー。`--comment` で GitHub に投稿 | claude-plugins-official の code-review を転記 |
| refactor | code-simplifier | 直近の変更コードを、動作を変えずに明快で一貫した形へ整える | claude-plugins-official の code-simplifier を改変 |

## 出典とライセンス

feature-dev と code-review は [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) のプラグインを元にしており、Apache License 2.0 に従います。変更点は次のとおりです。

- feature-dev: プラグインのコマンドとエージェント定義を、1つのスキルと `references/` に再構成した
- code-review: スキルの frontmatter を付けた以外は、コマンド本文と同じ
- code-simplifier: エージェント定義の frontmatter をスキル用に書き換えた以外は、本文と同じ

## 構成

```
skills/
├── dev/
│   ├── feature-dev/
│   │   ├── SKILL.md
│   │   └── references/
│   └── narrative-commits/
│       └── SKILL.md
├── review/
│   └── code-review/
│       └── SKILL.md
└── refactor/
    └── code-simplifier/
        └── SKILL.md
```

カテゴリはリポジトリ内の整理用です。`skills` CLI は `skills/` の下を3階層まで探索するため、カテゴリを挟んでもそのまま検出されます。インストール先は `.agents/skills/<スキル名>/` にフラットに展開され、`--skill` の指定もカテゴリではなくスキル名で行います。

新しいスキルは該当カテゴリの下に `<スキル名>/SKILL.md` として追加します。カテゴリを増やす場合も深さは3階層までにしてください。
