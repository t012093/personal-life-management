# 生活習慣管理システム セットアップガイド

## 概要

このプロジェクトは、GitHub ProjectsとIssuesを活用して生活習慣の改善と日々のルーティンを管理するためのシステムです。
ClineとGitHub Actionsの連携により、タスクの進捗管理や日報の自動生成を実現します。

## セットアップ手順

1. **リポジトリの準備**
   ```bash
   # リポジトリをクローン
   git clone <your-repo-url>
   cd personal-life-management
   ```

2. **GitHub Projectsのセットアップ**
   - 新しいプロジェクトを作成（Project name: Life Routine Management）
   - 以下のカラムを追加:
     - 📋 Backlog
     - 🏃 In Progress
     - 👀 Review
     - ✅ Done

3. **ラベルの設定**
   以下のラベルを作成:
   - `epic`: 大きな目標や習慣化プログラム用
   - `routine`: 日々のルーティンタスク用
   - `daily`: 毎日のタスク用
   - `in_progress`: 進行中のタスク用

4. **GitHub Actionsの有効化**
   - リポジトリの Settings > Actions > General で Actions permissions を有効化
   - 必要に応じて Workflow permissions で "Read and write permissions" を選択

5. **最初のEpicの作成**
   1. Issues > New Issue > "Life Routine Epic" テンプレートを選択
   2. 必要事項を入力:
      - タイトル（例: "[Routine] 朝活習慣化 30日チャレンジ"）
      - 開始日
      - 期間
      - 目標とする習慣
      - 成功指標

6. **日々のルーティンタスクの作成**
   1. Issues > New Issue > "Daily Routine Task" テンプレートを選択
   2. 必要事項を入力:
      - タイトル（例: "[Daily] 2024-02-27 朝活ルーティン"）
      - タスクリスト
      - スケジュール
      - メモ

## 使用方法

### 1. タスクの進捗管理

- プロジェクトボードでカードを移動すると自動的にステータスが更新されます
- ステータス変更時に自動コメントが追加され、進捗が記録されます

### 2. 日報の確認

- 毎朝7時に自動生成される日報でこれまでの進捗を確認できます
- Epicイシューにコメントとして追加されます

### 3. 振り返りの記録

1. 夜の振り返り時にタスクを "Review" に移動
2. 自動生成される振り返りテンプレートに記入
3. 完了後 "Done" に移動

## Clineとの連携

1. VSCodeでCline拡張機能を開く
2. 以下のコマンドでイシューを作成:
   ```
   /issue create "朝活ルーティン Day 1" --template "Daily Routine Task"
   ```

3. イシューの進捗更新:
   ```
   /issue move "朝活ルーティン Day 1" "In Progress"
   ```

## トラブルシューティング

### よくある問題

1. **Actionsが実行されない**
   - リポジトリの Settings でワークフローの権限を確認
   - `GITHUB_TOKEN` のパーミッションを確認

2. **自動コメントが追加されない**
   - イシューのラベルが正しく設定されているか確認
   - プロジェクトボードのカラム名が正しいか確認

3. **日報が生成されない**
   - Epicイシューに適切なラベル（epic, routine）が付いているか確認
   - タイムゾーンの設定を確認

### サポート

問題が解決しない場合は、イシューを作成してサポートを依頼してください。
