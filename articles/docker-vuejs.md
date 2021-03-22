---
title: "DockerでVue.jsの環境を作るまでの手順"
emoji: "🐳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Docker","vuejs",]
published: true
---
Dockerを使ってVue.jsの環境を作りたかったのでその記録です。

## 環境
- MacBook Air (M1, 2020) MacOS Big Sur
- Docker version 20.10.1
- docker-compose version 1.27.4

## フォルダ構成
```bash
project
├── docker
│   └── web
│       └── Dockerfile
├── docker-compose.yml
└── server
```

## docker-compose.yml
```yml
version: '3.8'

services:
  web:
    container_name: web
    build: ./docker/web
    ports:
      - 9000:9000
    privileged: true
    volumes:
      - ./server:/app
    tty: true
    stdin_open: true
    command: /bin/sh
```
ポートは9000にしてますけど、自身の環境に合わせて変えてください。ちなみにVue.jsのデフォルトポートは8080のようです。

## Dockerfile
Webフォルダの下に下記の様なDockerfileを作ります。FROMの値は適宜変えてください。
```dockerfile
FROM node:15.11.0-alpine

WORKDIR /app

RUN apk update && \
    npm install && \
    npm install -g npm && \
    npm install -g vue-cli
```

## Docker起動してコンテナに入る
```bash
# Docker構築&起動
docker-compose up -d

# コンテナに入る
docker-compose exec web sh
```

## Vue.jsプロジェクトを作成

コンテナに入ってプロジェクトを作成します。
```bash
/app # vue init webpack
# y/nで質問されますが、こだわりなければ基本yesまたはEnterでOK。こだわりがあればお好きな様に。
```

### 環境設定
project/server/config/index.js の値を環境に合わせて変更します。
hostを'localhost'から'0.0.0.0'に変更します。
```js
// Various Dev Server settings
host: '0.0.0.0', // can be overwritten by process.env.HOST
```
また、docker-compose.ymlでportも変更した場合、それに合わせてindex.jsのportも変更します。
私はdocker-compose.ymlで9000番を設定したので9000を設定します。
```js
port: 9000, // can be overwritten by process.env.PORT, if port is in use, a free one will be determined
```
さらに、ファイル変更も検知されるようにpollの値をtureにします。
```js
poll: true, // https://webpack.js.org/configuration/dev-server/#devserver-watchoptions-
```

## 実行
index.jsの値を変更し終えたらnpm run devで実行します。
```bash
/app # npm run dev
```

## 動作確認
http://0.0.0.0:9000/ にアクセスします。いつものこの画面がでればOKです。/project/server/src/components/HelloWorld.vue の中身も適当に変更して、変更が反映されるかも確認しておきましょう。

![](https://storage.googleapis.com/zenn-user-upload/7gdkhwcjfrrfqbmheqezy0gajl1a)

参考にしたページ：
https://qiita.com/A-Kira/items/ed12de84dda0230a4eae
