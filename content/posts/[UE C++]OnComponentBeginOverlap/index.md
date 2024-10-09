---
title: "[UE C++]OnComponentBeginOverlap"
date: 2024-10-03T16:41:48+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

```cpp

// .h
// UFUNCTION() をつけないとコールされないので注意
UFUNCTION()
void OnOverlapBegin(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);

UFUNCTION()
void OnOverlapEnd(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);

// .cpp
AHoge::AHoge()
{
    // イベントを登録
    // AddDynamicはマクロなので補完されないので注意
    PrimitiveComponent->OnComponentBeginOverlap.AddDynamic(this, &ACBWeapon::OnOverlapBegin);
    PrimitiveComponent->OnComponentEndOverlap.AddDynamic(this, &ACBWeapon::OnOverlapEnd);

}

void ACBWeapon::OnOverlapBegin(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult)
{
}

void ACBWeapon::OnOverlapEnd(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex)
{
}

```
