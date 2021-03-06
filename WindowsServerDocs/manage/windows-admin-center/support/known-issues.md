---
title: Windows Admin Center 알려진 문제
description: Windows Admin Center 알려진 문제(Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 4a91d09d6824795a21a9a7cdc7695c407aa70756
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322925"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center 알려진 문제

> 적용 대상: Windows 관리 센터, Windows 관리 센터 미리 보기

이 페이지에서 설명하지 않은 문제가 발생하는 경우 [알려주십시오](https://aka.ms/WACfeedback).

## <a name="installer"></a>설치 관리자

- 직접 인증서를 사용하여 Windows Admin Center를 설치하는 경우 인증서 관리자 MMC 도구에서 지문을 복사하면 [시작 부분에 잘못된 문자가 포함됩니다](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra). 해결 방법으로 지문의 첫 문자를 입력하고 나머지를 복사/붙여넣습니다.

- 1024 미만의 포트 사용은 지원 되지 않습니다. 서비스 모드에서는 지정 된 포트로 리디렉션하도록 포트 80을 선택적으로 구성할 수 있습니다.

## <a name="general"></a>일반

- Windows 관리 센터를 사용 중인 **Windows Server 2016** 에 게이트웨이로 설치한 경우 서비스는 ```Faulting application name: sme.exe``` 및 ```Faulting module name: WsmSvc.dll```를 포함 하는 이벤트 로그의 오류로 인해 중단 될 수 있습니다. 이 문제는 Windows Server 2019에서 수정 된 버그로 인해 발생 합니다. Windows Server 2016에 대 한 패치는 2 월 2019 누적 업데이트 [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)에 포함 되었습니다.

- Windows 관리 센터를 게이트웨이로 설치 하 고 연결 목록이 손상 된 것으로 나타나는 경우 다음 단계를 수행 합니다.

   > [!WARNING]
   >그러면 게이트웨이에서 모든 Windows 관리 센터 사용자에 대 한 연결 목록과 설정이 삭제 됩니다.

  1. Windows Admin Center 제거
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** 아래에 있는 **Server Management Experience** 폴더를 삭제합니다.
  3. Windows Admin Center 다시 설치

- 오랜 시간 동안 이 도구를 열어 놓고 사용하지 않으면 여러 **오류: 이 작업에 대한 runspace 상태가 잘못됨** 오류가 발생합니다. 이 문제가 발생하는 경우 브라우저를 새로 고칩니다. 이 문제가 발생 하면 [사용자 의견을 보내 주시기](https://aka.ms/WACfeedback)바랍니다.

- Windows 관리 센터 모듈에서 실행 되는 OSS 버전 번호 사이에는 약간의 차이가 있을 수 있으며 타사 소프트웨어 공지에 나열 됩니다.

### <a name="extension-manager"></a>확장 관리자

- Windows 관리 센터를 업데이트할 때 확장을 다시 설치 해야 합니다.
- 액세스할 수 없는 확장 피드를 추가 하는 경우에는 경고가 발생 하지 않습니다. [14412861]

## <a name="browser-specific-issues"></a>특정 브라우저 문제

### <a name="microsoft-edge"></a>Microsoft Edge

- Windows 관리 센터를 서비스로 배포 하 고 Microsoft Edge를 브라우저로 사용 하는 경우 새 브라우저 창을 생성 한 후 게이트웨이를 Azure에 연결 하지 못할 수 있습니다. 게이트웨이의 https://login.microsoftonline.com, https://login.live.com및 URL을 신뢰할 수 있는 사이트로 추가 하 고 클라이언트 쪽 브라우저에서 팝업 차단 설정에 허용 되는 사이트를 추가 하 여이 문제를 해결 해 보십시오. 이 문제를 해결 하는 방법에 대 한 자세한 내용은 [문제 해결 가이드를 참조](troubleshooting.md#azure-features-dont-work-properly-in-edge)하세요. [17990376]

### <a name="google-chrome"></a>Google Chrome

- 버전 70 (2018 년 10 월 출시) Chrome 이전에는 websocket 프로토콜 및 NTLM 인증에 대 한 [버그가](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) 있었습니다. 이는 이벤트, PowerShell, 원격 데스크톱과 같은 도구에 영향을 줍니다.

- Chrome에서 특히 **작업 그룹**(비도메인) 환경에서 연결 환경을 추가하는 동안 여러 자격 증명 메시지를 표시할 수 있습니다.

- Windows 관리 센터를 서비스로 배포한 경우 Azure 통합 기능이 작동 하려면 게이트웨이 URL에서 팝업을 사용 하도록 설정 해야 합니다.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center는 Mozilla Firefox에 대해 테스트되지 않지만 대부분의 기능이 작동해야 합니다.

- Windows 10 설치: Mozilla Firefox에는 자체 인증서 저장소가 있으므로 Windows 10에서 Windows 관리 센터를 사용 하려면 ```Windows Admin Center Client``` 인증서를 Firefox로 가져와야 합니다.

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>프록시 서비스를 사용 하는 경우 WebSocket 호환성

Windows Admin Center에서 원격 데스크톱, PowerShell 및 이벤트 모듈은 프록시 서비스를 사용할 때 종종 지원되지 않는 WebSocket 프로토콜을 활용합니다. Azure AD 응용 프로그램 프록시 호환성에서 WebSocket 지원은 [미리 보기](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)이며 호환성에 대한 피드백을 받고 있습니다.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>2016 이전의 Windows Server 버전에 대 한 지원 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows 관리 센터에는 Windows Server 2012 R2, 2012 또는 2008 r 2에 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows 관리 센터에서 Windows Server를 관리 하려면 해당 서버에 WMF 버전 5.1 이상을 설치 해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치할](https://www.microsoft.com/download/details.aspx?id=54616)수 있습니다.

## <a name="role-based-access-control-rbac"></a>RBAC (역할 기반 Access Control)

- RBAC 배포가 Windows Defender Application Control(WDAC, 이전의 코드 무결성)을 사용하기 위해 구성된 컴퓨터에서 성공하지 않습니다. [16568455]

- 클러스터에서 RBAC를 사용하려면 구성을 각 구성원 노드에 개별적으로 배포해야 합니다.

- RBAC를 배포하는 경우 RBAC 구성에 올바르지 않게 지정된 권한이 없는 오류가 발생할 수 있습니다. [16369238]

## <a name="server-manager-solution"></a>서버 관리자 솔루션

### <a name="certificates"></a>인증서

- 현재 사용자 저장소에 .PFX 암호화 인증서를 가져올 수 없습니다. [11818622]

### <a name="events"></a>이벤트

- 이벤트는 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websocket-compatibility-when-using-a-proxy-service)의 영향을 받습니다.

- 큰 로그 파일을 내보낼 때 "패킷 크기"를 참조하는 오류 메시지가 표시될 수 있습니다.

  - 이 문제를 해결 하려면 게이트웨이 컴퓨터의 관리자 권한 명령 프롬프트에서 다음 명령을 사용 합니다. ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>Files

- 대용량 파일 업로드 또는 다운로드는 아직 지원하지 않습니다. (\~100mb 제한) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell은 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websocket-compatibility-when-using-a-proxy-service)의 영향을 받습니다.

- 데스크톱 PowerShell 콘솔에서와 같이 마우스 오른쪽 단추를 한 번 클릭하여 붙여넣는 것은 작동하지 않습니다. 대신 붙여넣기를 선택할 수 있는 브라우저의 컨텍스트 메뉴를 얻을 수 있습니다. Ctrl+V도 작동합니다.

- Ctrl+ C 복사할 수는 없으며 항상 콘솔에 Ctrl+C Break 명령이 보내집니다. 마우스 오른쪽 단추 클릭 컨텍스트 메뉴에서 복사할 수 있습니다.

- Windows Admin Center 창 크기를 줄이면 터미널 콘텐츠는 재배치되지만 다시 크기를 키우면 콘텐츠는 이전 상태로 되돌아가지 않을 수 있습니다. 콘텐츠가 뒤죽박죽으로 섞여 있는 경우 Clear-Host를 시도하거나 터미널 위의 버튼을 사용하여 연결을 끊고 다시 연결합니다.

### <a name="registry-editor"></a>레지스트리 편집기

- 검색 기능이 구현되지 않았습니다. [13820009]

### <a name="remote-desktop"></a>원격 데스크톱

- Windows 관리 센터를 서비스로 배포 하는 경우 Windows 관리 센터 서비스를 새 버전으로 업데이트 한 후 원격 데스크톱 도구를 로드 하지 못할 수 있습니다. 이 문제를 해결 하려면 브라우저 캐시를 지웁니다.   [23824194]

- Windows Server 2012을 관리 하는 경우 원격 데스크톱 도구가 연결 되지 않을 수 있습니다. [20258278]

- 원격 데스크톱을 사용 하 여 도메인에 가입 되지 않은 컴퓨터에 연결 하는 경우 ```MACHINENAME\USERNAME``` 형식으로 계정을 입력 해야 합니다.

- 일부 구성에서는 그룹 정책을 사용 하 여 Windows 관리 센터의 원격 데스크톱 클라이언트를 차단할 수 있습니다. 이 문제가 발생 하는 경우 ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```에서 ```Allow users to connect remotely by using Remote Desktop Services```를 사용 하도록 설정 합니다.

- 원격 데스크톱은 [websocket 호환성](#websocket-compatibility-when-using-a-proxy-service) 의 영향을 받지 않습니다.

- 원격 데스크톱 도구는 현재 로컬 데스크톱 및 원격 세션 간에 모든 텍스트, 이미지 또는 파일 복사/붙여넣기를 지원하지 않습니다.

- 원격 세션 내에서 모든 복사/붙여넣기를 수행하려면 일반적으로(오른쪽 클릭 + 복사 또는 Ctrl+C) 복사하여 오른쪽 클릭 + 붙여넣기로 붙여넣어야 합니다(Ctrl+V는 사용할 수 없습니다).

- 원격 세션에 다음 주요 명령을 보낼 수 없음
  - Alt+Tab
  - 기능 키
  - Windows 키
  - PrtScn

### <a name="roles-and-features"></a>역할 및 기능

- 설치에 사용할 수 없는 소스를 사용하여 역할 또는 기능을 선택할 때 건너뛰게 됩니다. [12946914]

- 역할 설치 후 자동으로 다시 부팅하지 않도록 선택하면 다시 묻지 않습니다. [13098852]

- 자동으로 다시 부팅을 선택하는 경우 상태가 100%로 업데이트되기 전에 다시 부팅됩니다. [13098852]

### <a name="storage"></a>스토리지

- 하위 수준: DVD/CD/플로피 드라이브가 하위 수준에서 볼륨으로 표시되지 않습니다.

- 하위 수준: 볼륨 및 디스크에 있는 일부 속성이 하위 수준에서 사용할 수 없으므로 세부 정보 창에 알 수 없거나 비어 있는 것으로 나타납니다.

- 하위 수준: 새 볼륨을 만들 때 ReFS는 Windows 2012 및 2012 R2 컴퓨터에서 64K의 할당 단위 크기를 지원합니다. ReFS 볼륨이 하위 수준 대상에서 더 작은 할당 단위 크기로 만들어지면 파일 시스템 포맷이 실패합니다. 새 볼륨을 사용할 수 없습니다. 해결책은 볼륨을 삭제하고 64K 할당 단위 크기를 사용하는 것입니다.

### <a name="updates"></a>업데이트

- 업데이트를 설치한 후 설치 상태가 캐시 되어 브라우저 새로 고침이 필요할 수 있습니다.

- Azure 업데이트 관리를 설정 하려고 할 때 "키 집합이 존재 하지 않음" 오류가 발생할 수 있습니다. 이 경우 관리 되는 노드에서 다음 재구성 단계를 시도 하세요.
    1. ' 암호화 서비스 ' 서비스를 중지 합니다.
    2. 숨겨진 파일 (필요한 경우)을 표시 하도록 폴더 옵션을 변경 합니다.
    3. "%Allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18" 폴더를 가져오고 해당 내용을 모두 삭제 합니다.
    4. ' 암호화 서비스 ' 서비스를 다시 시작 합니다.
    5. Windows 관리 센터를 사용 하 여 업데이트 관리 설정 반복

### <a name="virtual-machines"></a>가상 컴퓨터

- Windows Server 2012 호스트에서 가상 컴퓨터를 관리 하는 경우 브라우저 내 VM 연결 도구는 VM에 연결 되지 않습니다. VM에 연결 하기 위한 .rdp 파일 다운로드는 계속 작동 해야 합니다. [20258278]

- Azure Site Recovery – WAC 외부의 호스트에서 ASR를 설정 하는 경우 WAC [18972276] 내에서 VM을 보호할 수 없습니다.

- 가상 SAN 관리자, VM 이동, VM 내보내기, VM 복제 등 Hyper-V 관리자에서 사용할 수 있는 고급 기능은 현재 지원되지 않습니다.

### <a name="virtual-switches"></a>가상 스위치

- 스위치 포함 팀(SET): 팀에 NIC을 추가할 때 팀과 NIC이 동일한 서브넷에 있어야 합니다.

## <a name="computer-management-solution"></a>컴퓨터 관리 솔루션

컴퓨터 관리 솔루션은 서버 관리자 솔루션의 도구 하위 집합을 포함하므로 동일한 알려진 문제가 적용되며 다음 특정 컴퓨터 관리 솔루션의 문제가 포함됩니다.

- Microsoft 계정 ([MSA](https://account.microsoft.com/account/))을 사용 하거나, AAD (Azure Active Directory)를 사용 하 여 Windows 10 컴퓨터에 로그온 하는 경우 "관리"를 사용 하 여 로컬 관리자 계정에 대 한 자격 증명을 제공 해야 합니다. [16568455]

- 로컬 호스트를 관리하려고 할 때 게이트웨이 프로세스의 권한을 상승하라는 메시지가 나타납니다. 다음에 나오는 사용자 계정 컨트롤 팝업에서 **아니요** 를 클릭 하는 경우 연결 시도를 취소 하 고 다시 시작 해야 합니다.

- Windows 10에는 기본적으로 WinRM/PowerShell 원격 기능이 설정 되어 있지 않습니다.
  
  - Windows 10 클라이언트의 관리를 사용하도록 설정하려면 관리자 권한 PowerShell 프롬프트에서 ```Enable-PSRemoting``` 명령을 실행해야 합니다.

  - 또한 ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any```로 방화벽을 업데이트하여 로컬 서브넷 외부에서의 연결을 허용해야 합니다. 보다 제한적인 네트워크 시나리오에 대해 [이 설명서](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1)를 참조하십시오.

## <a name="failover-cluster-manager-solution"></a>장애 조치 클러스터 관리자 솔루션

- 클러스터(하이퍼 컨버지드 또는 기존)를 관리하는 경우 **셸을 찾을 수 없음** 오류가 발생할 수 있습니다. 이런 경우 브라우저를 다시 로드하거나 다른 도구로 이동한 다음 되돌아옵니다. [13882442]

- 완전히 구성하지 않은 하위 수준(Windows Server 2012 또는 2012 R2) 클러스터를 관리할 때 문제가 발생할 수 있습니다. 이 문제를 해결하는 방법은 Windows 기능 **RSAT-클러스터링-PowerShell**이 설치되어 클러스터의 **각 구성원 노드**에서 사용하도록 설정되었는지 확인하는 것입니다. PowerShell로 이 작업을 수행하려면 모든 클러스터 노드에서 `Install-WindowsFeature -Name RSAT-Clustering-PowerShell` 명령을 입력합니다. [12524664]

- 클러스터를 올바르게 검색하려면 전체 FQDN으로 추가해야 할 수 있습니다.

- 게이트웨이로 설치된 Windows Admin Center를 사용하여 클러스터에 연결하고 명시적 사용자 이름/암호를 제공하여 인증할 때 자격 증명으로 구성원 노드를 쿼리할 수 있도록 **모든 연결에 이러한 자격 증명 사용**을 선택해야 합니다.

## <a name="hyper-converged-cluster-manager-solution"></a>하이퍼 컨버지드 클러스터 관리자 솔루션

- **드라이브 - 펌웨어 업데이트**, **서버 - 제거**, **볼륨 - 열기**와 같은 일부 명령은 사용하지 않도록 설정되며 현재 지원되지 않습니다.

## <a name="azure-services"></a>Azure 서비스

### <a name="azure-file-sync-permissions"></a>Azure File Sync 권한

Azure File Sync Windows 관리 센터에서 버전 1910 이전에 제공 하지 않은 Azure의 권한이 필요 합니다. Windows 관리 센터 버전 1910 이전 버전을 사용 하 여 Azure에 Windows 관리 센터 게이트웨이를 등록 한 경우 최신 버전의 Azure File Sync를 사용 하는 데 필요한 올바른 권한을 얻으려면 Azure Active Directory 응용 프로그램을 업데이트 해야 합니다. Windows 관리 센터. 추가 사용 권한을 통해 Azure File Sync는 [저장소 계정에 대 한 액세스 권한이 Azure File Sync 있는지 확인](https://docs.microsoft.com/azure/storage/files/storage-sync-files-troubleshoot?tabs=portal1%2Cazure-portal#tabpanel_CeZOj-G++Q-5_azure-portal)문서에 설명 된 대로 저장소 계정 액세스의 자동 구성을 수행할 수 있습니다.

Azure Active Directory 앱을 업데이트 하기 위해 다음 두 가지 중 하나를 수행할 수 있습니다.
1. **Azure** > **등록 취소** > **설정** 으로 이동한 다음 Windows 관리 센터를 azure에 다시 등록 하 여 새 Azure Active Directory 응용 프로그램을 만들도록 선택 합니다. 
2. Azure Active Directory 응용 프로그램으로 이동 하 여 Windows 관리 센터에 등록 된 기존 Azure Active Directory 앱에 필요한 사용 권한을 수동으로 추가 합니다. 이렇게 하려면 **azure에서** **azure** > View > **설정** 으로 이동 합니다. Azure의 **앱 등록** 블레이드에서 **API 권한**으로 이동 하 여 **권한 추가**를 선택 합니다. 아래로 스크롤하여 **그래프 Azure Active Directory**선택 하 고, **위임 된 권한**을 선택 하 고, **디렉터리**를 확장 하 고, **디렉터리. accessasuser**를 선택 합니다. 앱에 업데이트를 저장 하려면 **권한 추가** 를 클릭 합니다.

### <a name="options-for-setting-up-azure-management-services"></a>Azure 관리 서비스를 설정 하는 옵션

Azure Monitor, Azure 업데이트 관리 및 Azure Security Center를 포함 하는 azure 관리 서비스는 온-프레미스 서버에 대해 동일한 에이전트 (Microsoft Monitoring Agent)를 사용 합니다. Azure 업데이트 관리에는 지원 되는 지역 집합이 더 제한적 이며 Log Analytics 작업 영역을 Azure Automation 계정에 연결 해야 합니다. 이러한 제한으로 인해 Windows 관리 센터에서 여러 서비스를 설정 하려는 경우 먼저 Azure 업데이트 관리 설정 하 고 Azure Security Center 하거나 Azure Monitor 해야 합니다. Microsoft Monitoring Agent를 사용 하는 Azure 관리 서비스를 구성 하 고 Windows 관리 센터를 사용 하 여 Azure 업데이트 관리를 설정 하는 경우, Windows 관리 센터에서는 Azure 업데이트 관리 (기존 Microsoft Monitoring Agent에 연결 된 리소스는 Azure 업데이트 관리를 지원 합니다. 이 경우 두 가지 옵션이 있습니다.

1. 제어판 > Microsoft Monitoring Agent으로 이동 하 여 [기존 Azure 관리 솔루션](https://docs.microsoft.com/azure/azure-monitor/platform/log-faq#q-how-do-i-stop-an-agent-from-communicating-with-log-analytics) (예: Azure Monitor 또는 Azure Security Center)에서 서버 연결을 끊습니다. 그런 다음 Windows 관리 센터에서 Azure 업데이트 관리를 설정 합니다. 그 후에는 문제 없이 Windows 관리 센터를 통해 다른 Azure 관리 솔루션을 설정 하는 데 다시 돌아갈 수 있습니다.
2. [Azure 업데이트 관리에 필요한 azure 리소스를 수동으로 설정](https://docs.microsoft.com/azure/automation/automation-update-management) 하 고, Microsoft Monitoring Agent (Windows 관리 센터 외부)를 [수동으로 업데이트](https://docs.microsoft.com/azure/azure-monitor/platform/agent-manage#adding-or-removing-a-workspace) 하 여 사용 하려는 업데이트 관리 솔루션에 해당 하는 새 작업 영역을 추가할 수 있습니다.
