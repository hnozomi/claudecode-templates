# CLAUDE.md

> **Claude はこのファイルを毎プロンプト読むため、_必須ガイドラインのみ_ を記述します。**
> 詳細な規約やディレクトリ構造は `docs/` 配下の各ドキュメントを参照してください。

---

## スタック & 参照ドキュメント

- **Stack**: Next.js 14 / React 18 / TypeScript 5 · FastAPI 0.111 / Python 3.12
- **Docs**:

  - ディレクトリ構造 → `docs/directory-structure.md`
  - コーディング規則 → `docs/coding-rules.md`

## プロンプトベストプラクティス（Anthropic ガイド要約）

### 1 | 明確で直接的 (Be Clear & Direct)

- 出力フォーマット・制約を _冒頭_ で指定。
- あいまいな代名詞を避け、引用や再掲で文脈を明示。

### 2 | Step‑by‑Step 思考 (Chain of Thought)

- `まず手順を考えてから最終回答のみ返す` など、思考過程を内部で促す。
- **内部思考は出力しない**。

### 3 | 幻覚削減 (Reduce Hallucinations)

- 不確実な情報は **「不明」「要確認」** と回答。
- 事実主張には出典 ID を添付し、セルフチェックで裏付けを確認。

## 開発ワークフロー

- **Iterative**: _Plan → Code → Review → Commit_ の短サイクル。
- **不明点は質問**: 推測で進まない。

## Git

- `feat/*` ブランチで小さな差分を **commit**。
- 変更が安定したら **push** し、PR を作成。
  _ローカルで `pnpm lint` と `pnpm typecheck` を通してから push すること。_
- CI やデプロイ手順は別タスクで管理し、本ファイルでは扱わない。

## AI ガードレール

- 機密・個人情報をプロンプトに含めない。
- ESLint + Prettier 準拠、TypeScript `strict`、`any` 禁止。
- 出力は **日本語**。コードコメントは日英混在可。

---
