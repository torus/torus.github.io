---
title: Skeleton Follower Component (SpineBoneFollower) の使い方
tag: ue4
---

[Skeleton Follower Component](http://en.esotericsoftware.com/spine-ue4#Skeleton-Follower-Component) というコンポーネントを使うと、
Spine のアニメーションに追随してゲーム内の他の物を動かしたりできる。
ただ、公式のドキュメントには具体的な設定方法が書いてなかったので、すこし補足します。

![image](https://user-images.githubusercontent.com/65044/176592012-37f93752-0910-4275-a7cd-29dfdd89b5d2.png)

SpineBoneFollower というコンポーネントを追加する。

![image](https://user-images.githubusercontent.com/65044/176592075-3f504b21-9bde-4226-8563-cda38d9c72fd.png)

Bone Name に追跡したいボーンの名前を指定する。
また、Use Component Transform をチェックする。

![image](https://user-images.githubusercontent.com/65044/176592304-348f363d-3195-4f3a-bf1b-70d60d78e71b.png)

BeginPlay などのイベントを使って、Target に Spine アニメーションを含むアクター自身を指定する。

![image](https://user-images.githubusercontent.com/65044/176592410-53982989-b905-49f4-8dad-d5115d5a5272.png)

追随したいコンポーネントを SpineBoneFollower の子に追加する。

実際の Spine ランタイムのコードでは次のように記述されている。
ここから分かるように、Target と UseComponentTransform の有無で動作が決まるようになっている。

```c++
void USpineBoneFollowerComponent::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) {
    Super::TickComponent(DeltaTime, TickType, ThisTickFunction);

    if (Target) {
        USpineSkeletonComponent *skeleton = static_cast<USpineSkeletonComponent *>(Target->GetComponentByClass(USpineSkeletonComponent::StaticClass()));
        if (skeleton) {
            FTransform transform = skeleton->GetBoneWorldTransform(BoneName);
            if (UseComponentTransform) {
                if (UsePosition) SetWorldLocation(transform.GetLocation());
                if (UseRotation) SetWorldRotation(transform.GetRotation());
                if (UseScale) SetWorldScale3D(transform.GetScale3D());
            } else {
                AActor *owner = GetOwner();
                if (owner) {
                    if (UsePosition) owner->SetActorLocation(transform.GetLocation());
                    if (UseRotation) owner->SetActorRotation(transform.GetRotation());
                    if (UseScale) owner->SetActorScale3D(transform.GetScale3D());
                }
            }
        }
    }
}
```
