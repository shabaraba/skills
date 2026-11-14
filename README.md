# skills

Claude Code や Command Code などで使うエージェントスキル集。

## インストール

[pnpm](https://pnpm.io/) が必要です。`skills` CLI はインストールせず `pnpm dlx` で実行できます。

```bash
# 収録スキルの一覧を確認する
pnpm dlx skills add shabaraba/skills --list

# すべてのスキルを入れる
pnpm dlx skills add shabaraba/skills --all

# スキルを指定して入れる
pnpm dlx skills add shabaraba/skills --skill narrative-commits

# 複数指定する（--skill を繰り返す）
pnpm dlx skills add shabaraba/skills --skill feature-dev --skill code-review
```

`--all` は `--skill '*' --agent '*' -y` と同じ意味です。プロジェクト単位ではなくユーザー全体に入れたい場合は `-g` を付けます。

```bash
pnpm dlx skills add shabaraba/skills --all -g
```

インストール後の操作は次のとおりです。

```bash
# インストール済みスキルを一覧する
pnpm dlx skills list

# 最新版に更新する
pnpm dlx skills update

# スキルを削除する
pnpm dlx skills remove
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
