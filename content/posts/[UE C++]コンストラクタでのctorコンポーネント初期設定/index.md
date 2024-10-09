---
title: "[UE C++]コンストラクタでのctorコンポーネント初期設定"
date: 2024-10-03T16:25:02+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

## Actor のクラスを指定して実行時に Spawn

```cpp

// .h
UPROPERTY(EditAnywhere, Category="Hoge")
TSubclassOf<class AHoge> HogeClass;

// .cpp
AHoge::AHoge()
{
    // デフォルト設定
    ConstructorHelpers::FClassFinder<AHoge> AssetFile(TEXT("/Game/path/to/BP_Hoge"));
    HogeClass = AssetFile.Class;
}

void AHoge::Spawn()
{
    FActorSpawnParameters SpawnParameters;
    Hoge = GetWorld()->SpawnActor<ACBHoge>(Hoge, FTransform(this->GetActorLocation()), SpawnParameters);
}

```

## 指定のオブジェクト

```cpp
UPROPERTY(EditDefaultsOnly)
TSoftObjectPtr<USkeletalMesh> CustomMeshA;

UPROPERTY(EditDefaultsOnly)
TSoftObjectPtr<USkeletalMesh> CustomMeshB;

USkeletalMesh* CustomMesh;
if(条件)
{
    CustomMesh = CustomMeshA.LoadSynchronous();
}
else
{
    CustomMesh = CustomMeshB.LoadSynchronous();
}

```

----

- [UnrealEngine マップやキャラクターの裏読み方法　～アセットロードのすすめ～ - Qiita](https://qiita.com/hoshiimonn/items/6f6528b06fc4314dbc97)
