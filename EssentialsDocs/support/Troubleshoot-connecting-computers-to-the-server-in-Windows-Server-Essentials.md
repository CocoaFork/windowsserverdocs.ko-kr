---
title: Windows Server Essentials에서 서버에 컴퓨터 연결 시 발생하는 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 52ec9bf1caa4cb4c7ed661eec1448f3f2a4be980
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436053"
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Windows Server Essentials에서 서버에 컴퓨터 연결 시 발생하는 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 이 항목에서는 Windows Server Essentials를 실행 하는 서버 또는 Windows Server Essentials에 컴퓨터를 연결할 때 발생할 수 있는 문제에 대 한 문제 해결 지침을 포함 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 및 Windows Server Essentials 커뮤니티에서 최신 문제 해결 정보에 대 한 것이 좋습니다를 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserveressentials)합니다. Windows Server Essentials 포럼은 도움말을 검색하거나 질문하기 좋은 곳입니다.  
  
 이 항목에서는 다음 문제에 대한 솔루션을 제공합니다.  
  

-   문제 1: [문제 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   문제점 2: [문제점 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   문제 3: [문제점 3](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   문제 4: [문제 4](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   문제 5: [문제 5](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   문제 6: [문제 6](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   문제 7: [문제 7](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   문제 8: [문제 8](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   문제 9: [문제 9](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   문제 10: [문제 10](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   문제 11: [문제 11](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

-   문제 1: [문제 1](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   문제점 2: [문제점 2](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   문제 3: [문제점 3](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   문제 4: [문제 4](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   문제 5: [문제 5](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   문제 6: [문제 6](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   문제 7: [문제 7](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   문제 8: [문제 8](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   문제 9: [문제 9](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   문제 10: [문제 10](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   문제 11: [문제 11](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

  
##  <a name="BMRK_Package"></a> 문제 1  
 **문제점**  
  
 내가 패키지 설치에 실패 했습니다. Windows Server Essentials 커넥터를 다시 설치하세요. 문제가 지속 되 면 컴퓨터를 서버에 연결할 때 네트워크 관리자 오류에 문의  
  
 **설명**  
  
 이 문제는 다른 Windows 업데이트 또는 응용 프로그램 설치 보류 중이 고 커넥터 설치가 취소 하는 동안 Windows Server Essentials를 실행 하는 서버에 컴퓨터를 연결 하는 경우에 발생할 수 있습니다.  
  
 **해결 방법**  
  
 다른 모든 업데이트 또는 응용 프로그램 설치를 완료합니다. 메시지가 표시되면 컴퓨터를 다시 시작합니다.  
  
##  <a name="BKMK_ConnectorIssue2"></a> 문제점 2  
 **문제점**  
  
 Windows Server Essentials에 컴퓨터를 가입할 수 없습니다.  
  
 **설명**  
  
 Windows Server Essentials에 컴퓨터 이름에 비 ASCII 문자를 포함 하는 컴퓨터를 조인할 수 없습니다. 컴퓨터 이름에 비 ASCII 문자가 포함되어 있으면 "예기치 않은 오류가 발생했습니다." 오류 메시지가 나타납니다.  
  
 **해결 방법**  
  
 ASCII 문자만 포함 된 이름 사용 하 여 클라이언트 컴퓨터 이름을 바꾸고 Windows Server Essentials에 컴퓨터를 다시 추가 하려고 합니다.  
  
##  <a name="BKMK_ConnectorIssue2a"></a> 문제점 3  
 **문제점**  
  
 오류가 커넥터 소프트웨어 설치가 취소 된 서버에 컴퓨터를 연결 하는 경우  
  
 **설명**  
  
 서버에 컴퓨터를 연결할 수 시스템 계정에 Windows Server Essentials 대시보드를 표시 하는 서버 폴더에서 전체 권한이 있어야 합니다. 필요한 사용 권한이 부여되지 않은 경우 "커넥터 소프트웨어 설치가 취소되었습니다." 오류 메시지가 나타납니다.  
  
 **해결 방법**  
  
 SYSTEM 계정에 각 서버 폴더에 대한 **모든 권한** 을 부여합니다.  
  
#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>SYSTEM 계정에 서버 폴더에 대한 모든 권한을 부여하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  **저장소**, **서버 폴더**를 차례로 클릭합니다.  
  
3.  서버 폴더를 마우스 오른쪽 단추로 클릭한 다음 **폴더 열기**를 클릭합니다. **폴더 열기** 옵션이 표시되지 않는 경우 폴더에 대한 사용 권한을 설정할 필요가 없습니다.  
  
4.  Windows 탐색기의 맨 위에 있는 네트워크 경로에서 서버 공유를 클릭하여 서버의 공유 폴더를 표시합니다. 예를 들어 경로가 **네트워크 > Server01 > 파일 히스토리 백업**인 경우 **Server01**을 클릭합니다.  
  
5.  서버 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
6.  **보안** 탭을 클릭합니다.  
  
7.  SYSTEM 계정에 대해 **모든 권한**이 허용되지 않는 경우 **편집**, **SYSTEM**을 차례로 클릭합니다. **SYSTEM의 사용 권한**아래에서 **모든 권한** 옆의 **허용**확인란을 선택합니다.  
  
8.  **확인** 을 두 번 클릭하여 사용 권한을 업데이트하고 **속성**을 닫습니다.  
  
##  <a name="BKMK_ConnectorIssueNetFramework"></a> Issue 4  
 **문제점**  
  
 이 응용 프로그램을 실행 하는 To 인가요,.NET Framework의 다음 버전 중 하나를 설치 해야 합니다. V4.5.50709" 오류가 표시됨  
  
 **설명**  
  
 Windows Server Essentials를 실행 하는 서버 또는 Windows Server Essentials에 컴퓨터를 연결할 때 마법사에서는.NET Framework 버전 4.5.50709 컴퓨터에 설치 하려고 합니다. 그러나 이전 버전의.NET Framework 버전 4.5가 있는 경우 업데이트 된 릴리스를 설치할 수 없습니다 및이 오류 메시지와 함께 연결 시도가 실패 합니다. 이 응용 프로그램을 실행 하려면.NET Framework의 다음 버전 중 하나를 설치 해야 합니다. V4.5.50709. .NET Framework의 적절 한 버전에 대 한 지침은 할당 게시자에 게 문의 합니다.  
  
 **해결 방법**  
  
 컴퓨터에서 .NET Framework 4.5를 제거한 다음 컴퓨터를 서버에 연결합니다.  
  
#### <a name="to-uninstall-net-framework-45"></a>.NET Framework 4.5를 제거하려면  
  
1.  클라이언트 컴퓨터의 **시작** 페이지에서 **제어판**을 엽니다.  
  
2.  제어판의 **프로그램**에서 **프로그램 제거**를 클릭합니다.  
  
3.  **Microsoft .NET Framework 4.5**를 마우스 오른쪽 단추로 클릭한 다음 **제거**를 클릭합니다.  
  
4.  .NET Framework 4.5를 제거한 후 컴퓨터를 서버에 연결합니다. .NET Framework 4.5의 올바른 릴리스가 커넥터 소프트웨어와 함께 설치됩니다.  
  
##  <a name="BKMK_Time"></a> 문제 5  
 **문제점**  
  
 얻게 된 서버를 사용할 수 없습니다. 이 문제를 해결 하려면 네트워크에 대 한 담당자에 게 문의 합니다. 오류가 표시됨  
  
 **설명**  
  
 이 문제는 연결된 컴퓨터의 날짜 및 시간이 서버의 날짜 및 시간과 동기화되지 않은 경우에 발생할 수 있습니다.  Windows Server Essentials 및 Windows Server Essentials는 Windows Server Essentials 또는 Windows Server Essentials 네트워크에서 실행 하는 컴퓨터의 시간과 날짜를 동기화 하는 시간 동기화 서비스를 사용 합니다. 기본 인증 프로토콜이 서버 시간을 인증 프로세스의 일부로 사용하므로 동기화된 시간은 중요합니다. 예를 들어, 클라이언트 컴퓨터에 있는 시계가 올바른 날짜 및 시간, Windows Server Essentials에 동기화 되지 않았거나 Windows Server Essentials 인증 잘못 될 수 있습니다 하는 경우 로그온 요청을 침입 시도로 해석 하 고 사용자에 대 한 액세스를 거부 합니다.  
  
 이 서버의 사용 가능한 메모리가 5% 미만인 경우에 발생할 수 있습니다.  
  
 이 문제는 Windows Essentials 서버에 대한 VPN 연결이 이미 있고 도메인 주소를 사용하여 오프-프레미스로 커넥터 소프트웨어를 구성하려는 경우에 발생할 수 있습니다.  
  
 **해결 방법**  
  
1.  클라이언트 컴퓨터의 날짜 및 시간을 서버의 날짜 및 시간과 동기화합니다. 그런 다음 컴퓨터를 서버에 연결합니다.  
  
2.  서버 쪽에서 일부 응용 프로그램을 닫은 후 컴퓨터를 서버에 연결합니다.  
  
3.  VPN 연결을 닫은 후 컴퓨터를 서버에 연결합니다.  
  
#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>클라이언트 컴퓨터의 날짜 및 시간을 변경하려면  
  
1. 클라이언트 컴퓨터의 시작 페이지에서 **제어판**을 엽니다.  
  
2. 제어판에서 **시계, 언어 및 국가별 옵션**을 클릭한 다음 **날짜 및 시간**을 클릭합니다.  
  
3. **날짜 및 시간 변경**을 클릭하고 날짜 및 시간을 올바른 날짜 및 시간으로 설정한 다음 **확인**을 클릭합니다.  
  
4. **확인**을 클릭하고 제어판을 닫습니다.  
  
5. 클라이언트 컴퓨터를 서버에 다시 연결합니다. 지침은 서버에 컴퓨터 연결을 참조하세요.  
  
   그래도 클라이언트 컴퓨터를 서버에 연결할 수 없는 경우 서버의 날짜 및 시간이 올바른지 확인합니다. 날짜 및 시간이 잘못된 경우 변경합니다.  
  
#### <a name="to-change-the-date-and-time-on-the-server"></a>서버의 날짜 및 시간을 변경하려면  
  
1.  Windows Server Essentials 또는 Windows Server Essentials 설치 및 구성 하는 동안 설정 하는 암호를 사용 하 여 서버에 로그온 합니다.  
  
    > [!NOTE]
    >  서버를 원격으로 관리하는 경우 원격 데스크톱 연결을 사용하여 서버에 로그온해야 합니다.  
  
2.  **시작** 페이지에서 **제어판**을 엽니다.  
  
3.  제어판에서 **시계, 언어 및 국가별 옵션**을 클릭한 다음 **날짜 및 시간**을 클릭합니다.  
  
4.  **날짜 및 시간 변경**을 클릭하고 날짜 및 시간을 올바른 날짜 및 시간으로 설정한 다음 **확인**을 클릭합니다.  
  
5.  **확인**을 클릭하고 제어판을 닫습니다.  
  
6.  클라이언트 컴퓨터에서 클라이언트 컴퓨터를 서버에 다시 연결합니다. 지침은 서버에 컴퓨터 연결을 참조하세요.  
  
##  <a name="BKMK_ServiceStopped"></a> 문제 6  
 **문제점**  
  
 An 가져오는 예기치 않은 오류가 발생 했습니다. 이 문제를 해결 하려면 네트워크에 대 한 담당자에 게 문의 합니다. 오류가 표시됨  
  
 **설명**  
  
 이 오류 메시지가 나타나는 경우 WSS 인증서 웹 서비스가 실행되고 있지 않을 수 있습니다.  
  
 **해결 방법**  
  
 WSS 인증서 웹 서비스를 시작합니다.  
  
#### <a name="to-start-the-wss-certificate-web-service"></a>WSS 인증서 웹 서비스를 시작하려면  
  
1.  서버의 **시작** 페이지에서 **관리 도구**를 엽니다.  
  
     **관리 도구**에서 **IIS(인터넷 정보 서비스) 관리자**를 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭합니다.  
  
2.  탐색 창에서 **WSS 인증서 웹 서비스**를 클릭합니다.  
  
3.  **작업** 창에서 **시작**을 클릭합니다.  
  
##  <a name="BKMK_ConnectorIssueReconnect"></a> 문제 7  
 **문제점**  
  
 컴퓨터는 연결 시도가 실패 한 후 다시 서버에 연결할 때이 이름 가진 컴퓨터가 서버에 이미 연결 되어 경고가 나타나는  
  
 **설명**  
  
 컴퓨터를 서버에 연결하려는 이전 시도가 취소 또는 중단된 경우 다시 연결할 때 다음과 같은 경고가 나타날 수 있습니다. 이 이름 가진 컴퓨터는 서버에 이미 연결 됩니다. 이 문제는 서버에 처음 연결을 시도했을 때 인증서가 발급되었기 때문에 발생합니다.  
  
 **해결 방법** 동일한 이름을 가진 다른 컴퓨터가 서버에 연결되어 있지 않은 것을 확신하는 경우 **다음**을 클릭하고 지침에 따라 **서버에 컴퓨터 연결** 마법사를 완료합니다.  
  
##  <a name="BKMK_JoinWin7"></a> 문제 8  
 **문제점**  
  
 Windows 7 Home을 실행하는 클라이언트 컴퓨터를 서버에 연결하려고 하면 커넥터 소프트웨어를 실행하기 위한 웹 페이지가 열리지만 클라이언트 컴퓨터가 서버에 연결할 수 없음  
  
 **설명**  
  
 네트워크의 라우터에서 멀티캐스트가 사용되는 경우 Windows 7 Home Basic 또는 Windows 7 Home Premium을 실행하는 클라이언트 컴퓨터와 서버 간의 통신이 올바르게 작동하지 않습니다.  
  
 **해결 방법**  
  
 라우터에서 멀티캐스트를 사용하지 않도록 설정합니다. 일부 라우터에서는 RIP-2M 라우팅 프로토콜을 사용하지 않도록 설정하는 작업이 포함될 수도 있습니다. 자세한 내용은 라우터 제조업체에서 제공한 설명서를 참조하세요.  
  
##  <a name="BKMK_ConnectorIssueAutologon"></a> 문제 9  
 **문제점**  
  
 컴퓨터를 서버에 연결한 후 자동 로그온이 작동 중지됨  
  
 **설명**  
  
 자동 로그온에 대해 설정 된 사용자 계정을 Windows Server Essentials에 컴퓨터를 연결 하는 경우 컴퓨터에 connector 소프트웨어를 설치할 때 설정을 덮어씁니다.  
  
 **해결 방법** 이 문제를 해결하려면 컴퓨터를 서버에 연결할 때 사용자 계정에 사용되는 암호를 적어둡니다. 커넥터 소프트웨어가 설치된 후 해당 계정을 사용하도록 자동 로그온을 구성합니다.  
  
> [!NOTE]
>  Windows Server Essentials 도메인 계정에는 기본 암호 정책 요구 사항을 충족 하는 암호가 필요 합니다.  
  
##  <a name="BKMK_ConnectorIssueOldLogs"></a> 문제 10  
 **문제점**  
  
 커넥터 소프트웨어의 시험판 버전을 제거하는 경우 기존 로그가 제거되지 않음  
  
 **설명**  
  
 Windows Server Essentials의 시험판 (베타 또는 RC) 버전에서 정식된 버전으로 업데이트 한 후 서버에 연결 된 각 컴퓨터에서 connector 소프트웨어를 제거 하며 컴퓨터 릴리스된 설치를 다시 연결 connector 소프트웨어의 버전입니다.  
  
 그러나 네트워크 컴퓨터에서 커넥터 소프트웨어를 제거할 때 해당 컴퓨터의 %ProgramData%\Microsoft\Windows Server\Logs\ 폴더에 있는 기존 로그 파일은 삭제되지 않습니다. Logs 폴더를 삭제 하면 Windows Server Essentials의 릴리스 버전에 컴퓨터를 연결한 경우에 로그 파일 손상 될 수 있습니다.  
  
 **해결 방법** 로그 파일의 손상을 방지하려면 클라이언트 컴퓨터를 업데이트된 서버에 다시 연결하기 전에 Logs 폴더를 수동으로 삭제합니다.  
  
#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>로그 파일을 손상시키지 않고 서버 업데이트 후에 컴퓨터를 다시 연결하려면  
  
1.  클라이언트 컴퓨터에서 커넥터 소프트웨어를 제거합니다.  
  
2.  %ProgramData%\Microsoft\Windows Server\ 폴더에서 Logs 폴더를 삭제합니다.  
  
3.  서버에 컴퓨터를 다시 연결합니다. 그러면 커넥터 소프트웨어의 릴리스 버전이 설치되고 새 Logs 폴더와 로그 파일이 생성됩니다.  
  
##  <a name="BKMK_UpgradeClientOS"></a> 문제 11  
 **문제점**  
  
 클라이언트 컴퓨터의 운영 체제를 업그레이드하려고 함  
  
 **설명**  
  
 커넥터 소프트웨어를 설치하는 동안 클라이언트 운영 체제에 대해 다양한 검사가 수행되어 클라이언트가 커넥터 필수 조건을 모두 충족하는지 확인합니다. 커넥터 소프트웨어를 설치한 후 클라이언트 운영 체제를 업그레이드하는 경우 필수 조건 중 일부가 없을 수 있으며 클라이언트 커넥터가 실패할 수도 있습니다.  
  
 **해결 방법**  
  
 클라이언트 운영 체제를 다른 버전으로 업그레이드하기 전에(예: Windows XP를 Windows Vista로 업그레이드 또는 Windows Vista를 Windows 7으로 업그레이드) 커넥터 소프트웨어를 제거해야 합니다. 제어판의 **프로그램 추가/제거**를 사용합니다. 클라이언트 운영 체제 업그레이드를 완료 한 후 http://&lt 열어 클라이언트 커넥터 다시를 설치할 수 있습니다*서버*> 웹 브라우저에서 연결 / 여기서 <*server*>의 이름인 합니다  Windows Server Essentials 서버입니다.  
  
 커넥터 소프트웨어가 설치되어 있는 클라이언트를 이미 업그레이드한 경우 **프로그램 추가/제거** 또는 **프로그램 및 기능**을 사용하여 커넥터 소프트웨어를 제거합니다. 그런 다음 커넥터 소프트웨어를 다시 설치합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  
-   [Windows 2012 Server Essentials ConnectComputer (TechNet Wiki) 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/14370.windows-2012-server-essentials-connectcomputer-troubleshooting.aspx)
