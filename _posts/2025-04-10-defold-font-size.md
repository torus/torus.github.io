---
title: Defold でエディタのフォントサイズを大きくする方法
---

ホームディレクトリに `.defold/editor.css` というファイルを作り、下のように書く。

```css
.root {
    -fx-font-size: 20px;
}
```

Defold の Discord で見つけた。

![image](https://github.com/user-attachments/assets/89b99825-3956-44df-9ae9-69b1394531b4)

https://github.com/defold/defold/blob/eebdb359378aeab5b865fe2b0c51e72e313a5956/editor/src/clj/editor/ui.clj#L641
ソースはこのへん。

```clojure
(defn- apply-default-css! [^Parent root]
  (.. root getStylesheets (add (str (io/resource "editor.css"))))
  nil)
```
