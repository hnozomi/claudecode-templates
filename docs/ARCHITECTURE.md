# Next.js プロジェクト アーキテクチャ

## 概要

このドキュメントは、Next.js 14+ (App Router) を使用したプロジェクトの標準的なフォルダ構成を定義します。

### 主な特徴
- **Framework**: Next.js 14+ (App Router)
- **言語**: TypeScript
- **スタイル**: Tailwind CSS
- **アーキテクチャ**: Feature-based（機能別モジュール構成）
- **レンダリング**: クライアントサイドレンダリング中心

## フォルダ構成
```
project-name/
├── src/
│   ├── app/                      # App Router（ルーティングのみ）
│   │   ├── (public)/             # 認証不要ページグループ
│   │   │   ├── login/
│   │   │   │   └── page.tsx     # /login ルート
│   │   │   ├── signup/
│   │   │   │   └── page.tsx     # /signup ルート
│   │   │   └── layout.tsx       # 公開ページ共通レイアウト
│   │   │
│   │   ├── (authenticated)/      # 認証必要ページグループ
│   │   │   ├── dashboard/
│   │   │   │   └── page.tsx     # /dashboard ルート
│   │   │   ├── users/
│   │   │   │   ├── page.tsx     # /users 一覧
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx # /users/[id] 詳細
│   │   │   ├── settings/
│   │   │   │   └── page.tsx     # /settings ルート
│   │   │   └── layout.tsx       # 認証ページ共通レイアウト
│   │   │
│   │   ├── api/                  # Route Handlers
│   │   │   ├── auth/
│   │   │   │   ├── login/
│   │   │   │   │   ├── route.ts # POST /api/auth/login
│   │   │   │   │   └── route.test.ts
│   │   │   │   └── logout/
│   │   │   │       └── route.ts # POST /api/auth/logout
│   │   │   └── users/
│   │   │       └── [id]/
│   │   │           ├── route.ts # GET/PUT/DELETE /api/users/[id]
│   │   │           └── route.test.ts
│   │   │
│   │   ├── layout.tsx            # ルートレイアウト
│   │   ├── page.tsx              # ホームページ (/)
│   │   ├── loading.tsx           # グローバルローディング
│   │   ├── error.tsx             # グローバルエラーハンドリング
│   │   ├── not-found.tsx         # 404ページ
│   │   └── providers.tsx         # クライアントプロバイダー
│   │
│   ├── features/                 # 機能別モジュール
│   │   ├── auth/                # 認証機能
│   │   │   ├── components/      # UI コンポーネント
│   │   │   │   ├── LoginPage.tsx
│   │   │   │   ├── LoginPage.test.tsx
│   │   │   │   ├── LoginForm.tsx
│   │   │   │   ├── LoginForm.test.tsx
│   │   │   │   ├── SignupForm.tsx
│   │   │   │   └── SignupForm.test.tsx
│   │   │   ├── hooks/           # カスタムフック
│   │   │   │   ├── useAuth.ts
│   │   │   │   ├── useAuth.test.ts
│   │   │   │   ├── useLogin.ts
│   │   │   │   ├── useLogin.test.ts
│   │   │   │   ├── useCurrentUser.ts
│   │   │   │   └── useCurrentUser.test.ts
│   │   │   ├── api/             # API 通信層
│   │   │   │   ├── authApi.ts
│   │   │   │   ├── authApi.test.ts
│   │   │   │   └── authKeys.ts # React Query キー
│   │   │   ├── services/        # ビジネスロジック
│   │   │   │   ├── authService.ts
│   │   │   │   └── authService.test.ts
│   │   │   ├── types/           # 型定義
│   │   │   │   └── index.ts
│   │   │   └── index.ts         # 公開 API（バレルファイル）
│   │   │
│   │   ├── user/                # ユーザー管理機能
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── api/
│   │   │   ├── services/
│   │   │   ├── types/
│   │   │   └── index.ts
│   │   │
│   │   └── dashboard/           # ダッシュボード機能
│   │       ├── components/
│   │       └── index.ts
│   │
│   ├── shared/                  # 共通モジュール
│   │   ├── components/
│   │   │   └── ui/             # 共通 UI コンポーネント
│   │   │       ├── button/
│   │   │       │   ├── Button.tsx
│   │   │       │   └── Button.test.tsx
│   │   │       ├── input/
│   │   │       │   ├── Input.tsx
│   │   │       │   └── Input.test.tsx
│   │   │       ├── card/
│   │   │       │   ├── Card.tsx
│   │   │       │   └── Card.test.tsx
│   │   │       ├── modal/
│   │   │       │   ├── Modal.tsx
│   │   │       │   └── Modal.test.tsx
│   │   │       └── layout/
│   │   │           ├── Layout.tsx
│   │   │           ├── Layout.test.tsx
│   │   │           ├── Header.tsx
│   │   │           ├── Header.test.tsx
│   │   │           ├── Footer.tsx
│   │   │           └── Footer.test.tsx
│   │   ├── hooks/              # 共通カスタムフック
│   │   │   ├── useDebounce.ts
│   │   │   ├── useDebounce.test.ts
│   │   │   ├── useLocalStorage.ts
│   │   │   ├── useLocalStorage.test.ts
│   │   │   ├── useMediaQuery.ts
│   │   │   └── useMediaQuery.test.ts
│   │   └── utils/              # ユーティリティ関数
│   │       ├── format.ts
│   │       ├── format.test.ts
│   │       ├── validation.ts
│   │       ├── validation.test.ts
│   │       ├── cn.ts
│   │       └── cn.test.ts
│   │
│   ├── infrastructure/          # インフラ層
│   │   └── database/
│   │       ├── prisma.ts       # Prisma クライアント
│   │       └── prisma.test.ts
│   │
│   ├── lib/                     # 外部ライブラリ設定
│   │   ├── axios.ts            # Axios 設定
│   │   ├── axios.test.ts
│   │   ├── queryClient.ts      # React Query 設定
│   │   └── queryClient.test.ts
│   │
│   ├── types/                   # グローバル型定義
│   │   ├── global.d.ts         # グローバル型
│   │   ├── env.d.ts            # 環境変数型
│   │   └── next.d.ts           # Next.js 拡張型
│   │
│   ├── constants/               # 定数管理
│   │   ├── config.ts           # アプリ設定
│   │   └── config.test.ts
│   │
│   ├── styles/                  # グローバルスタイル
│   │   ├── globals.css         # グローバル CSS
│   │   └── variables.css       # CSS 変数
│   │
│   └── middleware.ts            # Next.js ミドルウェア
│       └── middleware.test.ts
│
├── public/                      # 静的アセット
│   ├── images/
│   └── fonts/
│
├── prisma/                      # Prisma 設定
│   ├── schema.prisma           # スキーマ定義
│   └── migrations/             # マイグレーション
│
├── e2e/                         # E2E テスト
│   ├── auth/
│   │   ├── login.spec.ts
│   │   └── signup.spec.ts
│   ├── user/
│   │   └── user-crud.spec.ts
│   └── playwright.config.ts
│
└── [設定ファイル]               # プロジェクト設定
    ├── .env.example
    ├── .eslintrc.json
    ├── .prettierrc
    ├── jest.config.js
    ├── jest.setup.js
    ├── next.config.js
    ├── package.json
    ├── tailwind.config.js
    └── tsconfig.json
```

