---
title: Docker compose でビルドコンテキストを指定する
---

Docker 関連のファイルは他の主要なファイルに紛れ込まないように別のフォルダに隔離したい。
でもそうすると `docker-compose build` した時にビルドコンテキストの外のファイルを参照することになってしまい、イメージがビルドできない。

この状況に対応するために、`docker-compose` にはビルドコンテキストと Dockerfile を個別に指定する機能がある。
下のように `build:` の下に `dockerfile` と `context` を指定するだけ。
Dockerfile のパスはビルドコンテキストからの相対パスになることに注意する。

便利！

```
version: '3'
services:
  my-service:
    build:
      dockerfile: ./my/service/Dockerfile
      context: ../..
    ports:
      - "8080:8080"
    environment:
      PORT: "8080"
```

c.f. [Compose Build Specification \| Docker Docs](https://docs.docker.com/compose/compose-file/build/#context)
