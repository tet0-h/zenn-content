---
title: "router-viewでなぜかコンポーネントが二つ重なる問題"
emoji: "👻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["veu", "vue3"]
published: ture
---

Vue3 で vue-router を使おうとしたら router-view を指定しているところで何故かコンポーネントが 2 つ重複して表示されて困ってしまった。

全然理由がわからず右往左往していたのだが、原因は router-view を　<router-view/>
と指定していたことだった。
<router-view></router-view>　としたら解決した。

すごくハマってしまった…
