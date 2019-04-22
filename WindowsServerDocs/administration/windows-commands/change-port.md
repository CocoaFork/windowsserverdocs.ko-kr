---
title: change port
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 477761c35f08d5ec81adae80ba8f2fe9667786e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818644"
---
# <a name="change-port"></a>change port

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

나열 하거나 MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 변경 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.
## <a name="syntax"></a>구문
```
change port [<PortX>=<PortY> | /d <PortX> | /query]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<PortX>=<PortY>|COM 매핑합니다 <*PortX*>를 <*PortY*>입니다.|
|/d <PortX>|COM에 대 한 매핑을 삭제 하는 <*PortX*>.|
|/ 쿼리|현재 포트 매핑을 표시합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
-   대부분의 MS-DOS 응용 프로그램 COM4 직렬 포트를 통해 c o m 1만 지원합니다. **포트 변경** 명령 직렬 포트에 액세스 하는 포트 번호가 큰 COM을 지원 하지 않는 응용 프로그램을 허용 하는 다른 포트 번호를 직렬 포트에 매핑합니다. 다시 매핑 현재 세션에 대해서만 작동 하며 세션에서 로그 오프 한 다음 다시 로그온 하는 경우 유지 되지 않습니다.
-   사용 하 여 **포트 변경** 대 한 현재 매핑을 사용할 수 있는 COM 포트를 표시 하려면 매개 변수 없이 합니다.
## <a name="BKMK_examples"></a>예제
-   COM12 c o m 1을 사용 하기 위해 MS-DOS-기반 응용 프로그램을 매핑하려면 다음을 입력 합니다.
    ```
    change port com12=com1
    ```
-   현재 매핑된 포트를 표시 하려면 다음을 입력 합니다.
    ```
    change port /query
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[변경할](change.md)
[Remote Desktop Services &#40;터미널&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
