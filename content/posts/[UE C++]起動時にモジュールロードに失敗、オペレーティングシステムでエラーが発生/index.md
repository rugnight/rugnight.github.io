+++
title = "[UE C++]起動時にモジュールロードに失敗、オペレーティングシステムでエラーが発生"
date = "2024-10-08T17:24:03+09:00"
tags = ["UnrealEngine"]
+++

## 2024-10-09 追記

僕の場合の原因が判明した。
MotionWarpingの機能を追加してコードを書いていたのだが、C++とBuild.csの方はGitへコミットしていたにも関わらずエディタ側のPlugin有効化設定をGitにコミットし忘れていたのが原因。
設定に矛盾ができてしまい、エンジン側はONにしていないはずの機能がC++側で使用されており起動不能になっていたようだ。

----

## 現象

このような文言が表示されてプロジェクトの起動ができない状態に陥った。

> ゲームモジュール「Hoge」をロードできませんでした。オペレーティングシステムでエラーが発生。モジュールが正しくセットアップされていない、あるいはビルドに含まれているプラグインが有効ではない可能性があります。
![](2024-10-08-17-25-49.png)

## 対処

半日近く以下の対応を繰り返し最終的にQuixelBridgeの再インストールを実施してリビルドを行ったタイミングで起動に成功した。
正直最後の対応が効いたような気はしないが、記録として残しておく。

- エンジン再インストール
- VisualStudioの復元
- sln再生成してリビルド
- QuixelBridgeの再インストール  
    ※プロジェクトで使用しており、ちょうどアップデートが入ったタイミングだったので怪しんだ

英語ではこのような文言らしい。

> The game module ‘ProjectName’ could not be loaded. There may be an operating system error or the module may not be properly set up.”

----

- [The game module 'X' could not be loaded. There may be an operating system error](https://stackoverflow.com/questions/77348549/the-game-module-x-could-not-be-loaded-there-may-be-an-operating-system-error)

- [UE4・UE5でC＋＋のプロジェクトが開けなくて困っている皆様へ｜magumac（まぐまく・マグマック）](https://note.com/world_of_magumac/n/n5e7578050119)

- [Unable to load Module](https://forums.unrealengine.com/t/unable-to-load-module/330343)
