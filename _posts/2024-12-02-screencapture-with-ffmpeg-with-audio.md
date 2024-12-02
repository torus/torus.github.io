---
title: FFmpeg で音声付きで画面を録画するコマンド
---

ChatGPT に聞いてみたら微妙に間違った答えが返ってきたので少し調べ直した。

まず `xwininfo` というコマンドでウィンドウの位置とサイズを調べる。

```
$ xwininfo

xwininfo: Please select the window about which you
          would like information by clicking the
          mouse in that window.

xwininfo: Window id: 0x440002f "Umi (64-bit Development SF_VULKAN_SM5) "

  Absolute upper-left X:  1820
  Absolute upper-left Y:  748
  Relative upper-left X:  14
  Relative upper-left Y:  49
  Width: 1920
  Height: 1080
  Depth: 24
  Visual: 0x22
  Visual Class: DirectColor
  Border width: 0
  Class: InputOutput
  Colormap: 0x440002e (not installed)
  Bit Gravity State: ForgetGravity
  Window Gravity State: NorthWestGravity
  Backing Store State: NotUseful
  Save Under State: no
  Map State: IsViewable
  Override Redirect State: no
  Corners:  +1820+748  -100+748  -100-332  +1820-332
  -geometry 1920x1080-86+699
```

このうちで Absolute upper-left と Width、Hight の値を覚えておく。この情報を使って次のように ffmpeg コマンドを呼び出す。

```
$ ffmpeg -video_size 1920x1080 -framerate 25 \
  -f x11grab -i :0.0+1820,748 \
  -f alsa -ac 2 -i pulse -acodec copy \
  output.mp4
```

`-video_size` で画面のサイズを指定する。
このオプションはそれ以降の `-f` オプションよりも前に書かなければいけないらしい。
それから `-f x11grab` 以下のオプションで X のディスプレイ ID（通常は `0.0`）とサイズを指定する。
さらに `-f alsa` 以下のオプションで音声入力を指定する。
