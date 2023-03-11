---
title: パスワードを生成するワンライナー
---

iOS のパスワードジェネレータ風のパスワードを作る JavaScript のワンライナー。
アルファベットの大文字と小文字および数字 18 文字のランダムな文字列を 6 文字ずつに区切って `-` でつなぐ。

```
String.fromCharCode.apply(null, Array.from(Array(18)).map(x => Math.random() * (10 + 26 * 2) | 0).map(n => n < 10 ? '0'.charCodeAt(0) + n : n < 36 ? 'A'.charCodeAt(0) + n - 10 : 'a'.charCodeAt(0) + n - 36)).split(/(:?.{6})/).filter(x => x.length > 0).join('-')
```

改行あり：

```javascript
String.fromCharCode.apply(null, Array.from(Array(18))
    .map(x => Math.random() * (10 + 26 * 2) | 0)
    .map(n => n < 10 ? '0'.charCodeAt(0) + n
            : n < 36 ? 'A'.charCodeAt(0) + n - 10
            : 'a'.charCodeAt(0) + n - 36))
  .split(/(:?.{6})/)
  .filter(x => x.length > 0)
  .join('-')
```
