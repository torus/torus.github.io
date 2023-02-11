---
title: UE5 で空の作り方
tag: ue5
---

案外簡単だった。

### 基本

- Directional Light を置く
- Engine Assets から BP_Sky_Sphare を探して置く
- BP_Sky_Sphare のプロパティの Directional Light Actor に上で置いた Directional Light を指定する

![BP_Sky_Sphare のプロパティ](https://user-images.githubusercontent.com/65044/218255004-8324957d-065e-4911-ac22-b27e297c1a46.png)

![空](https://user-images.githubusercontent.com/65044/218255046-9e25b93a-6a19-47c5-8072-440ce7d333cb.png)

### Sky Light

夕日がオブジェクトを照らすような効果がほしいときは Sky Light を置くといいみたい。

下の例は [POLYGON - Farm Pack](https://syntystore.com/products/polygon-farm-pack) のサンプルから。

#### Sky Light なし
![Sky Light なし](https://user-images.githubusercontent.com/65044/218255391-ab5c9148-6659-4486-9116-bc3be6eb38ed.png)

#### Sky Light あり
![Sky Light あり](https://user-images.githubusercontent.com/65044/218255397-dcfcaa3b-b617-40a0-9177-d9a79f31cd3d.png)
