---
title: "[UE C++]AssetManager管理のアセットをFPrimaryAssetIdで同期ロードする"
date: 2024-10-11T19:06:27+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

## 方法

```cpp
// アセットID
FPrimaryAssetId AssetId = FPrimaryAssetId(FName("HogeAssetType"), FName("HogeAssetName"));

// AssetManager取得
UAssetManager* AssetManager = UAssetManager::Get();

// 同期ロード
UObject* Asset = AssetManager.GetPrimaryAssetObject(AssetId);
```
