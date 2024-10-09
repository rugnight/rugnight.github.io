---
title: "[UE C++]GetComponents"
date: 2024-10-03T15:57:05+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

```cpp
// コリジョンコンポーネントを収集する
void AHoge::CollectCollisions()
{
 AttackCollisionArray.Empty();

 // コンポーネント取得
 TArray<UPrimitiveComponent*> PrimitiveComponent;
 this->GetComponents(UPrimitiveComponent::StaticClass(), PrimitiveComponent);

 for (int i = 0; i < PrimitiveComponent.Num(); ++i)
 {
  AttackCollisionArray.Add(PrimitiveComponent[i]);
 }
}
```
