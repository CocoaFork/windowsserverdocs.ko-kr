---
title: 추가 DriverPackage 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f5370d301f5fec15f4812b3d65588297d179455d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363746"
---
# <a name="using-the-add-driverpackage-command"></a>추가 DriverPackage 명령을 사용 하 여



서버에 드라이버 패키지를 추가합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

## <a name="parameters"></a>매개 변수

|          매개 변수           |                                                              설명                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile: \<Inf 파일 경로 >   |                                           추가할.inf 파일의 전체 경로 지정 합니다.                                            |
|    /Server: \<Server name >    | 서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다. |
|      /아키텍처: {x86      |                                                                 ia64                                                                  |
| [/Drivergroup: \< 그룹 이름 >] |                             패키지를 추가할 드라이버 그룹의 이름을 지정 합니다.                              |
|   [/Name: \<Friendly 한 이름 >]   |                                           드라이버 패키지에 대 한 이름을 알려 줍니다.                                            |

## <a name="BKMK_examples"></a>예와

드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:"C:\Temp\Display.inf"
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:"C:\Temp\Display.inf" /Architecture:x86 /DriverGroup:x86Drivers /Name:"Display Driver"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

