---
title: UE5 でのローカリゼーション
tags: ue5
---

Localization Dashboard の使い方はここを見るのがわかりやすい（ありがとうございます）：
[UE4 ローカライゼーションダッシュボードを試してみる - Qiita](https://qiita.com/unknown_ds/items/c0f501ca9b72081ecb32)

ただしこのままではゲームをパッケージしたときに望んだ言語が表示されないことがある。

上のページで言及されているパッケージ設定に加えて、国際化サポートのデータセットを指定する必要がある。
![image](https://user-images.githubusercontent.com/65044/212789572-328ffbd4-0767-483a-a709-adb7a73ed351.png)

これについては [ローカライゼーションの概要 \| Unreal Engine ドキュメント](https://docs.unrealengine.com/4.27/ja/ProductionPipelines/Localization/Overview/) でも言及されている。

さらに、手元のコンピュータでローカライズをテストするときは、ビルドしたゲームにコマンドラインオプションでカルチャを指定する。
`-culture=<LANG>` のような形式で。
