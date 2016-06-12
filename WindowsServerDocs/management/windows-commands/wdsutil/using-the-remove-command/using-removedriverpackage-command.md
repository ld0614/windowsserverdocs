---
title: Using the remove-DriverPackage Command
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
---
# Using the remove-DriverPackage Command
removes a driver package from a server.

## Syntax

```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|\[\/Server:<Server name>\]|Specifies the name of the server. This can be the NetBIOS name or the FQDN. if a server name is not specified, the local server is used.|
|\[\/DriverPackage:<Name>\]|Specifies the name of the driver package to remove.|
|\[\/PackageId:<ID>\]|Specifies the Windows deployment Services ID of the driver package to remove. You must specify the ID if the driver package cannot be uniquely identified by name.|

## <a name="BKMK_examples"></a>Examples
To view information about the images, type one of the following:

```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```

```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```

#### additional references
[Command-Line Syntax Key](../../commandline-syntax-key.md)

[Using the remove-DriverPackages Command](using-removedriverpackages-command.md)

