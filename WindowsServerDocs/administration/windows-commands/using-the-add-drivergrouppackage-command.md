---
title: 추가 DriverGroupPackage 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb443b6e6fdc71ccd3340552a23491ef7e61e0b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363810"
---
# <a name="using-the-add-drivergrouppackage-command"></a>추가 DriverGroupPackage 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이버 그룹에 드라이버 패키지를 추가 합니다.
## <a name="syntax"></a>구문
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>매개 변수

|         매개 변수         |                                                                                                                                               설명                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup: <Group Name> |                                                                                                                                 드라이버 그룹의 이름을 지정합니다.                                                                                                                                 |
|   /Server: <Server name>   |                                                                                  서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.                                                                                  |
|   /DriverPackage: <Name>   |                                                                      그룹에 추가할 드라이버 패키지의 이름을 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우이 옵션을 지정 해야 합니다.                                                                       |
|      /PackageId: <ID>      | 패키지에 대 한 ID를 지정합니다. 패키지 ID를 찾으려면 패키지가 드라이버 그룹을 클릭 합니다 (또는 **모든 패키지** 노드)에서 패키지를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다. 패키지 ID는 **일반** 탭에 표시 됩니다 (예: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}** ). |

## <a name="BKMK_examples"></a>예와
드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 DriverGroupPackages 명령을 사용 하 여](using-the-add-drivergrouppackages-command.md)
[추가 DriverPackage 명령을 사용 하 여](using-the-add-driverpackage-command.md)
[추가 AllDriverPackages 하위 명령 사용](using-the-add-alldriverpackages-subcommand.md)
