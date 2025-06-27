---
title: UE5 で Blueprint から Visual Studio のデバッガを制御する
---

Blueprint のブレークポイントでプレイ中のゲームを止めても Unreal Engine 自体は動いているので、そのままでは Visual Studio のデバッガで詳細を見られない。
その場合は、ゲームのほかの部分で使っていない Blueprint のノードをつなげて、そのノードが実行する C++ コードにブレークポイントを仕込めばいいらしい。

今回は Draw Debug Circle を使った。Blueprint から下のように呼び出す。
実際にちゃんと呼び出せているか確認するために具体的な座標などを設定して画面でも確認できるようにした。

![image](https://github.com/user-attachments/assets/5914b6c3-8e6b-4b70-bb32-ff172f99b077)

Visual Studio で DrawDebugCircle の実装部分を探してブレークポイントを設定する。

![image](https://github.com/user-attachments/assets/b0504030-a50b-4306-aeeb-b7ee4101353e)

これでうまくデバッガで捕捉することができた。

![image](https://github.com/user-attachments/assets/cfffc058-6484-4642-8c28-fb8c919bd1c4)
