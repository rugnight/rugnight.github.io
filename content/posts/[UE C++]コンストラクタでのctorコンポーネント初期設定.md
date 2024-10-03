---
title: "[UE C++]コンストラクタでのctorコンポーネント初期設定"
date: 2024-10-03T16:25:02+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

## Actorのクラスを指定して実行時にSpawn

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
