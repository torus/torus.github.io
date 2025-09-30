---
title: migemo を Windows で使う
---
- Windows ネイティブ版の [C/Migemo](https://www.kaoriya.net/software/cmigemo/) をダウンロードして Windows のホームディレクトリの local というディレクトリに展開する。
- 環境変数 PATH を設定して Emacs から見えるようにする。
- MELPA から migemo を Emacs にインストールする。
- 下のような設定を .emacs に書く：

```lisp
(require 'migemo)

;; cmigemo(default)
(setq migemo-command "cmigemo")
(setq migemo-options '("-q" "--emacs"))

;; Set your installed path
(setq migemo-dictionary
      (file-name-concat (getenv "HOME")
                        "local/cmigemo-default-win64/dict/utf-8/migemo-dict"))

(setq migemo-user-dictionary nil)
(setq migemo-regex-dictionary nil)
(setq migemo-coding-system 'utf-8-unix)
(migemo-init)
```

- ファイルのパスを連結するときは `file-name-concat` を使うといいらしい。
  - [elisp - What is the correct way to join multiple path components into a single complete path in emacs lisp? - Stack Overflow](https://stackoverflow.com/questions/3964715/what-is-the-correct-way-to-join-multiple-path-components-into-a-single-complete/70721746#70721746)
- cf. [emacs-jp/migemo: emacs migemo client](https://github.com/emacs-jp/migemo)
