---
title: Docker が突然動かなくなった時の対応
tags: docker wsl
---

昨日まで元気に動いていた Docker が突然動かなくなった。で、このブログの記事を見つけて解決した：
[WSL 2でCannot connect to the Docker daemonと言われたら、デフォルトを確認する。 | Ginpen.com](https://ginpen.com/2020/11/24/wsl-2-cannot-connect-to-the-docker-daemon/)

具体的には PowerShell で次のコマンドを実行した。

```
> wsl --set-default Debian
```

最初、[Neeva](https://neeva.com/) の検索の結果が英語のページばかりで、それらには GRUB パッケージを削除すれば直ると書いてあったんだけど、ダメだった。
Google で検索すると上の日本語の記事が出てきた。

Twitter のスレッド：
[Toru Hisai on Twitter: "なぜか今朝いきなり Docker が動かなくなった。 Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? でも Docker Engine 自体は動いてるし、Docker Desktop のステータスも正常なんだよな。 Docker から WSL のファイルが見えてない感じかな。" / Twitter](https://twitter.com/torus/status/1499919466221948931)

なにがどうしてこうなったんだろう。
