---
title: UE5 の Sparse Volume Texture の UV 座標の計算の仕方
---

Unreal Engine 5 の Sparse Volume Texture をつかって VDB のアセットから値を取り出すには、下のようなマテリアルグラフを作る。

<img width="1316" height="548" alt="image" src="https://github.com/user-attachments/assets/3f920b84-72b4-4338-a80e-6b433924fd71" />

Local Position から Object Local Bounds の Min を引いて、さらに Extents で割る。
この結果、0-1 の範囲の正規化された UV 座標（実際は 3 次元だけど）が出力されるらしい。

Engine Content に含まれる SparseVolumeMaterial に見本が含まれているが、これには Deprecated となった LocalPosition という別のノードが使われていたので、そこだけ新しいものに置き換えた。
