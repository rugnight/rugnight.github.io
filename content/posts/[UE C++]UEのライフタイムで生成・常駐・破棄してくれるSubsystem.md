+++
title = "[UE C++]UEのライフタイムで生成・常駐・破棄してくれるSubsystem"
date = "2024-10-03T17:39:42+09:00"
tags = ["UnrealEngine"]
+++

## GameInstanceSubsystem

ゲームの開始と終了にあわせて生成・破棄される。

コード例は Tick 処理を実装するために、FTickableGameObject を継承している。

```cpp
#pragma once

#include "Tickable.h"
#include "CoreMinimal.h"
#include "Subsystems/GameInstanceSubsystem.h"
#include "CBDebugGuiSubsystem.generated.h"

UCLASS()
class UE_SP_SHADERTEMP_API UCBDebugGuiSubsystem
    : public UGameInstanceSubsystem
    , public FTickableGameObject
{
 GENERATED_BODY()

public:
 // ==================================================
 // For UGameInstanceSubsystem
 // ==================================================
 virtual void Initialize(FSubsystemCollectionBase& Collection);

 virtual void Deinitialize();

 // ==================================================
 // For FTickableGameObject
 // ==================================================

 // 初期化の完了を待ってTickを動かすようにしないと初期数フレームで重複してTickが呼ばれてしまうのに対処
 virtual bool IsTickable() const override { return bIsInitialized; }

 virtual TStatId GetStatId() const override;

 virtual void Tick(float DeltaTime) override;

private:
 bool bIsInitialized = false;
};
```

```cpp
// Fill out your copyright notice in the Description page of Project Settings.
#include "CBDebugGuiSubsystem.h"
#include "Kismet/GameplayStatics.h"
#include "GameFramework/DamageType.h"

void UCBDebugGuiSubsystem::Initialize(FSubsystemCollectionBase& Collection)
{
 UE_LOG(LogTemp, Log, TEXT("UCBDebugGuiSubsystem::Initialize()"));

 Super::Initialize(Collection);
 bIsInitialized = true;
}

void UCBDebugGuiSubsystem::Deinitialize()
{
 UE_LOG(LogTemp, Log, TEXT("UCBDebugGuiSubsystem::Deinitialize()"));

 Super::Deinitialize();
 bIsInitialized = false;
}

// ==================================================
// For FTickableGameObject
// ==================================================
TStatId UCBDebugGuiSubsystem::GetStatId() const
{
 RETURN_QUICK_DECLARE_CYCLE_STAT(UCBDebugGuiSubsystem, STATGROUP_Tickables);
}

void UCBDebugGuiSubsystem::Tick(float DeltaTime)
{
}
```

---

[UE4 プログラミングサブシステムを試してみる](https://qiita.com/unknown_ds/items/afcff802ab17db486822)

