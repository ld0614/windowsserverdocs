---
title: convert dynamic
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-storage
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
---
# convert dynamic
converts a basic disk into a dynamic disk.

for instructions regarding how to use this command, see [change a Basic Disk into a Dynamic Disk](http://go.microsoft.com/fwlink/?LinkId=207047) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=207047\).

## Syntax

```
convert dynamic [noerr]
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|noerr|for scripting only. When an error is encountered, DiskPart continues to process commands as if the error did not occur. Without this parameter, an error causes DiskPart to exit with an error code.|

## remarks

-   Any existing partitions on the basic disk become simple volumes.

-   A basic disk must be selected for this operation to succeed. Use the **select disk** command to select a basic disk and shift the focus to it.

## <a name="BKMK_examples"></a>Examples
To convert a basic disk into a dynamic disk, type:

```
convert dynamic
```

#### additional references
[Command-Line Syntax Key](../commandline-syntax-key.md)

[Diskpart \[LH\]](assetId:///26a4a166-95fa-4faf-95bc-2d5345f4a57a)

