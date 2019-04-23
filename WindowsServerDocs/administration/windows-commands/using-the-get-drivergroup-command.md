---
title: Get DriverGroup 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f82969e03b3474cf39afd2ae5c3ef2f9d4f8b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847154"
---
# <a name="using-the-get-drivergroup-command"></a>Get DriverGroup 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에 드라이버 그룹에 대 한 정보를 표시합니다.
## <a name="syntax"></a>구문
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/DriverGroup:<Group Name>|드라이버 그룹의 이름을 지정합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다.  서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[표시 /: {PackageMetaData & #124; #124; 및 필터 모든}]|지정된 된 그룹의 모든 드라이버 패키지에 대 한 메타 데이터를 표시합니다. **PackageMetaData** 드라이버 그룹에 대 한 모든 필터에 대 한 정보를 표시 합니다. **필터** 모든 드라이버 패키지에 대 한 메타 데이터 및 그룹에 대 한 필터를 표시 합니다.|
## <a name="BKMK_examples"></a>예제
드라이버 파일에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[get AllDriverGroups 명령을 사용 하 여](using-the-get-alldrivergroups-command.md)
