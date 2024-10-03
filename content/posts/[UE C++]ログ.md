+++
title = "[UE C++]ログ"
date = "2024-10-03T17:55:24+09:00"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++


## Blueprint PrintStringと同じログ表示

```cpp
#include "Kismet/KismetSystemLibrary.h"

UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Log!!")));
```
