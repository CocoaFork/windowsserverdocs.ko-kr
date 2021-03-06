---
title: 추가 AllDriverPackages 하위 명령 사용
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8290a95dd53718b200d10b6804d312abe95e257
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363894"
---
# <a name="using-the-add-alldriverpackages-subcommand"></a>추가 AllDriverPackages 하위 명령 사용



서버에 폴더에 저장 된 모든 드라이버 패키지를 추가 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

## <a name="parameters"></a>매개 변수

|          매개 변수           |                                                              설명                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  /FolderPath: \< 폴더 경로 >  |                      드라이버 패키지에 대 한.inf 파일이 있는 폴더의 전체 경로 지정 합니다.                      |
|   [/Server: \<Server name >]   | 서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다. |
|     [/아키텍처: {x86      |                                                                 ia64                                                                  |
| [/Drivergroup: \< 그룹 이름 >] |                             패키지를 추가할 드라이버 그룹의 이름을 지정 합니다.                             |

## <a name="BKMK_examples"></a>예와

드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers" /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers\Printers" /DriverGroup:"Printer Drivers"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)