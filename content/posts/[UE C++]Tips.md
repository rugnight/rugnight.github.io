+++
title = "[UE C++]Tips"
date = "2024-10-03T17:57:39+09:00"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["UnrealEngine"]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++

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

[How to set animation blueprint in c++](https://forums.unrealengine.com/t/how-to-set-animation-blueprint-in-c/302820/2)
