+++
title = "[UE C++]DataAsset"
date = "2024-10-04T11:04:58+09:00"
tags = ["UnrealEngine", ]
+++

## 基本的な DataAsset の使用例

Web の記事を見ると DataTable や AssetManager を交えた別知識も必要な応用例が多いので、DataAsset を作って読み込むだけという基本的な方法を残しておく。

1. UDataAsset を継承してデータ型を作る

   ```cpp:UCharacterDataAsset.h
   UCLASS()
   class UE_HOGE_API UCharacterDataAsset : public UDataAsset
   {
       GENERATED_BODY()

   public:
       // 無敵時間
       UPROPERTY(EditAnywhere, Category="Damage")
       float DamagedInvulnerableDuration = 0.5f;
   };
   ```

1. 作成した型（UCharacterDataAsset）を継承して BP を作成する
   仮に、BP_CharacterDataAsset とする
1. 使用するクラスで参照する
   今回は BP から DataAsset を指定できる状態にして、初期値として先ほど作成したアセットを設定しておく。

   ```cpp:Character.cpp

   // --------------------------------------------------
   // header
   // --------------------------------------------------
   UPROPERTY(EditAnywhere, Category="DataAsset")
   TSoftObjectPtr<class UCharacterDataAsset> CharacterDataAsset;

   // --------------------------------------------------
   // cpp
   // --------------------------------------------------
   ACharacter::ACharacter()
   {
       // 作成したBP_CharacterDataAssetをデフォルトの値として設定
       static ConstructorHelpers::FObjectFinder<UCharacterDataAsset> CharacterDataAssetFinder(TEXT("CharacterDataAsset'/Game/DataAsset/BP_CharacterDataAsset.BP_CharacterDataAsset'"));
       if (ConstructorHelpers.Succeeded())
       {
           CharacterDataAsset = ConstructorHelpers.Object;
       }
   }

   void ACharacter::BeginPlay()
   {
       // 実データ読み込み
       CharacterDataAsset.LoadSynchronous();
   }

   void ACharacter::Hoge()
   {
       // データアクセス
       float value = CharacterDataAsset->DamagedInvulnerableDuration;
   }
   ```

---

[Unreal Engine の開発が楽になる便利機能を紹介 DataAsset, Subsystem, GameplayAbility 編 ](https://www.docswell.com/s/EpicGamesJapan/KXVDY5-2022-08-02-124838#p4)

1. PrimaryDataAsset を親クラスとして BP を作成
   保存するものと処理を担当
1.

```

```


