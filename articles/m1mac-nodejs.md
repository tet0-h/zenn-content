---
title: "M1 Macにnvmを使ってNode.jsをインストールする"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["M1", "Mac", "nvm", "Nodejs", "Homebrew"]
published: true
---

M1 MacにNode.jsをインストールします。

一応バージョン管理もできた方がいいと持ったのでnvmを使います。

[こちらの記事](https://note.com/kakedashi30/n/n13e4e23abfc0)を参考にしました。

[前回の記事](https://zenn.dev/tet0h/articles/a92651d52bd82460aefb)でHomebrewはインストールできていたので
```bash
brew install nvm
```
でインストールしようとしたら
```bash
Error: No developer tools installed.
Install the Command Line Tools:
  xcode-select --install
```
と怒られました。
あれ？インストールしてたつもりでいたのに気のせいだった？？
とりあえずインストールします。
10分弱待ちました。

command line toolをインストールした後、再度
```bash
brew install nvm
```
を叩くと無事インストールは完了しました。
インストール後の画面に
```bash
Please note that upstream has asked us to make explicit managing
nvm via Homebrew is unsupported by them and you should check any
problems against the standard nvm install method prior to reporting.

You should create NVM's working directory if it doesn't exist:

  mkdir ~/.nvm

Add the following to ~/.zshrc or your desired shell
configuration file:

  export NVM_DIR="$HOME/.nvm"
  [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion

You can set $NVM_DIR to any location, but leaving it unchanged from
/opt/homebrew/opt/nvm will destroy any nvm-installed Node installations
upon upgrade/reinstall.
```
と言われたので $HOME で
```bash
mkdir ~/.nvm
```
して、その後 ~/.zshrc に
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh" # This loads nvm
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" # This loads nvm bash_completion
```
を追記し、シェルを起動し直したら無事パスも通りました。
インストールされてバージョンは0.37.2でした。

これでnvmがインストールできました。

```bash
nvm ls-remote
```
上記コマンドで登録されているNode.jsのバージョンを確認したところ最新が15.11.0でした。
```bash
nvm i v15.11.0
```
でインストールします。
時間はかかりますが特に問題なく終了。
```bash
node -v
v15.11.0
```
```bash
nvm current
v15.11.0
```
```bash
node -p process.arch
arm64
```

バージョンもv15.11.0になっているしプロセスもARM64になっているので大丈夫そうです。