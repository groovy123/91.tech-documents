# VSCode関連


### 権限がないファイルをVSCodeで編集する
権限がないファイル（httpd.confなど）をVSCodeで編集する方法。linuxではsudoeditというコマンドがあってこちらを使うと安全にファイルを編集できる。aliasを作成してsudoeditでvscodeを開くように設定する。

```bash
# .bash_aliasesは.bashrc内で呼ばれる
vim .bash_aliases

# 以下の内容を追加して保存
alias sudocode='SUDO_EDITOR="$(which code) --wait" sudoedit'

# 以下実行するとVSCodeでファイルが開く。他のテキストと同じように編集できる
sudocode httpd.conf
```
