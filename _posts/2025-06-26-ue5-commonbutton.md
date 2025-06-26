---
title: UE5.4 から 5.6 に移行するときに Common Button Base のボタンが機能しなくなった時の確認事項
---

UE 5.4 で制作したプロジェクトを UE 5.6 に移行したときに、それまでは動作していた Common Button Base ベースのボタンが動かなくなった。
具体的には、マウスやゲームパッドには反応するけど、キーボードには反応しなくなった。
[Common UI Quickstart Guide for Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/common-ui-quickstart-guide-for-unreal-engine)
を読み返して設定項目を確認したが、とくに間違った設定はしていなかった。
Common Input Settings > Input Data などに設定されているデータテーブルも念のためすべて確認した。

エンジン側のバグということもあり得るので、それを確認するためにまず
[Content Examples Sample Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine)
をダウンロードして中身を見てみた。
これに含まれる CommonUI のサンプルは正常に動作していた。
しかし残念ながら、このサンプルには Common Button Base を使ったボタンは含まれていなかった。

次に UE 5.6 で新しくプロジェクトを作成し、Common Button Base を使った最小限の機能を作ってみた。
すると何の問題もなく動いた。
この時点で少なくともエンジンのバグではないことが分かったので少し安心した。

実際に動作するプロジェクトを眺めていると、見慣れない設定項目があることに気が付いた。
Project Settings > Plugins > Common UI Framework > Button > Common Button Accept Key Handling
の値が、新規プロジェクトでは TriggerClick だったのに対して、5.4 から移行したプロジェクトでは Ignore になっていた。

![image](https://github.com/user-attachments/assets/843def89-3c9f-4043-9eab-1c9ce6a437e3)

既存のプロジェクトでもこの値を TriggerClick に変更してみたら、これまで通り Common Button Base ベースのボタンが動作するようになった。

この変更によって Config/DefaultGame.ini に下のような項目が追加されていた。

```diff
index dc1a8b6d4..a2220f15d 100644
--- a/Umi/Config/DefaultGame.ini
+++ b/Umi/Config/DefaultGame.ini
@@ -112,3 +112,6 @@ bSkipMovies=False
 bRetainStagedDirectory=False
 CustomStageCopyHandler=

+[/Script/CommonUI.CommonUISettings]
+CommonButtonAcceptKeyHandling=TriggerClick
+
```

Common Button Base はとても便利だけどいまだに公式のドキュメントが整備されていないので、こういう非互換な変更があるとちょっと悩む。
