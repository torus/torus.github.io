---
title: UE5 のフルスクリーン設定
---

UE5 の Game User Settings の下の `FullscreenMode` は、0 がフルスクリーンで、2 がウィンドウを意味する。
これまでずっと 1 がフルスクリーンモードだと思ってた。

したがって、Saved/Config/WindowsEditor/GameUserSettings.ini などに下のように書くとゲームがウィンドウ表示になる。
通常、PIE では Game User Settings が読み込まれないが、明示的に読み込もうとすると上のパスから読み込まれるらしい。

```ini
[/Script/Engine.GameUserSettings]
FullscreenMode=2
```