## ディレクトリ構成の詳細

### `/src/app`
Next.js App Router のルーティング層。ページコンポーネントは薄く保ち、実際の実装は features ディレクトリに委譲する。

- `(public)/` - 認証不要なページをグループ化
- `(authenticated)/` - 認証が必要なページをグループ化
- `api/` - Route Handlers（旧 API Routes）
- `providers.tsx` - クライアントサイドのプロバイダー設定

### `/src/features`
機能別にモジュール化されたビジネスロジックと UI 実装。各機能は独立して開発・テスト・削除が可能。

- `components/` - 機能固有の UI コンポーネント
- `hooks/` - 機能固有のカスタムフック
- `api/` - API 通信関数と React Query キー
- `services/` - ビジネスロジック（純粋関数）
- `types/` - 機能固有の型定義
- `index.ts` - 外部公開 API（唯一のバレルファイル）

### `/src/shared`
複数の機能で共有される汎用的なモジュール。ビジネスロジックは含まない。

- `components/ui/` - ボタン、フォーム要素などの基本 UI
- `hooks/` - 汎用的なカスタムフック
- `utils/` - フォーマット、バリデーションなどのユーティリティ

### `/src/infrastructure`
外部システムとの接続を管理するインフラストラクチャ層。

- `database/` - データベース接続（Prisma クライアント等）

### `/src/lib`
サードパーティライブラリの設定とラッパー。アプリケーション全体で使用する設定済みインスタンスを提供。

### `/src/types`
アプリケーション全体で使用されるグローバルな型定義。

### `/src/constants`
アプリケーション全体で使用される定数と設定値。

### `/e2e`
E2E テストファイル。機能単位でディレクトリを分割。

## 命名規則

| 種類 | 命名規則 | 例 |
|------|---------|-----|
| フォルダ名 | kebab-case | `user-profile/`, `auth-guard/` |
| UI コンポーネント | PascalCase | `LoginForm.tsx`, `UserTable.tsx` |
| ページコンポーネント | PascalCase | `LoginPage.tsx`, `DashboardPage.tsx` |
| フック | lowerCamelCase | `useAuth.ts`, `useDebounce.ts` |
| API 関数 | lowerCamelCase | `authApi.ts`, `userApi.ts` |
| サービス | lowerCamelCase | `authService.ts`, `userService.ts` |
| ユーティリティ | lowerCamelCase | `format.ts`, `validation.ts` |
| 定数 | lowerCamelCase | `config.ts`, `routes.ts` |
| 型定義 | lowerCamelCase | `types/index.ts` |
| テストファイル | 元ファイル名.test | `LoginForm.test.tsx`, `useAuth.test.ts` |

## インポートルール

### パスエイリアス設定（tsconfig.json）
```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@/features/*": ["./src/features/*"],
      "@/shared/*": ["./src/shared/*"]
    }
  }
}
```

### インポート順序
1. Feature 内部：相対パスを使用
2. Feature 外部：パスエイリアスを使用（@/features/auth, @/shared/components/ui）
3. バレルファイル：各 feature 直下の index.ts のみ。内部実装（api, services）は公開しない。