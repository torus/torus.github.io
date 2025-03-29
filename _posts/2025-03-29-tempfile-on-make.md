---
title: GNU Make 一時ファイルを使う
---

コマンドが成功したときのみターゲットのファイルを更新したいときは下のように指定する。

```make
TMPFILE := $(shell mktemp -u --tmpdir=.)
$(TAEGET): $(SRC)
	$(COMMAND) $(SRC) > $(TMPFILE)
	mv $(TMPFILE) $(TARGET)
```

コマンドの出力をそのままターゲットにリダイレクトすると、コマンドが失敗してもファイルが更新されてしまうので、それを避けるために一時ファイルを作る。

一時ファイルの名前には `mktemp -u` コマンドの出力を使う。
ここで `:=` を使って `TMPFILE` に代入することで、何度も繰り返し呼ばれることを防ぐ。
(cf. [Setting (GNU make)](https://www.gnu.org/software/make/manual/html_node/Setting.html))
