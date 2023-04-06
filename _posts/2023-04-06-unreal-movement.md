---
title: UE5 のプレイヤーキャラクターの方向コントロール
tags: ue5
---

プレイヤーキャラクターは Character クラスを継承して作る。

プレイヤーキャラクターの回転にはいくつかのパラメタが関連している。

Pawn クラスの User Controller Rotation Yaw はデフォルトで true だけど、ThirdPerson テンプレートでは false になっている。

![image](https://user-images.githubusercontent.com/65044/230344254-e99b3ee7-234d-48a6-81da-e0910b3c96de.png)

これが false のとき、入力に応じてキャラの Z 軸方向にキャラが回転する。
この回転の角速度は Character Movement コンポーネントで設定する。

![image](https://user-images.githubusercontent.com/65044/230344972-7af98582-b868-45dc-944c-423715d1101b.png)

Character Movement コンポーネントの Rotation Rate の Z の値が Z 軸回りの角速度となる。
ただし、Orient Rotation to Movement を true にしていないと、回転が発生しない。

- [APawn \| Unreal Engine Documentation](https://docs.unrealengine.com/5.1/en-US/API/Runtime/Engine/GameFramework/APawn/)
- [UCharacterMovementComponent \| Unreal Engine Documentation](https://docs.unrealengine.com/5.1/en-US/API/Runtime/Engine/GameFramework/UCharacterMovementComponent/)
