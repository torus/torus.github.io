---
title: Synty のキャラを UE5 で使うための設定
tags: ue5
---

[UE5 - Synty Retarget to IK Mannequin \| Epic Developer Community](https://dev.epicgames.com/community/learning/tutorials/l0Kz/ue5-synty-retarget-to-ik-mannequin)

### キャラクター

- Third Person テンプレートに Synty パックをインストールする
- Third Person キャラクターを開き、必要ならメッシュを Manny に変える
- 子供のスケルトンメッシュを追加
- メッシュにビジネスマンスーツを指定
- 元のメッシュは Visible を false に設定して見えなくする
- Visibility Based Anim Tick Option を Always Tick Pose and Refresh Bones に設定する

### IK リグ

- IK_Mannequin をコピーして IKRig_Synty にリネーム
- 右クリック、Asset Actions → Bulk Edit via Property Matrix... を選ぶ
- Imported Skeleton → Preview Skeletal Mesh に SK_Character_BusinessMan_Shirt を設定する
- IKRig_Synty を開く
- 右の IK Retargeting タブを開く
- 左右の手の指のボーンを変更する
  - 左右の Pinky、Ring、Middle について End Bone を finger_04_l(r)
  - Index は indexFinger_01_l(r) - indexFinger_04_l(r)

### IK リターゲター

- Animation → IK Retargeter を新規作成し IK Rig To Copy Animation From に IK_Mannequin を選ぶ
  - IKRetargeter_Synty と名付ける
- Target IKRig Asset に IKRig_Synty を選ぶ
- Edit Pose を選ぶ
- 肩の関節を 50° 動かす
- 肘の関節を 40° 動かす
- アニメーションを確認するときは Edit Pose をキャンセルする

### Animation Blueprint

- Animation Blueprint を新規作成し Skeleton に SK_Character_City_Rig を選び ABP_Synty と名付ける
- Retarget Pose From Mesh を選び、Output Pose につなぐ
  - IKRetargeter Asset に IKRetargeter_Synty を選ぶ

### キャラクター

- キャラクター Blueprint を選び、CharacterMesh の Anim Class に ABP_Synty を選ぶ
- 完成！
