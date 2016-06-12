---
title: bitsadmin gettype
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
---
# bitsadmin gettype
Retrieves the job type of the specified job.

## Syntax

```
bitsadmin /gettype <Job>
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|Job|The job's display name or GUID|

## remarks
The type can be DOWNLOAD, UPLOAD, UPLOAD\-REPLY, or UNKNOWN.

## <a name="BKMK_examples"></a>Examples
The following example retrieves the job type for the job named *myDownloadJob*.

```
C:\>bitsadmin /gettype myDownloadJob
```

## additional references
[Command-Line Syntax Key](../commandline-syntax-key.md)

