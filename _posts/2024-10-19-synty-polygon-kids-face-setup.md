---
title: Unreal Engine で Synty POLYGON Kids Pack を使うときの顔のセットアップ
---

Synty の [POLYGON Kids Pack](https://syntystore.com/products/polygon-kids-pack?_pos=1&_psq=kid&_ss=e&_v=1.0) にはたくさんの種類の服装をした子どものキャラクターが含まれている。
しかし、それらのスケルタルメッシュには顔がついてないので、眉、目、そばかすをアタッチする必要がある。

### 眉や目のアタッチ

Kids Pack にもサンプルとしてキャラクターのプリセット Blueprint がいくつか含まれているのでそれを参考にする。

![image](https://github.com/user-attachments/assets/e60be7b5-698a-4822-94e3-3a7f24bc5fdc)

まず上のように眉と目のスケルタルメッシュを本体のスケルタルメッシュにアタッチする。

次に Construction Script を編集して、下のように眉と目に対して Set Leader Pose Component で本体のスケルタルメッシュを設定する。
これにより、目と眉が本体に追随して動くようになるので、アニメーションのリターゲティングをする必要はない。

![image](https://github.com/user-attachments/assets/91ba3bc9-30c7-48b0-a174-b43f088c20c8)

### レンダリングの設定

しかしこのままだとなぜか下のように目と眉が消えるという問題が発生する。

![umi-lennie-no-eyes](https://github.com/user-attachments/assets/dd34f933-1d01-4ec2-a54e-b89dbd8980fc)

よくみるとこれはスケルタルメッシュがまるごとカリングされているように見える。

やり方として正しいかはわからないけど、下のように「Render CustomDepth Pass」を true に設定すると直った。

![Screenshot from 2024-10-19 18-42-11](https://github.com/user-attachments/assets/df65a165-9d83-40af-aede-31476e8d568e)

![umi-lennie-eyes-fixed](https://github.com/user-attachments/assets/6ddce07c-7ebd-4f9f-b9e3-78a6897acb7a)
