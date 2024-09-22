---
title: AMDGPU のインストールで DKMS のエラーが出たときの対処
---

Ubuntu のマシンで AMD の Radeon グラフィックスカードをつかうには、つぎのサイトから公式のドライバをダウンロードできる：
[Linux® Drivers for AMD Radeon™ and Radeon PRO™ Graphics](https://www.amd.com/en/support/download/linux-drivers.html)

ここで Ubuntu のバージョンを選択するけど、Ubuntu 20.04.6 と 22.04.4 しかリストされていなくて、最新版の 24.04 が選べない。
そういうときでも次のダウンロードサイトに直接アクセスすることで必要なバージョンが見つかることがある：
[Index of /amdgpu-install/](https://repo.radeon.com/amdgpu-install/)

ここで最新版の latest→ubuntu というリンクを選ぶと focal、jammy、noble という Ubuntu の開発コード名がリストされる。
自分がいま使っているコード名を調べるには /etc/os-release というファイルの中身を表示すると良い。

で、無事にファイルがダウンロードできたら、次はこれをインストールする。
インストールの手順は次のページに書かれている：
[Radeon™ Software for Linux® Installation — amdgpu graphics and compute stack unknown-build documentation](https://amdgpu-install.readthedocs.io/en/latest/)

ここでインストールされるのは `amdgpu-install` というドライバのインストーラだけで、ドライバ自体はインストールされないのに注意しなくてはいけない。

で、`amdgpu-install` コマンドを実行すると関連する APT パッケージがインストールされるけど、なぜか下のようなエラーがでて正常に終了しない：

```
Error! Could not locate dkms.conf file.
File: /var/lib/dkms/amdgpu/6.3.6-1739731.22.04/source/dkms.conf does not exist.
```

DKMS というのは Dynamic Kernel Module Support の略らしい。
カーネルの話になるとお手上げだ。
ただ、エラーメッセージに表示されたファイルをしらべてみると、単にシンボリックリンクが壊れているだけだった。
おそらく過去にインストールしたバージョンのゴミが残っているだけのようだった。
壊れたシンボリックリンクを削除したら `amdgpu-install` が正常に終了した。

`amdgpu-install` の実行時にはオプションを何も渡さなかった。
なので、Vuklan もインストールされないかと思ったけど、なぜか UE5 などの Vulkan アプリケーションは普通に動いている。
でも vulkaninfo コマンドを実行するとちゃんとハードウェアの Vulkan 拡張などは認識されているようなので、これで問題なさそう。


Twitter に経緯を書いた：
[Toru Hisai on X: "なんか Xorg で起動しようとするとログイン後すぐにログアウトしてしまう。 Wayland ではログインはできるがなんかグラフィックデバイスがおかしい。 関係あるかわからないけど、syslog をみると MESA: error: ZINK: failed to choose pdev とかいってる。 https://t.co/0FTVvbXQIw" / X](https://x.com/torus/status/1835509838534869240)
