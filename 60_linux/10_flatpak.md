Flathubは、Linuxディストリビューション向けのFlatpakアプリケーションを配布する中央リポジトリです。以下に基本的な使い方を説明します。

## Flatpakのセットアップ

まず、お使いのLinuxディストリビューションにFlatpakをインストールする必要があります：

**Ubuntu/Debian系：**
```bash
sudo apt install flatpak
```

**Fedora：**
```bash
sudo dnf install flatpak
```

**Arch Linux：**
```bash
sudo pacman -S flatpak
```

## Flathubリポジトリの追加

Flatpakをインストールしたら、Flathubリポジトリを追加します：

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

## アプリケーションの検索とインストール

**コマンドラインから：**
```bash
# アプリケーションを検索
flatpak search アプリ名

# アプリケーションをインストール
flatpak install flathub com.example.AppName

# インストール済みアプリの一覧表示
flatpak list

# アプリケーションの実行
flatpak run com.example.AppName
```

**Webブラウザから：**
1. https://flathub.org にアクセス
2. 欲しいアプリを検索
3. アプリページで「Install」ボタンをクリック
4. .flatpakrefファイルをダウンロードして実行

## アプリケーションの管理

```bash
# アプリケーションの更新
flatpak update

# アプリケーションのアンインストール
flatpak uninstall com.example.AppName

# 未使用のランタイムを削除
flatpak uninstall --unused
```

## GUIでの管理

多くのLinuxディストリビューションでは、ソフトウェアセンター（GNOME Software、KDE Discoverなど）からもFlathubアプリを直接インストール・管理できます。

Flathubを使用することで、最新版のアプリケーションを安全にサンドボックス環境で実行でき、ディストリビューションに依存しない統一的なアプリ管理が可能になります。