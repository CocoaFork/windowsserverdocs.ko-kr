---
title: Server Core 설치
description: Windows Server 2019, Windows Server 2016 또는 Windows Server (반기 채널)에 Server Core 설치를 설치 하는 방법.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 1/04/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: d99cd0b028d08d5c3247541ce3a868676b60693d
ms.sourcegitcommit: 7fc7271745e40f110c54918b55624cadd0d7ff98
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "8991800"
---
# Server Core 설치

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)
  
처음으로 Windows Server를 설치 하면 다음과 같은 설치 옵션이 있습니다.

>[!NOTE]
> 다음 목록에서 "Desktop Experience"이 없는 버전은 Server Core 설치 옵션입니다.

-   Windows Server Standard
-   Windows Server Standard with Desktop Experience
-   Windows Server Datacenter
-   Windows Server Datacenter with Desktop Experience

Windows Server (반기 채널), 버전 1709, 1803 및 1809를 포함 하 여 설치할 때 다음과 같은 설치 옵션이 표시.

-   Windows Server Standard 
-   Windows Server Datacenter

Server Core 옵션을 사용하면 디스크에 필요한 공간과 공격 취약성이 감소합니다. 따라서 데스크톱 환경 포함 서버 옵션에 포함된 추가 사용자 인터페이스 요소와 그래픽 관리 도구가 특별히 필요한 경우가 아니라면 Server Core 설치 옵션을 선택하는 것이 좋습니다. 추가 사용자 인터페이스 요소가 필요하다고 생각되면 [Desktop 환경 포함 서버 설치](Getting-Started-with-Server-with-Desktop-Experience.md)를 참조하세요. 

Server Core 옵션을 선택하면 표준 사용자 인터페이스(Desktop Experience)가 설치되지 않으므로 명령줄이나 Windows PowerShell 또는 원격 메서드를 사용하여 서버를 관리해야 합니다.

>[!NOTE]
>
>일부 이전 릴리스의 Windows Server와 달리 설치 후 Server Core와 데스크톱 경험 기능이 설치된 서버 간에 변환할 수 없습니다. Server Core를 설치하고 나중에 데스크톱 경험이 설치된 서버를 사용하기로 결정하는 경우에는 새로 설치를 수행해야 합니다.

**사용자 인터페이스:** 명령 프롬프트

**로컬에서 서버 역할 설치, 구성, 제거:** Windows PowerShell의 명령 프롬프트 사용

**설치, 구성, Windows 클라이언트 컴퓨터에서 원격으로 서버 역할을 제거 (또는 데스크톱 환경 포함 서버 설치):** 서버 관리자, 원격 서버 관리 도구 (RSAT), Windows PowerShell 또는 Windows Admin Center를 사용 하 여 합니다.

>[!NOTE]
>
>RSAT의 경우 Windows 10 버전을 사용해야 합니다.
>Microsoft Management Console은 로컬에서 사용할 수 없습니다.

**예제 서버 역할 사용할 수 있습니다.**

- Active Directory 인증서 서비스
- Active Directory Domain Services
- DHCP 서버
- DNS 서버
- 파일 서비스(파일 서버 리소스 관리자 포함)
- AD LDS(Active Directory Lightweight Directory Services)
- Hyper-V
- 인쇄 및 문서 서비스
- 스트리밍 미디어 서비스
- 웹 서버(ASP.NET의 하위 집합 포함)
- Windows Server Update Server
- Active Directory Rights Management Server
- 라우팅 및 원격 액세스 서버와 다음 하위 역할
- 원격 데스크톱 서비스 연결 브로커
- 라이선싱
- 가상화
- 볼륨 정품 인증 서비스

Server Core에 포함 되지 않은 역할, [역할, 역할 서비스 및 Windows Server-Server Core에 없는 기능을](../administration/server-core/server-core-removed-roles.md)참조 하세요.

## Windows Server 2019 또는 Windows Server 2016에 설치

일반적인 설치 단계 및 Windows Server (장기 서비스 채널)에 대 한 옵션에 대 한 [Windows Server 설치 및 업그레이드를](installation-and-upgrade.md)참조 하세요.

## Windows Server (반기 채널)에 설치

Windows Server (반기 채널)에 대 한 설치 단계는 이전 버전의 Windows Server 설치와 동일 (에서 합니다. ISO 이미지) 다음을 제외한:
- 이전 버전의 Windows Server로부터 Windows Server, 버전 1709로의 업그레이드가 지원되지 않습니다. 항상 새로 설치해야 합니다.
   즉, Windows 컴퓨터의 데스크톱에서 setup.exe를 실행 하면 설치 환경이 업그레이드 옵션 (회색) 금지 않습니다.
- Windows Server (반기 채널)에 대 한 평가 버전이 있는
- OEM 또는 일반 정품 버전이 없습니다. Windows Server (반기 채널) Software Assurance 또는 통해서도 프로그램을 통해 사용 허가 될 수 있습니다.

Windows Server, 버전 1709를 알아보려면 [Windows Server, 버전 1709 소개](get-started-with-1709.md)를 참조하세요.

Windows Server 버전 1803 가져오려면 [소개 Windows Server, 버전 1803](get-started-with-1803.md)참조 하세요.

Windows Server의 새로운 기능, 버전 1809 참조 [Windows Server 버전 1809의에서 새로운 기능](whats-new-in-windows-server-1809.md)
