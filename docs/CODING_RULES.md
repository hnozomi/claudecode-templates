# Next.js 14 + TypeScript — コーディングルール（最終版）

## 1. 技術スタック

| 分類                           | 採用技術                                        |
| :----------------------------- | :---------------------------------------------- |
| **Framework**                  | Next.js 14（App Router）                        |
| **Language**                   | TypeScript (`strict`)                           |
| **UI**                         | React Client Components + Tailwind CSS          |
| **Data Fetch**                 | React Query v5                                  |
| **HTTP Client**                | axios（共通インスタンス `lib/axios.ts`）        |
| **Pkg Manager**                | **pnpm**                                        |
| **Lint / Format / Type Check** | **Biome**（lint・format・typecheck すべて実行） |

---

## 2. Biome 運用

    pnpm biome check --apply       # フォーマット + Lint
    pnpm biome check --typecheck   # 型チェック

CI では **型エラー / Lint エラーが 1 件でもあれば失敗** とする。

---

## 3. コーディング規約

| 項目                   | ルール                                                                          |
| :--------------------- | :------------------------------------------------------------------------------ |
| **ファイル構成**       | **1 ファイル = 1 コンポーネント**                                               |
| **コンポーネント記法** | Arrow Function + `FC<Props>`                                                    |
| **インポート**         | バレルファイル経由必須 ─ `@/components/ui`, `@/features/*`, `@/lib` など        |
| **テスト / Story**     | `*.test.tsx` / `*.stories.tsx` は実装ファイル **と同じディレクトリ**            |
| **命名規則**           | `camelCase`（変数・関数） / `PascalCase`（型・FC） / `UPPER_SNAKE_CASE`（定数） |
| **非同期関数**         | `getXxx` / `fetchXxx` プレフィックス、戻り値に `Promise<型>` 明示               |
| **例外処理**           | `axios.isAxiosError` で判定し、ドメイン層エラーへ変換して上位へ伝搬             |

---

## 4. React & TypeScript ベストプラクティス

### 4.1 Hooks

- **トップレベル呼び出し** を厳守
- `useEffect` を書く前に **Server Components / Server Actions** で代替可否を検討

### 4.2 再レンダリング最適化

- `memo` / `useMemo` / `useCallback` は **実測して必要と判断後に導入**
- Context には **高頻度更新 state** を渡さない

### 4.3 エラーハンドリング

- `/app/error.tsx` で全体を **Error Boundary** で包む
- 機能単位の Boundary は必要に応じて追加

### 4.4 Code Splitting

- `React.lazy` または `next/dynamic` で遅延読み込み
- **LCP を悪化させない範囲** に限定

### 4.5 データ取得戦略

- **RSC でプリフェッチ → React Query でハイドレート & 更新** が基本
- キャッシュキーは `['user', id]` など **配列形式** で統一

### 4.6 型安全

- 型引数の省略禁止（`string[]` を使用）
- `switch` 文は **exhaustive チェック** → `never` 到達でコンパイルエラー

### 4.7 定数管理

- `as const` でリテラル型化し、Union 型を自動生成

### 4.8 演算子の安全性

- optional-chaining と nullish-coalescing（`??`）を適切に使用
  - 暗黙の `||` による falsy 判定は避ける

### 4.9 ユーティリティ

- 共通ロジックは **`/lib`** に切り出し、複数 Hook から再利用
- 命名は **動詞＋目的語**（例 `toCamelCase`, `isEmpty`）

### 4.10 テスト方針

- **ピュア関数 & Hooks** を単体テスト必須（Vitest）
- UI テストは `@testing-library/react` で **Role / Text 検索** を推奨

---

## 5. `package.json` スクリプト例

```jsonc
{
  "scripts": {
    "dev": "pnpm next dev",
    "build": "pnpm next build",
    "start": "pnpm next start",
    "lint": "pnpm biome check --apply",
    "typecheck": "pnpm biome check --typecheck",
    "test": "pnpm vitest run"
  }
}
```

---

## 6. インポート規約

### バレルエクスポート必須

- UI コンポーネント: `import { Card, Button } from "@/components/ui"`
- 機能モジュール: `import { KpiPills } from "@/features/dashboard"`
- ライブラリ: `import { cn, type Run } from "@/lib"`

### 禁止事項

- 個別ファイルパス: `@/components/ui/card` ❌
- 複数行インポート: 関連モジュールは 1 行にまとめる
