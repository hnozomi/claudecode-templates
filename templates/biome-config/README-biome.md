# Biome設定テンプレート

JavaScript/TypeScriptプロジェクト用の汎用的なBiome設定ファイル集です。

## 📁 ファイル構成

```
biome-config/
├── biome.json              # Biome設定ファイル（メイン）
├── package.json            # npm scriptsテンプレート
├── .vscode-settings.json   # VSCode統合設定
└── README-biome.md         # このファイル
```

## 🚀 セットアップ手順

### 1. 基本セットアップ

```bash
# 1. Biomeをインストール
npm install --save-dev @biomejs/biome

# 2. 設定ファイルをプロジェクトルートにコピー
cp biome.json your-project/biome.json

# 3. package.jsonにスクリプトを追加
# package.jsonの"scripts"セクションにコピー&ペースト
```

### 2. VSCode統合

```bash
# 1. VSCode拡張機能をインストール
# 「Biome」拡張機能をVSCodeにインストール

# 2. VSCode設定をコピー
mkdir your-project/.vscode
cp .vscode-settings.json your-project/.vscode/settings.json
```

### 3. 動作確認

```bash
# 全体チェック（推奨）
npm run check

# 自動修正
npm run check:fix

# フォーマットのみ
npm run format
```

## 📋 主要コマンド一覧

### 基本操作

| コマンド | 役割 | 使用タイミング |
|----------|------|----------------|
| `npm run check` | 全体チェック（リント+フォーマット+インポート整理） | **最も推奨** - 定期的な品質確認 |
| `npm run check:fix` | 自動修正付き全体チェック | コーディング後の一括修正 |
| `npm run check:ci` | CI用チェック（修正なし） | GitHub Actions等での品質確認 |

### 個別操作

| コマンド | 役割 | 使用タイミング |
|----------|------|----------------|
| `npm run lint` | リンターのみ実行 | コード品質のみ確認したい場合 |
| `npm run format` | フォーマッターのみ実行 | スタイル統一のみ必要な場合 |
| `npm run imports` | インポート整理のみ実行 | 依存関係整理のみ必要な場合 |

### 開発フロー統合

| コマンド | 役割 | 使用タイミング |
|----------|------|----------------|
| `npm run pre-commit` | コミット前品質チェック | Git commit前の自動実行 |
| `npm run clean-code` | コード全体クリーンアップ | リファクタリング時 |

## ⚙️ 設定内容詳細

### biome.json の主要設定

```json
{
  // フォーマッター設定
  "formatter": {
    "indentStyle": "space",     // スペースインデント
    "indentWidth": 2,           // 2スペース幅
    "lineWidth": 80,            // 1行80文字制限
    "semicolons": "always",     // セミコロン必須
    "quoteStyle": "single",     // シングルクォート使用
    "trailingCommas": "all"     // 末尾カンマ付与
  },
  
  // リンター設定
  "linter": {
    "rules": {
      "recommended": true,      // 推奨ルールを全て有効
      "correctness": { ... },   // バグ防止ルール
      "performance": { ... },   // パフォーマンス最適化
      "security": { ... },      // セキュリティ強化
      "style": { ... },         // コードスタイル統一
      "suspicious": { ... }     // 疑わしいコード検出
    }
  }
}
```

### 特別な設定

#### ファイルタイプ別オーバーライド

- **テストファイル**: `console.log` 許可、複雑度チェック緩和
- **設定ファイル**: `require()` 使用許可
- **JSONファイル**: 末尾カンマ無効化

#### 除外ファイル

- `node_modules/`, `dist/`, `build/`, `.next/`
- `*.min.js`, `*.bundle.js`
- 環境変数ファイル (`.env*`)

## 🛠️ カスタマイズガイド

### プロジェクト固有の調整

