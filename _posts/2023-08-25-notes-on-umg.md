---
title: UE5 の UMG ウィジェットについての注意
---

UMG のウィジェットクラスを作るときの注意点。

### 導出クラスの Tick イベント

導出クラスでは親クラスの Tick がデフォルトで呼ばれない。
もともと半透明の形でグラフエディタ上にいる Tick イベントのノードを、下のように実体化すると呼ばれるようになる。

![image](https://github.com/torus/torus.github.io/assets/65044/1134e894-b9de-4fa7-bb79-7eed375cbc58)

Construct や PreConstruct イベントはデフォルトで親クラスのイベントが呼ばれるようので紛らわしい。

### Construct と PreConstruct のタイミング

Construct と PreConstruct は 1 つのインスタンスに対して 2 回以上呼ばれることがある。
これはドキュメントにも書いてあった。

> Called after the underlying slate widget is constructed. Depending on how the slate object is used this event may be called multiple times due to adding and removing from the hierarchy. If you need a true called-once-when-created event, use OnInitialized.
> 
> -- [UUserWidget::Construct \| Unreal Engine 5.2 Documentation](https://docs.unrealengine.com/52/en-US/API/Runtime/UMG/Blueprint/UUserWidget/Construct/) より。

また、PreConstruct はエディタで呼ばれることがあるので、気をつけないとエディタのクラッシュに結びつくことがある。

> WARNING This is intended purely for cosmetic updates using locally owned data, you can not safely access any game related state, if you call something that doesn't expect to be run at editor time, you may crash the editor.
> 
> -- [UUserWidget::PreConstruct \| Unreal Engine 5.2 Documentation](https://docs.unrealengine.com/5.2/en-US/API/Runtime/UMG/Blueprint/UUserWidget/PreConstruct/) より。

一度だけ呼び出される処理を実装するには [OnInitialized](https://docs.unrealengine.com/5.2/en-US/API/Runtime/UMG/Blueprint/UUserWidget/OnInitialized/) を使う。
