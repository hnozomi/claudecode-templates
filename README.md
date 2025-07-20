# Claude Code Templates

Claude Codeで使用する共通的なテンプレートとコードスニペットの集合

## 概要

このリポジトリは、Claude Codeを使用した開発作業で頻繁に使用されるテンプレート、コードスニペット、ユーティリティスクリプトを集めたものです。開発効率を向上させ、ベストプラクティスを共有することを目的としています。

## ディレクトリ構造

```
claudecode-templates/
├── README.md              # このファイル
├── .gitignore            # Gitで無視するファイルの設定
├── templates/            # テンプレートファイル
│   ├── web-development/  # Web開発用テンプレート
│   ├── data-analysis/    # データ分析用テンプレート
│   ├── automation/       # 自動化スクリプトテンプレート
│   └── utilities/        # ユーティリティテンプレート
├── scripts/              # 便利なスクリプト集
├── docs/                 # ドキュメント
└── examples/             # 使用例
```

## 使用方法

### 1. テンプレートの利用

必要なテンプレートを`templates/`ディレクトリから選択し、プロジェクトにコピーしてカスタマイズしてください。

```bash
# 例: Web開発テンプレートを使用
cp -r templates/web-development/react-app-template/* your-project/
```

### 2. スクリプトの実行

`scripts/`ディレクトリ内のスクリプトは直接実行可能です。

```bash
# 例: セットアップスクリプトの実行
./scripts/setup-environment.sh
```

### 3. サンプルコードの参照

`examples/`ディレクトリには、各テンプレートの使用例が含まれています。

## コントリビューションガイドライン

1. **新しいテンプレートの追加**
   - 適切なカテゴリディレクトリに配置
   - READMEファイルを含める
   - 使用例を`examples/`に追加

2. **既存テンプレートの改善**
   - プルリクエストを作成
   - 変更内容を明確に記述
   - 必要に応じてドキュメントを更新

3. **バグ報告**
   - Issueを作成
   - 再現手順を記載
   - 環境情報を含める

## ライセンス

MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.