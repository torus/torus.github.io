---
title: Ubuntu のマイク入力に対するノイズキャンセリング
tags: linux ubuntu
---

Ubuntu でマイクを使うとノイズがものすごいので設定を調べてみた。
まず PulseAudio の設定でノイズキャンセルっぽいのがあるのを見つけたのでそのとおり設定してみた。
cf. [sound - Microphone static noise - Ask Ubuntu](https://askubuntu.com/questions/722913/microphone-static-noise)

具体的にはまず以下の内容を `/etc/pulse/default.pa.d/echo_cancel.pa` というファイルに書き込んだ。

```
set-default-source echoCancel_source
set-default-sink echoCancel_sink
load-module module-echo-cancel use_master_format=1 aec_method=webrtc aec_args="noise_suppression=1" source_name=echoCancel_source sink_name=echoCancel_sink
set-default-source echoCancel_source
set-default-sink echoCancel_sink
```

次に PulseAudio を再起動した。

```
$ pulseaudio -k && pulseaudio --start
```

pulseaudio コマンドは root ではなく一般ユーザとして実行する。

pacmd コマンドで `module-echo-cancel` が有効になっているかを確認した。

```
$ pacmd list-modules | grep echo
	name: <module-echo-cancel>
	argument: <use_master_format=1 aec_method=webrtc aec_args="noise_suppression=1" source_name=echoCancel_source sink_name=echoCancel_sink>
```

ちゃんと反映されているっぽい。Zoom の [テストミーティング](https://zoom.us/test) で自分の声を聞いてみたけどノイズはきれいになくなっていた。

### 追記

どうやらやっぱり上記の設定はもともと意図していたヘッドセットのマイクには反映されていなくて、ウェブカムについてるマイクにだけ適用されているようだった。Zoom や Google Meet ではノイズがきれいに除去されていたけど、これはおそらくサーバ側でのノイズキャンセリングの機能によるものと思われる。

というわけなので、一旦上の設定は削除する。
