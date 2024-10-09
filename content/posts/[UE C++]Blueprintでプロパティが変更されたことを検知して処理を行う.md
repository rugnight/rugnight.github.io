+++
title = "[UE C++]Blueprintでプロパティが変更されたことを検知して処理を行う"
date = "2024-10-07T13:05:36+09:00"
tags = ["UnrealEngine"]
hideComments = false
+++

```cpp
// --------------------------------------------------
// Header
// --------------------------------------------------

#if WITH_EDITOR
private:
 virtual void PostEditChangeProperty(struct FPropertyChangedEvent& PropertyChangedEvent) override;
#endif // WITH_EDITOR

// --------------------------------------------------
// CPP
// --------------------------------------------------
#if WITH_EDITOR
void AHoge::PostEditChangeProperty(struct FPropertyChangedEvent& PropertyChangedEvent)
{
 // 忘れると、親の変更が反映されないので注意
 Super::PostEditChangeProperty(PropertyChangedEvent);

 // クラス名とプロパティ名を取得し、比較して処理を行う
 FName PropertyName = (PropertyChangedEvent.Property != NULL) ? PropertyChangedEvent.Property->GetFName() : NAME_None;
 if (PropertyName == GET_MEMBER_NAME_CHECKED(ACBCharacter, CBCharacterUniqueDataAsset))
 {
  // 処理
 }
}
#endif // WITH_EDITOR

```

## 参考

[OnPropertyChanged or similiar, does it exist?](https://forums.unrealengine.com/t/onpropertychanged-or-similiar-does-it-exist/4679/2)
