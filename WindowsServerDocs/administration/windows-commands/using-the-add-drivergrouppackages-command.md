---
title: 추가 DriverGroupPackages 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29022f53-ce14-4b2d-a81a-679c18e022b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad0f8c7ed202f0d6fccc11307b17b742c70c3e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842794"
---
# <a name="using-the-add-drivergrouppackages-command"></a>추가 DriverGroupPackages 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 명령을 사용 하는 방법을의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
## <a name="syntax"></a>구문
```
wdsutil /add-DriverGroupPackages /DriverGroup:<Group Name> [/Server:<Server Name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/DriverGroup:<Group Name>|드라이버 그룹의 이름을 지정합니다.|
|/Server:<Server name>|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/Filtertype:<Filter type>|드라이버 패키지에 대 한 검색의 특성을 지정 합니다. 단일 명령으로 여러 특성을 지정할 수 있습니다. 이 옵션에도 /Operator 및 /Value를 지정 해야 합니다.<br /><br /><Filter type> 다음 중 하나일 수 있습니다.<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/ 연산자: {같은 & #124; NotEqual & #124; GreaterOrEqual & #124; LessOrEqual & #124; (를) 포함|특성 값 사이의 관계를 지정합니다. 만 지정할 수 있습니다 **Contains** 문자열 특성입니다. 만 지정할 수 있습니다 **같은**, **NotEqual**, **GreaterOrEqual** 및 **LessOrEqual** 날짜 및 버전 특성이 있습니다.|
|/ 값입니다.<Value>|해당 하는 클라이언트 값 지정 **/Filtertype**합니다. 단일에 대 한 여러 값을 지정할 수 있습니다 **/Filtertype**합니다. 다음 목록은 각 필터에 대해 지정할 수 있는 값을 설명 합니다. 이러한 값에 대 한 자세한 내용은 참조 하세요. [드라이버 및 패키지 특성](https://go.microsoft.com/fwlink/?LinkId=166895) (https://go.microsoft.com/fwlink/?LinkId=166895)합니다.<br /><br />-PackageId-올바른 GUID를 지정 합니다. 예: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageName 지정 임의의 문자열 값입니다.<br />-PackageEnabled-지정 **예** 또는 **No**합니다.<br />-Packagedateadded-다음 형식으로 날짜를 지정 합니다. YYYY/MM/DD<br />-PackageInfFilename 지정 임의의 문자열 값입니다.<br />-PackageClass-올바른 클래스 이름 또는 클래스 GUID 지정합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **DiskDrive**, **Net**를 또는 {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-PackageProvider 지정 임의의 문자열 값입니다.<br />-PackageArchitecture-지정 **x86**, **x64**, 또는 **ia64**합니다.<br />-PackageLoale-유효한 언어 식별자를 지정 합니다. 예를 들어: **EN-US** 또는 **ES-ES**합니다.<br />-PackageSigned-지정 **예** 또는 **No**합니다.<br />-PackagedatePublished-다음 형식으로 날짜를 지정 합니다. YYYY/MM/DD<br />-다음 형식으로 버전을 지정 하는 Packageversion-: a.b.x.y. 예를 들어 다음과 같은 가치를 제공해야 합니다. 6.1.0.0<br />-Driverdescription 지정 임의의 문자열 값입니다.<br />-DriverManufacturer 지정 임의의 문자열 값입니다.<br />-DriverHardwareId-임의의 문자열 값을 지정 합니다.<br />-DrivercompatibleId-임의의 문자열 값을 지정 합니다.<br />-DriverExcludeId-임의의 문자열 값을 지정 합니다.<br />-DriverGroupId-올바른 GUID를 지정 합니다. 예: {4d36e972-e325-11ce-bfc1-08002be10318}.<br />-DriverGroupName 지정 임의의 문자열 값입니다.|
## <a name="BKMK_examples"></a>예제
드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:printerdrivers /Filtertype:PackageClass /Operator:Equal /Value:printer /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2
```
```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:DisplayDriversX86 /Filtertype:PackageClass /Operator:Equal /Value:Display /Filtertype:PackageArchitecture /Operator:Equal /Value:x86 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 DriverGroupPackage 명령을 사용 하 여](using-the-add-drivergrouppackage-command.md)
[추가 DriverPackage 명령을 사용 하 여](using-the-add-driverpackage-command.md)
[추가 AllDriverPackages 하위 명령 사용](using-the-add-alldriverpackages-subcommand.md)
