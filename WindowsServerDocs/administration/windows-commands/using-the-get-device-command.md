---
title: Get 장치 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 117720c5102da5713c1b0bb5e59cbcc099f3aa8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871034"
---
# <a name="using-the-get-device-command"></a>Get 장치 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사전 준비 된 컴퓨터 (즉, 물리적 컴퓨터를 active directory Domain Services에서 컴퓨터 계정으로 정렬 되었습니다에 대 한 Windows 배포 서비스 정보를 검색 합니다.
## <a name="syntax"></a>구문
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ 장치:<Device name>|(SAMAccountName) 컴퓨터의 이름을 지정합니다.|
|/ID:<MAC or UUID>|다음 예제에 표시 된 대로 MAC 주소 또는 컴퓨터의 UUID (GUID)를 지정 합니다. 유효한 GUID는 두 가지 중 하나에 있어야 하는 참고 이진 문자열이 나 GUID 문자열 형식<br /><br />-   **이진 문자열**: /ID:ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC 주소**: 00B056882FDC (대시 없음) 또는 (대시)와 00-B0-56-88-2F-DC<br />-   **GUID 문자열**: / id:e8a3efac-201F-4E69-953-B2DAA1E8B1B6|
|[/ 도메인:<Domain>]|사전 준비 된 컴퓨터에 대 한 검색할 도메인을 지정 합니다. 이 매개 변수의 기본값은 로컬 도메인입니다.|
|[포리스트 /: {예 &#124; No}]|Windows 배포 서비스 전체 포리스트 또는 로컬 도메인 검색 해야 하는지 여부를 지정 합니다. 기본값은 **No**, 로컬 도메인만을 검색할 의미 합니다.|
## <a name="BKMK_examples"></a>예제
컴퓨터 이름을 사용 하 여 정보를 가져오려면 다음을 입력 합니다.
```
wdsutil /Get-Device /Device:computer1
```
MAC 주소를 사용 하 여 정보를 가져오려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-Device /ID:"00-B0-56-88-2F-DC" /Domain:MyDomain
```
GUID 문자열을 사용 하 여 정보를 가져오려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[하위 명령: /set-device](subcommand-set-device.md)
[장치 추가 명령을 사용 하 여](using-the-add-device-command.md)
[get AllDevices 명령을 사용 하 여](using-the-get-alldevices-command.md)
