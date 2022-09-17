---
title: Ubuntu で ptrace を使うときに必要な設定
tags: ubuntu
---

ptrace コマンドを誰がどのプロセスに対して使えるかは、このファイルで制御されている：
/proc/sys/kernel/yama/ptrace_scope

この値を 0 にすると、自分で起動したプロレスに対して ptrace できるようになる。
gdb でプロセスにアタッチするときにもこれが必要になる。

cf. [Protect against ptrace of processes: kernel.yama.ptrace_scope](https://linux-audit.com/protect-ptrace-processes-kernel-yama-ptrace_scope/)
