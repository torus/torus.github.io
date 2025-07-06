---
title: UE5 の各種 Blueprint クラスの違い
---

#### Actor

- つよい
- キー入力イベントのハンドラはかけない
- Spawn Actor でスポーンする

#### Level Blueprint

- 他のレベルに使いまわせない

#### Actor Component

- だいたい何でもできるけど、コンポーネント内から親アクタに新しいコンポーネントを追加（Add * 関数）することができない
- Construction Script が作れない

#### Scene Component

- Actor Component とだいたい同じっぽいけど、エディタ上で階層構造を作れるので整理しやすい
- Owner の Actor に対する相対位置を持てる（位置が意味を持たないなら使わないほうがいいかも）

#### Object

- 明示的な破棄ができない代わりに GC される
- イベントディスパッチャも定義できる
- Delay などのランタイムの機能が使えない
- Construct でインスタンスを生成する


[Ello 2020-07-20T04:18:58.816Z - Torus Solutions 改](https://torus.github.io/2020/07/20/ello-21518769.html)
