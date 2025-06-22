npmでGitからプロジェクトを取得した後に行う基本的な手順を説明します。

## 基本的な流れ

### 1. プロジェクトのクローンまたはダウンロード

```bash
# GitHubからクローン
git clone https://github.com/username/project-name.git
cd project-name

# または特定のブランチをクローン
git clone -b develop https://github.com/username/project-name.git
```

### 2. プロジェクト構造の確認

```bash
# ディレクトリ構造確認
ls -la

# 重要なファイルの確認
cat package.json
cat README.md
```

### 3. Node.jsバージョンの確認

```bash
# プロジェクトが要求するNode.jsバージョンを確認
cat .nvmrc          # nvmrcファイルがある場合
cat package.json    # enginesフィールドを確認

# 現在のNode.jsバージョン確認
node --version
npm --version
```

#### Node.jsバージョン管理（必要に応じて）
```bash
# nvmを使用してバージョン切り替え
nvm use            # .nvmrcがある場合
nvm use 18.17.0    # 特定バージョンを指定

# 指定バージョンがインストールされていない場合
nvm install 18.17.0
nvm use 18.17.0
```

### 4. 依存関係のインストール

```bash
# package.jsonの依存関係をインストール
npm install

# または短縮形
npm i

# 開発依存関係も含めてインストール（通常は自動）
npm install --include=dev
```

#### パッケージマネージャーの確認
```bash
# yarn.lockがある場合はYarnを使用
yarn install

# pnpm-lock.yamlがある場合はpnpmを使用
pnpm install
```

### 5. 環境変数の設定

```bash
# .env.exampleがある場合
cp .env.example .env

# .env.templateがある場合
cp .env.template .env

# 環境変数ファイルを編集
nano .env
# または
code .env
```

#### 一般的な環境変数例
```bash
# .env
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
API_KEY=your-api-key-here
JWT_SECRET=your-jwt-secret
```

### 6. 利用可能なスクリプトの確認

```bash
# package.jsonのscriptsセクションを確認
npm run

# または
cat package.json | grep -A 10 "scripts"
```

### 7. プロジェクトの起動

```bash
# 開発サーバー起動（一般的なコマンド）
npm start
npm run dev
npm run serve

# ビルド（必要に応じて）
npm run build

# テスト実行
npm test
npm run test
```

## プロジェクトタイプ別の追加手順

### React/Vue.js/Angularプロジェクト

```bash
# 依存関係インストール
npm install

# 開発サーバー起動
npm start          # React (Create React App)
npm run dev        # Vite, Nuxt.js
npm run serve      # Vue CLI

# ビルド
npm run build

# プレビュー（Viteの場合）
npm run preview
```

### Next.jsプロジェクト

```bash
# 依存関係インストール
npm install

# 開発サーバー起動
npm run dev

# 本番ビルド
npm run build

# 本番サーバー起動
npm start
```

### Express.js/Node.jsサーバー

```bash
# 依存関係インストール
npm install

# 開発モード起動（nodemonなど）
npm run dev

# 本番モード起動
npm start

# データベースセットアップ（必要に応じて）
npm run db:migrate
npm run db:seed
```

### TypeScriptプロジェクト

```bash
# 依存関係インストール
npm install

# TypeScriptコンパイル
npm run build
npm run tsc

# 開発サーバー起動
npm run dev

# 型チェック
npm run type-check
```

## よくある問題と解決方法

### 1. Node.jsバージョン不一致

```bash
# エラー例: "Node.js version mismatch"
# 解決法
nvm use $(cat .nvmrc)
# または指定されたバージョンをインストール
nvm install 18.17.0 && nvm use 18.17.0
```

### 2. 依存関係の競合

```bash
# node_modulesとlockファイルを削除して再インストール
rm -rf node_modules
rm package-lock.json
npm install

# または npm cache をクリア
npm cache clean --force
npm install
```

### 3. 権限エラー

```bash
# Macの場合のnpm権限設定
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules

# または npmの設定変更
npm config set prefix ~/.npm-global
export PATH=~/.npm-global/bin:$PATH
```

### 4. ポート競合

```bash
# .envファイルでポート変更
PORT=3001

# または実行時に指定
PORT=3001 npm start
```

## プロジェクト設定の確認

### package.jsonの重要項目確認

```bash
# エンジン要件
"engines": {
  "node": ">=18.0.0",
  "npm": ">=8.0.0"
}

# スクリプト
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js",
  "build": "webpack --mode production",
  "test": "jest"
}

# 依存関係
"dependencies": {},
"devDependencies": {}
```

### 設定ファイルの確認

```bash
# よくある設定ファイル
ls -la | grep -E '\.(config|rc)'

# 例
.eslintrc.js      # ESLint設定
.prettierrc       # Prettier設定
webpack.config.js # Webpack設定
vite.config.js    # Vite設定
tsconfig.json     # TypeScript設定
```

## ベストプラクティス

### 1. READMEファイルを必ず読む
```bash
cat README.md
# または
less README.md
```

### 2. 段階的にセットアップ
```bash
# 1. 依存関係インストール
npm install

# 2. 環境変数設定
cp .env.example .env

# 3. 開発サーバー起動
npm run dev

# 4. ブラウザで確認
# http://localhost:3000 など
```

### 3. Git設定（必要に応じて）
```bash
# 上流リポジトリ設定（フォークした場合）
git remote add upstream https://github.com/original-author/project.git

# ブランチ作成
git checkout -b feature/your-feature
```

### 4. コードの品質チェック
```bash
# リンティング
npm run lint

# フォーマット
npm run format

# テスト
npm test
```

この手順に従うことで、Gitから取得したnpmプロジェクトを正しくセットアップして開発を開始できます。プロジェクト固有の要件については、必ずREADMEファイルを確認してください。