---
title: docker-compose.yml に書く各種のパス
---

下のような docker-compose.yml があるとする：

```
version: '3'
services:
  local-dev:
    build:
      dockerfile: ./${PROJECT_DIR}/gcloud/Dockerfile
      context: ..
    volumes:
      - ..:/app
```

`context` は docker-compose.yml ファイルからの相対パス。
これは `docker-compose` コマンドを `-f` オプション付きで実行したときにも当てはまる。
すなわち、`docker-compose` が実行されたときのカレントディレクトリの影響を受けない。

`dockerfile` は `context` からの相対パス。
同様に `volumes` も `context` からの相対パス。
