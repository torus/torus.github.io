---
title: UE4 Blueprint の Delay ノードの不確実性
tags: ue4
---

![image](https://user-images.githubusercontent.com/65044/158941619-b1446f9f-daf9-4549-9b47-c8746ef6116a.png)

UE4 の Blueprint で
[Delay](https://docs.unrealengine.com/4.27/en-US/BlueprintAPI/Utilities/FlowControl/Delay/)
を使うと指定した時間経った後で動作を再開することができるんだけど、
どうやらこれはあまり厳密に時間を計測していないらしい。
FPS が 60-100 くらいのときはほぼ正確に指定した時間通りに動くけど、FPS が 40 くらいまで落ちると 0.1 秒が 120 ミリ秒くらいかかる。

下は計測に使用した Blueprint: [measuring the actual delay posted by tor | blueprintUE | PasteBin For Unreal Engine 4](https://blueprintue.com/blueprint/-fb2z-23/)
<iframe src="https://blueprintue.com/render/-fb2z-23/" scrolling="no" allowfullscreen></iframe>
