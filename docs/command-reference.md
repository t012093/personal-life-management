# GitHub CLI コマンドリファレンス

このドキュメントでは、タスク管理システムで使用する主なGitHub CLIコマンドの詳細な説明と使用例を提供します。

## 基本コマンド

### リポジトリ関連

1. リポジトリの作成
```bash
gh repo create <name> --private --description "<description>" --clone
```
- `<name>`: リポジトリ名
- `--private`: プライベートリポジトリとして作成
- `--description`: リポジトリの説明
- `--clone`: 作成後にローカルにクローン

例：
```bash
gh repo create personal-tasks --private --description "Personal task management system" --clone
```

### プロジェクト関連

1. プロジェクトの作成
```bash
gh project create --title "<title>" --owner "@me"
```
- `<title>`: プロジェクト名
- `--owner "@me"`: 自分をオーナーとして設定

例：
```bash
gh project create --title "Life Management" --owner "@me"
```

2. プロジェクトへのアイテム追加
```bash
gh project item-add <project-number> --owner "@me" --url "<issue-url>"
```
- `<project-number>`: プロジェクト番号
- `--url`: イシューのURL

例：
```bash
gh project item-add 1 --owner "@me" --url "https://github.com/user/repo/issues/1"
```

### イシュー関連

1. イシューの作成
```bash
gh issue create --title "<title>" --body "<body>" --label "<label1>,<label2>"
```
- `<title>`: イシューのタイトル
- `--body`: イシューの本文
- `--label`: カンマ区切りのラベル

例：
```bash
gh issue create --title "Morning Routine" --body "## Tasks\n- [ ] Wake up\n- [ ] Exercise" --label "routine,habits"
```

2. ラベルの作成
```bash
gh label create <name> --color "<color>" --description "<description>"
```
- `<name>`: ラベル名
- `--color`: 色コード（16進数）
- `--description`: ラベルの説明

例：
```bash
gh label create routine --color "#0366d6" --description "Regular scheduled activities"
```

## 高度な使用方法

### イシューの一括管理

1. 複数イシューの作成（スクリプト例）
```bash
#!/bin/bash
REPO="personal-tasks"

# 朝のルーティン
gh issue create --repo $REPO \
  --title "🌅 Morning Routine" \
  --body "## Daily Tasks\n- [ ] Wake up at 6:00\n- [ ] Exercise" \
  --label "routine,daily"

# 週間レビュー
gh issue create --repo $REPO \
  --title "📊 Weekly Review" \
  --body "## Review Points\n- [ ] Task completion\n- [ ] Goals progress" \
  --label "review,weekly"
```

### プロジェクトのカスタマイズ

1. プロジェクトビューの作成
```bash
gh api graphql -f query='
mutation {
  createProjectV2Field(
    input: {
      projectId: "PROJECT_ID"
      dataType: SINGLE_SELECT
      name: "Status"
      options: ["Todo", "In Progress", "Done"]
    }
  ) {
    projectV2Field {
      id
    }
  }
}'
```

### 自動化スクリプト

1. 定期的なイシュー作成（GitHub Actions用）
```yaml
name: Create Daily Tasks
on:
  schedule:
    - cron: '0 0 * * *'  # 毎日00:00に実行

jobs:
  create-daily-tasks:
    runs-on: ubuntu-latest
    steps:
      - name: Create Daily Tasks
        run: |
          gh issue create \
            --title "$(date +"%Y-%m-%d") Daily Tasks" \
            --body "## Today's Tasks\n- [ ] Morning routine\n- [ ] Review goals" \
            --label "daily,routine"
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Tips & トラブルシューティング

### よくある問題

1. 認証エラー
```bash
# トークンの再認証
gh auth login
```

2. コマンド実行エラー
```bash
# バージョン確認
gh --version

# アップデート（Homebrew使用の場合）
brew upgrade gh
```

### 便利なエイリアス設定

```bash
# .gitconfig に追加
[alias]
  ic = "!gh issue create"
  il = "!gh issue list"
  pl = "!gh project list"
```

## 参考情報

- [GitHub CLI 公式ドキュメント](https://cli.github.com/manual/)
- [GitHub Projects API](https://docs.github.com/en/rest/reference/projects)
- [GitHub Issues API](https://docs.github.com/en/rest/reference/issues)
