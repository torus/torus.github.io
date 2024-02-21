---
title: Emacs のフレームの位置とサイズの設定
tags: [emacs]
---

`initial-frame-alist` という変数を `customize` で設定する。

![image](https://github.com/torus/torus.github.io/assets/65044/fc75c1f3-66fd-4564-b1e8-0aaa54521cbf)

高さは画面いっぱい、幅は 80 桁 2 枚分に少し遊びをもたせて 170、画面右端にだしたいので `left` を -1 にした。

```
 '(initial-frame-alist '((height . 66) (width . 170) (left . -1)))
```
