# template

汎用プロジェクトテンプレート。

## このテンプレートから新しいリポジトリを作る手順

### 1. リポジトリ作成

GitHub の「Use this template」ボタン、または gh CLI でリポジトリを作成してクローンする。

```bash
gh repo create <your-repo> --template ht311/template --private --clone
cd <your-repo>
```

### 2. セットアップスクリプトを実行（初回のみ）

```bash
bash scripts/setup-repo.sh
```

以下を自動で設定する:

- **main ブランチ保護**（PR 必須・CI 必須・force push / 削除禁止）
- **自動マージ有効化**（squash のみ・マージ後ブランチ自動削除）
- **標準ラベル**（bug / enhancement / chore / documentation / question）

前提: `gh` CLI がインストール・認証済みであること。

### 3. CI のカスタマイズ

`.github/workflows/ci.yml` のプレースホルダーをプロジェクト固有の lint / test に置き換える。
ジョブ ID `ci` はルールセットの必須チェック名と対応しているため変更しないこと。

### 日常フロー

```bash
# 1. フィーチャーブランチを作る
git checkout -b feature/xxx

# 2. 作業してコミット・push
git commit -m "feat: ..."
git push -u origin HEAD

# 3. PR を作る
gh pr create --fill

# 4. CI が通れば自動マージされる（または手動で有効化）
gh pr merge --auto --squash
```

## ディレクトリ構成

```
.
├── .github/
│   ├── workflows/
│   │   ├── ci.yml                    # CI スケルトン（PR 必須チェック）
│   │   └── dependabot-auto-merge.yml # Dependabot の minor/patch を自動マージ
│   └── dependabot.yml                # Dependabot 設定
├── .devcontainer/                    # Dev Container 設定
├── docs/                             # ドキュメント・図
├── infrastructure/                   # Infrastructure as Code
├── scripts/
│   └── setup-repo.sh                 # リポジトリ初期設定スクリプト
└── CLAUDE.md                         # Claude Code 用の開発ガイドライン
```
