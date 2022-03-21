---
title: UE4 で設定ファイルで設定できる変数を作る
tags: ue4
---

ビルドのバージョンを Blueprint の変数として取り出せるように、文字列の変数を Config Variable として作った。
この変数のデフォルト値は Config/DefaultEngine.ini で設定することができるので、ビルドスクリプトで自動的に値を埋め込むことができる。

![image](https://user-images.githubusercontent.com/65044/159197914-6a51a1e0-f61b-43a4-8c7d-d72f30e1136f.png)

しかしこうやって作った変数を実際に Blueprint で参照すると、なぜかいつも少しだけ古い値に上書きされてしまう。
UE4Editor のインスペクタ上では設定した値が表示されているのに、実際にゲームを走らせると違う値が設定される。
Saves や Intermediate フォルダを消しても古い値から更新されない。

![image](https://user-images.githubusercontent.com/65044/159198464-4cda569d-d081-474b-a3d0-6ef7e6e9cac4.png)

結果的に、[Get Class Defaults](https://docs.unrealengine.com/4.27/en-US/BlueprintAPI/Class/GetClassDefaults/) ノードを使って解決できた。
