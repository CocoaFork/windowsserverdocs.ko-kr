---
title: 하위 명령 시작-서버
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1bdf80aa9c255e12e1e4821467d556eb67f8691
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370727"
---
# <a name="subcommand-start-transportserver"></a>시작-TransportServer 하위 명령:

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전송 서버에 대 한 모든 서비스를 시작 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|전송 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예와
서버를 시작 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[TransportServer 사용 안 함 명령을 사용 하 여](using-the-disable-transportserver-command.md)
[사용 TransportServer 명령을 사용 하 여](using-the-enable-transportserver-command.md)
[get TransportServer 명령을 사용 하 여](using-the-get-transportserver-command.md)
[하위 명령: 집합 TransportServer](subcommand-set-transportserver.md)
[하위 명령: TransportServer 중지](subcommand-stop-transportserver.md)