```json
// より厳しい設定にする場合
{
  "linter": {
    "rules": {
      "suspicious": {
        "noConsoleLog": "error"  // console.logを完全禁止
      },
      "complexity": {
        "noExcessiveCognitiveComplexity": "error"
      }
    }
  }
}

// より緩い設定にする場合
{
  "linter": {
    "rules": {
      "style": {
        "useTemplate": "warn"  // テンプレートリテラル強制を警告に
      }
    }
  }
}
```

### フレームワーク別の追加設定

#### Next.js プロジェクト

```json
{
  "files": {
    "ignore": [
      "**/.next/**",
      "**/out/**",
      "**/.vercel/**"
    ]
  }
}
```

#### React Native プロジェクト

```json
{
  "files": {
    "ignore": [
      "**/android/**",
      "**/ios/**",
      "**/node_modules/**"
    ]
  },
  "javascript": {
    "globals": [
      "__DEV__",
      "global",
      "require"
    ]
  }
}
```

## 🔄 ESLint/Prettierからの移行

### 1. 既存設定の無効化

```json
// package.json
{
  "scripts": {
    // ESLint/Prettierスクリプトをコメントアウトまたは削除
    // "lint": "eslint .",
    // "format": "prettier --write ."
  }
}
```

### 2. 設定ファイルの移行

```bash
# ESLint設定の移行（オプション）
npx biome migrate eslint --write

# Prettier設定の移行（オプション）
npx biome migrate prettier --write
```

### 3. VSCode拡張機能の調整

```json
// .vscode/settings.json
{
  "eslint.enable": false,
  "prettier.enable": false,
  "editor.defaultFormatter": "biomejs.biome"
}
```

## 🚨 トラブルシューティング

### よくある問題と解決方法

#### 1. Biomeが動作しない

```bash
# Biomeがインストールされているか確認
npx biome --version

# 設定ファイルの構文チェック
npx biome check --config-path=./biome.json
```

#### 2. VSCodeでフォーマットが効かない

- Biome拡張機能がインストールされているか確認
- `editor.defaultFormatter` が `"biomejs.biome"` に設定されているか確認
- VSCodeを再起動

#### 3. 他のツールとの競合

```json
// .vscode/settings.json で他のフォーマッターを無効化
{
  "eslint.enable": false,
  "prettier.enable": false,
  "[javascript]": {
    "editor.defaultFormatter": "biomejs.biome"
  }
}
```

#### 4. パフォーマンス問題

```json
// 大きなプロジェクトの場合
{
  "files": {
    "ignore": [
      "**/dist/**",
      "**/coverage/**",
      "**/*.min.js"
    ]
  }
}
```

## 📈 CI/CD統合

### GitHub Actions

```yaml
name: Code Quality Check
on: [push, pull_request]

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run check:ci
```

### pre-commit hooks

```bash
# Huskyのインストール
npm install --save-dev husky

# pre-commitフックの設定
npx husky add .husky/pre-commit "npm run pre-commit"
```

## 🎯 ベストプラクティス

### 1. 開発フロー統合

```bash
# 開発開始時
npm run check:fix

# コミット前
npm run pre-commit

# CI/CD
npm run check:ci
```

### 2. チーム開発

- `biome.json` と `.vscode/settings.json` をリポジトリにコミット
- チーム全体で同じBiomeバージョンを使用
- プロジェクト固有のルール調整は必要最小限に

### 3. 段階的導入

```bash
# 1. まずフォーマッターのみ
npm run format

# 2. 次にリンター
npm run lint:fix

# 3. 最後に全体統合
npm run check:fix
```

## 📚 参考リンク

- [Biome公式ドキュメント](https://biomejs.dev/)
- [Biome設定リファレンス](https://biomejs.dev/reference/configuration/)
- [VSCode拡張機能](https://marketplace.visualstudio.com/items?itemName=biomejs.biome)
- [移行ガイド](https://biomejs.dev/guides/migrate-eslint-prettier/)

## 📝 更新履歴

- v1.0.0 - 初回リリース（Biome v1.9.4対応）