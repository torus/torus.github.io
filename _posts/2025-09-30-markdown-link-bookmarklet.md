---
title: Markdown のリンクを作る Bookmarklet 2025 年版
---
ブラウザのブックマークバーを右クリックして新しいページを追加する。

<img width="694" height="749" alt="image" src="https://github.com/user-attachments/assets/751067bd-5dd8-4477-818f-f9c4d8bc8456" />

URL 欄には次のように書く：
```
javascript:((d,l)=>prompt(`${d.title}`, `[${d.title.replaceAll(/([\[\]])/g, (matched, c1, index, input)=>`\\${c1}`)}](${l.href})`))(document,location)
```

JavaScript の replaceAll で引数に手続きをとれることを知ったので、タイトル中の `[]` を `\` でエスケープするようにしてみた。
[javascript - How to replace captured groups only? - Stack Overflow](https://stackoverflow.com/questions/3954927/how-to-replace-captured-groups-only#3954957)
