---
title: "TypeScriptで非推奨になったコードを洗い出す方法はないのか??"
emoji: "🔍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["TypeScript","ESLint"]
published: true
---
利用していたTypeScriptのバージョンを上げた時に今まで使っていたコードが非推奨になっていたりすること、あると思います。

VSCode上で見ると打ち消し線が引かれていて気付けるけど、規模が大きいプロジェクトだと全ファイル目視とかしんどすぎるのでtscとかでわからんのん？？と思いました。

それで調べたらこんなものを見つけました。

https://www.npmjs.com/package/eslint-plugin-deprecation

ESLintでできそう。

というわけで試してみたところこのプラグインを導入したら無事プロジェクト全体をESLintでチェックして非推奨コードを洗い出すことができました！

どうやら@deprecationが付いているものを拾っていそうな感じでした。

大変助かりました。