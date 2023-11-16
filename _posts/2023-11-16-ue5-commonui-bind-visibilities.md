---
title: "UE5: Common UI の Set Bind Visibilities の使い方"
tags: [ue5, unreal]
---

Unreal Engine の [Content Examples in UE Feature Samples - UE Marketplace](https://www.unrealengine.com/marketplace/en-US/product/content-examples)
に含まれる Common UI のサンプルで、下のような Blueprint がある。

![Screenshot from 2023-11-16 11-25-29](https://github.com/torus/torus.github.io/assets/65044/fa686e36-3328-42d7-97e1-bc37b4f828de)

これは最初見たとき意味がわからなかったけど、
[Bind Visibility to Activation](https://docs.unrealengine.com/5.2/en-US/BlueprintAPI/ActivatableWidget/BindVisibilitytoActivation/)
を読んでやっと意図がわかった。

> Bind our visibility to the activation of another widget, useful for making mouse collisions behave similiar to console navigation w.r.t activation Will immediately update visibility based on the bound widget activation & visibilites set by SetBindVisibilities.

つまり、別のウィジェットがアクティブになったら self のビジビリティをそれに応じて変えろということことらしい。

![image](https://github.com/torus/torus.github.io/assets/65044/c47e299c-6d35-4c1e-91c8-00443a5f07c7)

上のように手前のポップアップがアクティブな間は、その奥のウィジェット（ここでは self）は「見えるけどカーソルに反応しない (Not Hit-Testable)」にしろという指定だった。
cf. [HitTestInvisible \| Unreal Engine 5.2 Documentation](https://docs.unrealengine.com/5.3/en-US/API/Runtime/SlateCore/Layout/EVisibility/HitTestInvisible/)
