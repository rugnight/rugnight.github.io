---
title: "[UE C++]Error Unable to Build While Live Coding Is Active. Exit the Editor and Game"
date: 2024-10-09T11:42:51+09:00
categories: []
tags: ["UnrealEngine"]
thumbnail: ""
---

## 症状

以下のようなエラーが発生し、VisualStudio上からのビルドが失敗する。

> Error Unable to build while Live Coding is active. Exit the editor and game, or press Ctrl+Alt+F11 if iterating on code in the editor or game

> "HogeHoge\Build\BatchFiles\Build.bat -Target="UnrealEditor Win64 Development" -Target="ShaderCompileWorker Win64 Development -Quiet" -WaitMutex -FromMsBuild" はコード 6 で終了しました。 UE5 C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.MakeFile.Targets 44

## 対応

以下のディレクトを削除して再ビルド。

- Binaries
- DerivedDataCache

----

- [In UE 5 I keep getting this error Unable to build while Live Coding is active](https://stackoverflow.com/questions/72396354/in-ue-5-i-keep-getting-this-error-unable-to-build-while-live-coding-is-active)
