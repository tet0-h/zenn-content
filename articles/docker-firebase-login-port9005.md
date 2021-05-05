---
title: "Dockerでfirebase loginしようとしたら9005ポートが開いてない問題の解決方法"
emoji: "🔥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["docker", "firebase"]
published: true
---

タイトルの通り、Docker で作った環境で firebase login しようとすると 9005 ポートを使って Google アカウントで認証がはしるけどポートが開いてないので蹴られる。

どうにかポートを開ける方法を探していたけど、そういうアプローチではなく、コマンドのオプションに
--no-localhost をつけて firebase login --no-localhost とすると、認証用のコードを表示するページに飛べるようになり、それを貼り付けると認証できる。

そもそもちゃんとそういう時のためのオプションが用意されていたという話。

無駄に時間を使ってしまった。公式ドキュメントはちゃんと隅々まで読もう。

https://firebase.google.com/docs/cli?hl=ja
