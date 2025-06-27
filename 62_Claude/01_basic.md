# Claudeについての基本的なこと

### 強調レベルについて
```bash
# NEVER（絶対禁止）
NEVER: パスワードやAPIキーをハードコーディングしない
NEVER: ユーザーの確認なしにデータを削除しない
NEVER: テストなしで本番環境にデプロイしない

# YOU MUST（必須事項）
YOU MUST: すべての公開APIにドキュメントを記載
YOU MUST: エラーハンドリングを実装
YOU MUST: 変更前に既存テストが通ることを確認

# IMPORTANT（重要事項）
IMPORTANT: パフォーマンスへの影響を考慮
IMPORTANT: 後方互換性を維持
IMPORTANT: セキュリティベストプラクティスに従う
```

### コンテキストの最適化
```bash
# コンテキストを一旦クリア
/clear

# 再読込
@CLAUDE.mdを読んでプロジェクトのコンテキストを復元して
```

