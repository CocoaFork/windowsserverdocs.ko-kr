---
title: 하위 명령 중지-서버
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7584dcbca5bfc52d303f187f62be24cbad407416
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383736"
---
# <a name="subcommand-stop-server"></a>하위 명령: 서버 중지

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 배포 서비스 서버에서 모든 서비스를 중지합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="BKMK_examples"></a>예와
서비스를 중지 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[는 서버 사용 안 함-명령을 사용 하 여](using-the-disable-server-command.md)
[사용 서버 명령을 사용 하 여](using-the-enable-server-command.md)
[get 서버 명령을 사용 하 여](using-the-get-server-command.md)
[Initialize 서버 명령을 사용 하 여](using-the-initialize-server-command.md)
[하위 명령: 서버 설정](subcommand-set-server.md)
[하위 명령: 서버 시작](subcommand-start-server.md)
[초기화 서버 옵션](the-uninitialize-server-option.md)
