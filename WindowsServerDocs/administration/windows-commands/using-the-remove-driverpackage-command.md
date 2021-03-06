---
title: 제거 DriverPackage 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 923a86805134c4162b36cdade98c2122b3cb7ccd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362812"
---
# <a name="using-the-remove-driverpackage-command"></a>제거 DriverPackage 명령을 사용 하 여

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 드라이버 패키지를 제거 합니다.
## <a name="syntax"></a>구문
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                            설명                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:<Server name>] |              서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.              |
| [/ DriverPackage:<Name>] |                                                        제거할 드라이버 패키지의 이름을 지정 합니다.                                                         |
|    [/ 패키지 Id:<ID>]    | 제거할 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우에 ID를 지정 해야 합니다. |

## <a name="BKMK_examples"></a>예와
이미지에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[제거 DriverPackages 명령을 사용 하 여](using-the-remove-driverpackages-command.md)
