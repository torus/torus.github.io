---
title: Sound Attenuation のリスナーを設定する
tags: ue5 ue4
---

[Sound Attenuation in Unreal Engine](https://docs.unrealengine.com/5.0/en-US/sound-attenuation-in-unreal-engine/)
を使うと、レベル上に音源を配置して空間オーディオを作ることができる。
このとき、デフォルトではカメラがリスナーとなるけど、プレイヤーキャラクターなどのアクターをリスナーにしたい場合は
[Set Audio Listener Attenuation Override](https://docs.unrealengine.com/5.0/en-US/BlueprintAPI/Game/Audio/SetAudioListenerAttenuationOverr-/)
を使う。

プレイヤーキャラクターをスポーンし、リスナーに設定する Blueprint は下のようになる：

![image](https://user-images.githubusercontent.com/65044/182007342-6e8ff2cf-feb5-48e5-bfcc-de0c6aff016f.png)
