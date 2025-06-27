Snapの基本的な使い方について説明します。

## Snapとは
SnapはUbuntuが開発したパッケージ管理システムで、アプリケーションを独立したコンテナ形式で配布・インストールできます。

## 基本コマンド

**インストール済みのSnapパッケージを確認**
```bash
snap list
```

**新しいパッケージをインストール**
```bash
sudo snap install パッケージ名
```

**パッケージをアンインストール**
```bash
sudo snap remove パッケージ名
```

**利用可能なパッケージを検索**
```bash
snap find キーワード
```

**インストール済みパッケージの更新**
```bash
sudo snap refresh パッケージ名
```

**全てのパッケージを更新**
```bash
sudo snap refresh
```

## 実用例

人気のあるアプリケーションのインストール例：
```bash
sudo snap install code          # Visual Studio Code
sudo snap install discord       # Discord
sudo snap install firefox       # Firefox
sudo snap install vlc           # VLC メディアプレイヤー
```

## 便利な機能

**パッケージ情報の詳細表示**
```bash
snap info パッケージ名
```

**インストール履歴の確認**
```bash
snap changes
```

Snapは依存関係を自動的に解決し、セキュアな環境でアプリケーションを実行するため、従来のパッケージ管理システムよりも安全で使いやすいのが特徴です。