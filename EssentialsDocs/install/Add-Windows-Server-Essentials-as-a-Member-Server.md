---
title: Windows Server Essentials를 구성원 서버로 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d09dd82f-f7d2-47ce-862d-fd9869f2021c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 502e54cf719895dd11030cf163159f6cdda47164
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433734"
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials를 구성원 서버로 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 Windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 R2 Standard, Windows Server 2012 R2 Datacenter, 또는 Windows Server 2016을 실행 하는 서버에 적용 됩니다. 이 문서의 나머지 부분에서는 Windows Server 필수 패키지 환경 역할을 Windows Server Essentials라고 합니다.  
  
> [!NOTE]
>   Windows Server Essentials 도메인 컨트롤러로 배포할 수 있습니다. 이 문서에서는 Windows Server Essentials는 Windows Server Essentials를 다루지 않습니다.  
  
 Windows Server Essentials는 Windows 도메인 내에서 주 서버일 필요가 없습니다. Windows Server Essentials를 기존 Active Directory 도메인 환경에 구성원 서버로 추가하여 이러한 환경에서 제공되는 단순한 데이터 보호, 보안된 원격 액세스 및 클라우드 통합 기능을 활용할 수 있습니다. 또한 Windows Server Essentials를 기존 Active Directory 환경에 도메인 컨트롤러로 사용하지 않고 배포할 수 있습니다. 따라서 저장소를 확장하거나 로컬 저장소 및 관리에 지점을 사용할 수 있습니다.  
  
 다음과 같은 시나리오에서 Windows Server Essentials를 추가할 수 있습니다.  
  
-   네이티브 도구를 사용하여 지점에 Windows Server Essentials를 추가하고 별도의 위치에 있는 본사에 소재한 도메인 컨트롤러에 가입시킵니다. 이 구성원 서버에 대한 최적의 대역폭 이용률을 위해 BranchCache 기능을 설정할 수 있습니다.  
  
-   Windows Server Essentials를 구성원 서버에서 서버 폴더를 더 추가 하 여 네트워크의 저장소를 확장 하는 데 Windows Server Essentials 네트워크 내에 구성원 서버로 추가 합니다.  
  
-   Windows Server Essentials를 실행 하는 주 서버는 Microsoft Azure에서 호스팅되는 경우 Windows Server Essentials를 지사에 구성원 서버로 추가 또는 타사 호스팅 서비스 공급자에서 호스트 합니다. 지사에 Windows Server Essentials를 구성원 서버로 보유하면 대역폭 이용률을 최적화하는 데 도움이 됩니다.  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials를 구성원 서버로 추가  
 Windows Server Essentials를 구성원 서버로 기존 Active Directory 환경에서 Windows Server 2012 R2 또는 Windows Server Essentials를 실행 하는 주 서버를 추가 하려면 다음 단계를 완료 해야 합니다.  
  
1.  Windows Server Essentials를 실행하는 서버를 작업 그룹에 가입시킵니다.  
  
2.  기본 Windows Server Essentials 서버의 도메인에 Windows Server Essentials를 실행 하는 서버를 조인 합니다.  
  
3.  Windows Server Essentials Experience 서버 관리자에서 구성 합니다.  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Windows Server Essentials를 작업 그룹 또는 도메인에 가입시키려면  
  
1. 두 번째 서버에서 Windows Server Essentials 설치를 완료한 후 Windows Server Essentials 구성 마법사를 닫습니다.  
  
2. **검색** 상자에 **System Settings**를 입력한 후 검색 결과에서 **고급 시스템 설정 보기**를 클릭합니다.  
  
3. **시스템 속성**에서 **컴퓨터 이름** 탭을 클릭합니다.  
  
4. **컴퓨터 이름**의 **도메인** 섹션에서 **변경**을 클릭합니다.  
  
5. **컴퓨터 이름/도메인 변경**를 **멤버** 섹션에서 Windows Server Essentials를 실행 하는 서버를 가입 하려는 경우를 **작업 그룹** 또는 **도메인**합니다.  
  
   -   서버를 작업 그룹에 추가하려면 **workgroup**을 입력한 후 **확인**을 클릭합니다.  
  
   -   이 서버를 기존 Active Directory 도메인에 가입시키려면 도메인의 이름을 입력한 후 **확인**을 클릭합니다.  
  
6. 서버를 다시 시작하여 변경 내용을 적용합니다.  
  
   서버를 주 서버의 도메인에 가입 후 서버 관리자에서 Windows Server Essentials 구성 마법사를 실행 하 여 Windows Server Essentials를 구성 하려면 계속할 수 있습니다.  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>구성원 서버에서 Windows Server 필수 패키지 환경을 구성하려면  
  
1.  (선택 사항) 필요한 경우 서버 이름을 변경합니다.  
  
    > [!IMPORTANT]
    >  Windows Server Essentials Experience를 구성한 후 서버 이름을 변경할 수 없습니다.  
  
2.  도메인 관리자 계정을 사용하여 서버에 로그인합니다.  
  
3.  서버 관리자를 엽니다.  
  
4.  **서버 관리자**의 플래그 알림 영역에서 플래그를 클릭한 후 **Windows Server Essentials 구성**을 클릭합니다.  
  
5.  서버를 구성원 서버로 구성하도록 선택한 후 **다음**을 클릭합니다.  
  
6.  **구성**을 클릭하여 구성을 시작합니다. 구성 프로세스를 완료하는 데 10분 정도 걸립니다.  
  
7.  바탕 화면에서 대시보드 아이콘을 클릭하여 서버 대시보드를 시작합니다. 홈 페이지에서 **설치** 탭에 나열된 **시작** 작업을 완료합니다.  
  
## <a name="see-also"></a>참조  
  

-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

-   [Windows Server Essentials 설치](../install/Install-Windows-Server-Essentials.md)
