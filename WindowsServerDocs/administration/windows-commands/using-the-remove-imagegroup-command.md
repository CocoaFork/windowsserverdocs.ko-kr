---
title: 제거 ImageGroup 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df6af7fbd19cc95dfbffa0a5c0e2a4b3e33fb82c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877894"
---
# <a name="using-the-remove-imagegroup-command"></a>제거 ImageGroup 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 이미지 그룹을 제거합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup:<Image group name>|제거할 이미지 그룹의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예제
이미지 그룹을 제거 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer 
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 ImageGroup 명령을 사용 하 여](using-the-add-imagegroup-command.md)
[get AllImageGroups 명령을 사용 하 여](using-the-get-allimagegroups-command.md)
[get ImageGroup 명령을 사용 하 여](using-the-get-imagegroup-command.md)
[하위 명령: ImageGroup 집합](subcommand-set-imagegroup.md)
