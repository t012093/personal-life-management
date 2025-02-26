# Clineを使用した生活習慣管理

Clineを使用してGitHub上で生活習慣を管理するための手順です。

## イシュー操作コマンド

### 1. Epicの作成

新しい習慣化プログラムを開始する際に使用します：

```
/issue create "[Routine] 朝活習慣化 30日チャレンジ" --template "Life Routine Epic"
```

### 2. デイリータスクの作成

毎日のルーティンタスクを作成します：

```
/issue create "[Daily] $(date '+%Y-%m-%d') Morning Routine" --template "Daily Routine Task" --assignee "@me"
```

### 3. タスクの進捗更新

タスクのステータスを更新します：

```
# タスクを開始
/issue move "Morning Routine" "In Progress"

# レビューへ移動
/issue move "Morning Routine" "Review"

# 完了にする
/issue move "Morning Routine" "Done"
```

### 4. ラベル操作

```
# ラベルの追加
/issue label add "Morning Routine" routine daily

# ラベルの削除
/issue label remove "Morning Routine" in_progress
```

### 5. コメントの追加

```
# 進捗メモを追加
/issue comment "Morning Routine" "今日の朝活達成！6時に起床して、ストレッチと読書を完了。"

# チェックリストの更新
/issue comment "Morning Routine" "- [x] 6:00 起床
- [x] ストレッチ
- [x] 朝食
- [ ] 運動"
```

## 便利なショートカット

### 1. イシューのクイック作成

```
# 翌日のタスクを事前作成
/issue create "[Daily] $(date -v+1d '+%Y-%m-%d') Morning Routine" --template "Daily Routine Task"
```

### 2. 進捗の確認

```
# 自分のオープンタスクを表示
/issue list --assignee "@me" --state open

# 特定のラベルのタスクを表示
/issue list --label routine --state open

# 完了したタスクを表示
/issue list --label routine --state closed
```

### 3. バッチ操作

```
# 特定のラベルの全タスクを移動
/issue list --label routine --state open | xargs -I {} /issue move {} "Review"
```

## テンプレートメッセージ

### 1. 朝の開始時

```
/issue comment "Morning Routine" "🌅 おはようございます！

### 今日の目標
- [ ] 6:00-6:15 起床・着替え
- [ ] 6:15-6:30 ストレッチ
- [ ] 6:30-7:00 読書
- [ ] 7:00-7:30 朝食

体調: 良好
気分: やる気あり"
```

### 2. 夜の振り返り

```
/issue comment "Morning Routine" "🌙 本日の振り返り

### 達成したこと
- 予定通り6時に起床
- モーニングルーティン完了

### 改善点
- 

### 明日への準備
- 就寝時間を22時に設定
- 運動着の準備"
```

## 活用のコツ

1. **コマンドの組み合わせ**
   - タスク作成と同時にラベルを付ける
   - 進捗更新時に自動でコメントを追加

2. **定期的な振り返り**
   - 週次でのパターン分析
   - 月次での習慣形成の確認

3. **自動化の活用**
   - GitHub Actionsとの連携
   - 定期的なリマインダーの設定

## トラブルシューティング

### よくあるエラーと対処法

1. **コマンドが実行されない**
   - Clineが正しく認証されているか確認
   - リポジトリのパーミッションを確認

2. **テンプレートが見つからない**
   - テンプレート名が正確か確認
   - リポジトリにテンプレートが存在するか確認

3. **ステータス更新が反映されない**
   - プロジェクトボードの設定を確認
   - カラム名が正確か確認

## 参考：定期的なメンテナンス

1. **週次レビュー**
   ```
   /issue create "[Review] 週次振り返り" --body "
   ### 今週の達成度
   - 
   ### パターンと気づき
   - 
   ### 来週の改善点
   - "
   ```

2. **月次サマリー**
   ```
   /issue create "[Summary] 月間レビュー" --body "
   ### 主な成果
   - 
   ### 習慣化の進捗
   - 
   ### 来月の目標
   - "
