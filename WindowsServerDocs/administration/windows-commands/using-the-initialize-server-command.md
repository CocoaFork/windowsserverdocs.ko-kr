---
title: 서버 초기화 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9e95972838fc70ee1e617d1e299c9e35db5b979
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392099"
---
# <a name="using-the-initialize-server-command"></a>서버 초기화 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버 역할이 설치 된 후 초기 사용을 위해 Windows 배포 서비스 서버를 구성 합니다. 이 명령을 실행 한 후에 이미지 추가 [명령을](using-the-add-image-command.md) 사용 하 여 서버에 이미지를 추가 해야 합니다.
## <a name="syntax"></a>구문
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/Uia: "<Full path>"|RemoteInstall 폴더의 전체 경로와 이름을 지정 합니다. 지정 된 폴더가 존재 하지 않는 경우이 옵션을 선택 하면 명령이 실행 될 때 해당 폴더가 만들어집니다. 원격 컴퓨터의 경우에도 항상 로컬 경로를 입력 해야 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **D:\remoteInstall**.|
|/Authorize|DHCP (Dynamic Host Control Protocol)에서 서버에 권한을 부여 합니다. 이 옵션은 DHCP rogue 검색이 사용 되는 경우에만 필요 합니다. 즉, 클라이언트 컴퓨터를 서비스 하려면 먼저 DHCP에서 Windows 배포 서비스 PXE 서버에 권한을 부여 해야 합니다. DHCP rogue 검색은 기본적으로 사용 되지 않습니다.|
## <a name="BKMK_examples"></a>예와
서버를 초기화 하 고 remoteInstall 공유 폴더를 F: 드라이브에 설정 하려면을 입력 합니다.
```
wdsutil /Initialize-Server /remInst:"F:\remoteInstall"
```
서버를 초기화 하 고 remoteInstall 공유 폴더를 C: 드라이브로 설정 하려면을 입력 합니다.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:"C:\remoteInstall"
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
 사용[안 함](using-the-disable-server-command.md)-서버 명령을 사용 하 여 @no__t-[3 명령을 사용 하 여 @no__t](using-the-enable-server-command.md)-5[Get 서버](using-the-get-server-command.md)명령을 사용 
 하위 명령:[설정 서버](subcommand-set-server.md)
 하위 명령[: 시작-서버](subcommand-start-server.md)1[하위 명령: 중지](subcommand-stop-server.md)-서버 3[초기화 서버 옵션](the-uninitialize-server-option.md)
