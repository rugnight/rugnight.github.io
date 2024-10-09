+++
title = "[UE C++]Tips"
date = "2024-10-03T17:57:39+09:00"
tags = ["UnrealEngine"]
+++

記事にするまでもない小さな諸々。
後々個別の記事にすることもある。

## メンバのオブジェクトはTObjectPtrの方が良い

SetupAttachmentなどのUSceneComponentが持っている関数を叩くことができるようになる。

```cpp

// × こちらではなく
UPROPERTY(BlueprintReadOnly, EditAnywhere, Category = "Camera") 
class USpringArmComponent* SpringArm;

// ○ こちらを使う
UPROPERTY(BlueprintReadOnly, EditAnywhere, Category = "Camera") 
TObjectPtr<class USpringArmComponent> SpringArm;
```

## AnimationBlueprintをデータパスから読み込む

```cpp
// 指定のアセットを探し
const ConstructorHelpers::FObjectFinder<UAnimBlueprint> AnimObj(TEXT("AnimBlueprint'/Game/Path/To/HogeAnimBP_Maw.HogeAnimBP_Maw'"));

// クラスを設定する
GetMesh()->SetAnimInstanceClass(AnimObj.Object->GeneratedClass);
```

- [How to set animation blueprint in c++](https://forums.unrealengine.com/t/how-to-set-animation-blueprint-in-c/302820/2)

## コーディング規約

- [コーディング規約](https://docs.unrealengine.com/4.27/ja/ProductionPipelines/DevelopmentSetup/CodingStandard/)

## アセット命名規則

- [Gamemakin UE4 スタイルガイド](https://github.com/akenatsu/ue4-style-guide/blob/master/README.jp.md)

## 命名参考

- [Dark Souls - ダークソウル英語表記まとめ](https://seesaawiki.jp/darksouls_en/)

## ヘッダーを調べる
