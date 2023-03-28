---
title: UE5 でパラパラマンガ
---

- 連番の画像ファイルを用意する。
- ImageMagick の [Montage](https://legacy.imagemagick.org/Usage/montage/) を使ってスプライトシート画像を作る。
- スプライトシート画像を UE5 にインポートする。
- 新規にマテリアルを作る。
- Flipbook 関数を使う。
cf. [Render a Flipbook Animation \| Unreal Engine 4.27 Documentation](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/RenderToTextureTools/5/)
- Animation Phase には Time をつなぐ。
cf. [Constant Material Expressions in Unreal Engine \| Unreal Engine 5.1 Documentation](https://docs.unrealengine.com/5.1/en-US/constant-material-expressions-in-unreal-engine/)

例えば全体を 5 秒で再生したい場合は、Time の Period に 5.0 を指定し、その出力を 5.0 で割る。
すると 5 秒かけて 0 から 1 まで上昇する出力が得られる。
