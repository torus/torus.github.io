---
title: Windows の Git を WSL で使うとファイルの実行パーミッションが扱えない
tag: git
---

普段 WSL のターミナルで Git を使うときに Windows ネイティブの Git を使うように `alias git=git.exe` と指定していて、これでこれまでうまくいってた。
でも、WSL の Linux ファイルシステムで Windows 版 Git を使うと、Windows と Linux のファイルシステムの差異のためにファイルの実行パーミッションが Git から見えないことが分かった。

![image](https://user-images.githubusercontent.com/65044/170804210-6fa06694-c74a-4dd4-9432-309f3e8f1224.png)

Linux アプリケーションを作っていて、実行可能なスクリプトなどを含める時は、Linux 版の Git を使う必要がある。
