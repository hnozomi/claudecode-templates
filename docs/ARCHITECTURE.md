# Next.js プロジェクト アーキテクチャ

このドキュメントは、**Next.js 14+ / TypeScript / Tailwind CSS** を用いた個人開発テンプレートのフォルダ構成を定義します。claudecode で新規リポジトリを生成する際の参照用ドキュメントです。

---

## 1. フォルダ構成

```text
project-name/
├── src/
│   ├── app/                      # App Router（ページ & ルートハンドラ）
│   │   ├── (public)/            # 認証不要ページ
│   │   ├── (authenticated)/     # 認証必須ページ
│   │   ├── api/                 # Route Handlers
│   │   ├── layout.tsx           # ルートレイアウト
│   │   └── page.tsx             # ホームページ
│   │
│   ├── features/                # 機能ごとにカプセル化
│   │   └── auth/                # 例）認証機能
│   │       ├── components/
│   │       ├── hooks/
│   │       ├── api/
│   │       ├── services/
│   │       ├── types/
│   │       └── index.ts         # バレル（外部公開）
│   │
│   ├── shared/                  # 共有 UI / フック / Utils
│   │   ├── components/ui/
│   │   ├── hooks/
│   │   └── utils/
│   │
│   ├── lib/                     # 外部ライブラリ初期化・ラッパ
│   │                            # 例: axios.ts など（ライブラリごとにファイルを配置）
│   │
│   ├── types/                   # グローバル型定義
│   ├── constants/               # 定数・設定値
│   └── styles/                  # グローバル CSS
│
├── public/                      # 静的アセット
├── docs/                        # 設計書・テンプレート置き場（本ドキュメントを含む）
└── README.md                    # プロジェクト概要（任意）
```

> **注**: `infrastructure/`, `middleware.ts`, `prisma/`, `e2e/` などの層はテンプレート外とし、必要に応じて導入してください。

---

## 2. hooks と services の責務分離

| 区分         | 役割                                                                           | 依存                    | 呼び出し方向               |
| ------------ | ------------------------------------------------------------------------------ | ----------------------- | -------------------------- |
| **hooks**    | React ライフサイクル & 副作用を扱う。データ取得やイベントリスナーもここ。      | React, React Query など | hooks → services           |
| **services** | 純粋ビジネスロジック／I/O ラッパ（API 呼び出し・計算処理）。副作用を含めない。 | なし（Pure TS 推奨）    | （hooks からのみ呼び出し） |

> **ルール**: `services` から `hooks` を呼び出すことは **禁止** です。

---

## 3. パスエイリアス設定（tsconfig.json）

```jsonc
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@components/*": ["./src/shared/components/*"],
      "@hooks/*": ["./src/shared/hooks/*"],
      "@utils/*": ["./src/shared/utils/*"],
      "@lib/*": ["./src/lib/*"],
      "@/features/*": ["./src/features/*"]
    }
  }
}
```

---

## 4. `/src/lib` ディレクトリの指針

外部ライブラリを導入する際は、**初期化コードまたはラッパーモジュール**を作成し、`/src/lib` に配置します。

- **命名規則**: `<libraryName>.ts`（例: `axios.ts`）
- **責務**: インスタンス生成や共通設定を一元管理し、アプリ各所で直接ライブラリを import しないようにします。

---

## 5. shared / features / app の依存方針

```
shared  →  features  →  app
```

- `shared` は他層に依存しません。
- `features` は複数 `shared` モジュールを利用可。
- `app` 層は UI 構成のみに集中します。

---

## 6. 命名規則（抜粋）

| 種類              | 規則           | 例                             |
| ----------------- | -------------- | ------------------------------ |
| フォルダ          | kebab-case     | `user-profile/`                |
| UI コンポーネント | PascalCase     | `LoginForm.tsx`                |
| Hook / Service    | lowerCamelCase | `useAuth.ts`, `authService.ts` |
| 定数 / 型         | lowerCamelCase | `config.ts`, `global.d.ts`     |

---
