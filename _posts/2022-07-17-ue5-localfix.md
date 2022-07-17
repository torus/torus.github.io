---
title: UE5 のローカル修正
tags: ue5 ue4
---

手元の UE5 のソースコードは shallow で fetch していて、修正したものは GitHub にプッシュできないので、Gist にパッチを置いた。
→ [UE5 local fix](https://gist.github.com/torus/44139605ffb744c607e4bb1c31fc6abe)

1 個目は、複雑な Blueprint を書くとパッケージに失敗するのを修正するもので、これは pull request も出したけど絶賛放置中になってる。

2 個目はさっき作ったもので、アセットのインポートを Python で自動化したときに、ダイアログボックスの質問に対するデフォルトの回答が指定されていないのを修正するもの。

ちなみに、GitHub にプッシュしようとしたときに出たエラーはこんな感じ：

```
toru@ryn:/mnt/e/UnrealEngine5$ git push mine localfix
Enumerating objects: 137165, done.
Counting objects: 100% (137165/137165), done.
Delta compression using up to 32 threads
Compressing objects: 100% (100841/100841), done.
Writing objects: 100% (137165/137165), 295.06 MiB | 4.03 MiB/s, done.
Total 137165 (delta 33107), reused 136189 (delta 33015), pack-reused 0
remote: Resolving deltas: 100% (33107/33107), done.
To github.com:torus/UnrealEngine.git
 ! [remote rejected]     localfix -> localfix (shallow update not allowed)
error: failed to push some refs to 'github.com:torus/UnrealEngine.git'
```
