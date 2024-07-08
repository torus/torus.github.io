---
title: Emacs の Compilation Mode で ANSI カラーを有効にする
---

![image](https://github.com/torus/torus.github.io/assets/65044/6c4aa9cd-d296-41d5-9d23-dd425f2e0f3c){:width="240"}
➡️
![image](https://github.com/torus/torus.github.io/assets/65044/0daefdf1-6613-4fab-8c97-2a85a1492b1f){:width="240"}

Emacs で `M-x compile` としてユニットテストを走らせたいときとかに、エスケープシーケンスがそのまま表示されて読みづらかった。
しらべてみると `ansi-color-for-compilation-mode` という変数は初期状態から有効になっていた。
でも、Compilation Mode でそれを有効にするにはフックを追加する必要があった。

>   In order for this to have any effect, ‘ansi-color-compilation-filter’
>   must be in ‘compilation-filter-hook’.

このフックは Emacs の Customize では設定できないようだったので .emacs に手動で書き足した。

```
   (add-hook 'compilation-filter-hook 'ansi-color-compilation-filter)
```
