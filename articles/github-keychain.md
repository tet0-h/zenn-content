---
title: "キーチェーン内のgithubの認証情報を書き換える方法"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["github", "Mac", "KeyChain"]
published: true
---
Githubにpushしようとしたら403エラーが返ってきてpush出来ませんでした。

理由は単純で、パスワードを使って認証をしていたから。

Githubは2021/08/13以降パスワードの認証を受け入れなくなるとアナウンスされていたにもかかわらずめんどくさがって対応をしていなかったから。

https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/

個人のアクセストークンを使用するようにすれば問題なし。

やり方はこちら↓
https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token

しかし手順通りにやったつもりでもうまくいかず…

原因はキーチェーン内に前の認証情報が残っていたからでした。

削除もうまくいかなかったので、ここでは情報を更新する方法をメモしておきます。

## キーチェーン内のGithub認証情報を更新する

![](https://storage.googleapis.com/zenn-user-upload/b7a2580928bd1d8c0717c5c0.png)

検索窓にgitなどと打ち込むとgithub.comが出てきます。

私の環境の場合何故か削除ができなかったので

![](https://storage.googleapis.com/zenn-user-upload/470e8f3bebed6b2a1241172d.png)

「情報を見る」から

![](https://storage.googleapis.com/zenn-user-upload/ea7501eed886bb3b2b51a8b8.png)

「パスワードを表示」にチェックを入れると管理者権限を求められます。管理者権限のパスワードを入力すると、github.comのパスワードが表示されるので

https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token

のページの方法で作っておいたトークンに書き換えて、「変更内容を保存」すればOK。

これで問題なくpushできるようになりました。