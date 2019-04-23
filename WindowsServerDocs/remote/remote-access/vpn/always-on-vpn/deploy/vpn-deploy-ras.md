---
title: Always On VPN에 대한 원격 액세스 서버 구성
description: RRAS는 라우터 및 원격 액세스 서버를 모두 수행 하도록 합니다. 따라서 다양 한 기능을 지원합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: a338ddfec1ed5cd0e9198f64dc4952eb591cdc1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829674"
---
# <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>3단계. Always On VPN에 대한 원격 액세스 서버 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** 2단계. Server 인프라 구성](vpn-deploy-server-infrastructure.md)<br>
&#187;  [**이전:** 4단계. 설치 및 구성 (NPS (네트워크 정책 서버)](vpn-deploy-nps.md)


RRAS는 다양 한 기능을 지원 하기 때문에 라우터 및 원격 액세스 서버를 모두 수행 하도록 설계 되었습니다. 이 배포에서는 이러한 기능 중 일부만 필요: IKEv2 VPN 연결 및 LAN 라우팅에 대 한 지원.

IKEv2 VPN 터널링 프로토콜 주석 7296에 대 한 Internet Engineering Task Force 요청에 설명 된 경우 IKEv2의 주요 이점은 기본 네트워크 연결에서 중단을 허용 하는 경우 예를 들어 연결이 일시적으로 끊어진 경우 또는 사용자 클라이언트 컴퓨터 하나의 네트워크에서 다른 위치로 이동 하는 경우 IKEv2를 자동으로 복원 VPN 연결 네트워크 다시 연결이 되 면, 사용자 개입 없이 합니다.

서버의 보안 공간을 줄일 수는 사용 되지 않는 프로토콜을 해제 하는 동안 IKEv2 연결을 지원 하려면 RRAS 서버를 구성 합니다. 또한 고정 주소 풀에서 주소를 VPN 클라이언트를 할당 하는 서버를 구성 합니다. DHCP 서버 또는 풀에서 주소를 적절히 할당할 수 있습니다. 그러나 DHCP 서버를 사용 하 여 디자인에 복잡성이 추가 및 최소한의 이점을 제공 합니다.


>[!Important]
>고려해 야 합니다.
>- 실제 서버에 두 개의 이더넷 네트워크 어댑터를 설치 합니다. 두 개의 외부 가상 스위치를 각 실제 네트워크 어댑터에 대해 하나씩 만들어야 VPN 서버를 설치 하는 VM의 경우 한 다음 VM에 대해 하나의 가상 스위치에 연결 된 각 네트워크 어댑터를 사용 하 여 두 가상 네트워크 어댑터를 만듭니다.
>
>- 외부 경계 네트워크에 연결 된 하나의 네트워크 어댑터 및 내부 경계 네트워크에 연결 된 하나의 네트워크 어댑터를 사용 하 여 가장자리 사이의 내부 방화벽, 경계 네트워크에서 서버를 설치 합니다.


>[!Warning]
>시작 하기 전에 VPN 서버에서 IPv6을 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 없습니다 하 고 오류 메시지가 표시 됩니다.

## <a name="install-remote-access-as-a-ras-gateway-vpn-server"></a>RAS 게이트웨이 VPN 서버로 원격 액세스 설치

이 절차에서는 단일 테 넌 트 RAS 게이트웨이 VPN 서버로 원격 액세스 역할을 설치 합니다. 자세한 내용은 [원격 액세스](../../../Remote-Access.md)를 참조하세요.


### <a name="install-the-remote-access-role-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 원격 액세스 역할을 설치 합니다.

1. 로 Windows PowerShell을 엽니다 **관리자**합니다.

2. 다음 명령 및 키를 눌러 입력 **ENTER**:

   `Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools`

   설치가 완료 되 면 Windows PowerShell에서 다음과 같은 메시지가 나타납니다.
    
   | 성공 | 다시 시작 필요 | 종료 코드 | 기능 결과                             |
   |---------|----------------|-----------|--------------------------------------------|
   | True    | 아니오             | 성공   | {RAS 연결 관리자 관리 키트 |
   ---

### <a name="install-the-remote-access-role-by-using-server-manager"></a>서버 관리자를 사용 하 여 원격 액세스 역할 설치

서버 관리자를 사용 하 여 원격 액세스 역할을 설치 하려면 다음 절차를 사용할 수 있습니다.

1.  VPN 서버의 서버 관리자에서 클릭 **관리** 누릅니다 **역할 및 기능 추가**합니다. <p>역할 및 기능 추가 마법사가 열립니다.

2.  앞에 페이지 시작 하면,이 클릭 **다음**합니다.

3.  설치 유형 선택 페이지에서 선택 합니다 **역할 기반 또는 기능 기반 설치** 옵션을 클릭 **다음**합니다.

4.  선택 대상 서버 페이지에서 선택 합니다 **서버 풀에서 서버 선택** 옵션입니다.

5.  서버 풀에서 로컬 컴퓨터를 선택 하 고 클릭 **다음**합니다.

6.  Select 서버 역할 페이지에서 **역할**, 클릭 **원격 액세스**를 차례로 **다음**합니다.

7.  기능 선택 페이지에서 **다음**을 클릭합니다.

8.  원격 액세스 페이지에서 클릭 **다음**합니다.

9.  역할 선택 서비스 페이지에서 **역할 서비스**, 클릭 **DirectAccess 및 VPN (RAS)** 합니다.<p>**역할 및 추가 기능 마법사** 대화 상자가 열립니다.

10. 역할 및 기능 추가 대화 상자에서 클릭 **기능 추가** 누릅니다 **다음**합니다.

11. 웹 서버 역할 (IIS) 페이지에서 클릭 **다음**합니다.

12. 역할 선택 서비스 페이지에서 클릭 **다음**합니다.

13. 설치 선택 확인 페이지에서 선택 내용을 검토 하 고 클릭 **설치**합니다.

14. 설치가 완료되면 **닫기**를 클릭합니다.

## <a name="configure-remote-access-as-a-vpn-server"></a>VPN 서버로 원격 액세스를 구성 합니다.

이 섹션에서는 IKEv2 VPN 연결을 허용, 다른 VPN 프로토콜에서 연결을 거부, 권한 있는 VPN 클라이언트 연결 IP 주소를 발급 하기 위한 정적 IP 주소 풀을 할당 하는 원격 액세스 VPN을 구성할 수 있습니다.

1.  VPN 서버의 서버 관리자에서 클릭 합니다 **알림을** 플래그입니다.

2.  에 **태스크** 메뉴에서 클릭 **시작 마법사를 엽니다**합니다.<p>원격 액세스 구성 마법사가 열립니다. 

    >[!NOTE] 
    >원격 액세스 구성 마법사를 Server Manager 뒤에 있는 열릴 수 있습니다. 생각 하는 경우 마법사는 열기, 이동 또는 숨김 마법사 인지 확인 하려면 서버 관리자를 최소화 하려면 너무 오래 걸립니다. 그렇지 않은 경우 마법사 초기화 될 때까지 기다립니다.

3.  클릭 **VPN만 배포**합니다.<p>라우팅 및 원격 액세스 관리 콘솔 MMC (Microsoft)가 열립니다.

4.  VPN 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **구성 및 라우팅 및 원격 액세스 사용**합니다.<p>라우팅 및 원격 액세스 서버 설치 마법사가 열립니다.

5.  라우팅 및 원격 액세스 서버 설치 마법사를 시작, 클릭 **다음**합니다.

6.  **Configuration**, 클릭 **사용자 지정 구성**를 클릭 하 고 **다음**합니다.

7.  **사용자 지정 구성을**, 클릭 **VPN 액세스**를 클릭 하 고 **다음**합니다.<p>완료 라우팅 및 원격 액세스 서버 설치 마법사가 열립니다.

8.  클릭 **완료할** 마법사를 닫고 클릭 **확인** 라우팅 및 원격 액세스 대화 상자를 닫습니다.

9.  클릭 **서비스를 시작** 원격 액세스를 시작 합니다.

10. 원격 액세스 mmc에서 VPN 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.

11. 속성을 클릭 합니다 **보안** 탭 하 고 실행 합니다.

    a. 클릭 **인증 공급자** 누릅니다 **RADIUS 인증**합니다.
    
    b. 클릭 **구성**합니다.<p>RADIUS 인증 대화 상자가 열립니다.
    
    다. **추가**를 클릭합니다.<p>RADIUS 서버 추가 대화 상자가 열립니다.
    
    d. **서버 이름**, 조직/회사 네트워크에 완전히 정규화 된 도메인 이름 (FQDN) NPS 서버를 입력 합니다.<p>NPS 서버의 NetBIOS 이름이 NPS1 도메인 이름이 corp.contoso.com 인 경우 입력 하는 예를 들어 **NPS1.corp.contoso.com**합니다.
    
    e. **공유 비밀**, 클릭 **변경**합니다.<p>암호 변경 대화 상자가 열립니다.
    
    f. **새 암호**, 텍스트 문자열을 입력 합니다.
    
    g. **새 암호 확인**동일한 텍스트 문자열을 입력 하 고 클릭 **확인**합니다.

    >[!IMPORTANT] 
    >이 텍스트 문자열을 저장 합니다. 조직/회사 네트워크의 NPS 서버를 구성한 경우이 VPN 서버를 RADIUS 클라이언트로 추가 합니다. 이 구성에서는 사용 하 여이 동일한 공유 암호 NPS 및 VPN 서버에서 통신할 수 있도록 합니다.

12. **RADIUS 서버 추가**에 대 한 기본 설정을 검토 합니다.

    - **Time-out**
    
    - **점수**
    
    - **포트**

13. 필요한 경우 사용자 환경 및 클릭에 대 한 요구 사항에 맞게 값을 변경 **확인**합니다.<p>NAS에는 일정 수준의 더 큰 네트워크에 대 한 액세스를 제공 하는 장치입니다. RADIUS 인프라를 사용 하 여 NAS RADIUS 클라이언트를 인증, 권한 부여에 대 한 RADIUS 서버로 연결 요청 및 계정 메시지를 전송 및 계정 이기도 합니다.

14. 에 대 한 설정을 검토 **계정 공급자**:

    | 원하는 경우 여는 중...  | 발생하는 결과             |
    |---------------------|-------------------|
    | 원격 액세스 서버에 로그온 하는 원격 액세스 활동 | 했는지 **Windows 계정** 을 선택 합니다.      |
    | VPN에 대 한 계정 서비스를 수행 하는 NPS   | 변경 **계정 공급자** 하 **RADIUS 계정** 선택한 다음 계정 공급자를 NPS를 구성 합니다. |
    ---

15. 클릭 합니다 **IPv4** 탭 하 고 실행 합니다.

    a. 클릭 **고정 주소 풀**합니다.
    
    b. 클릭 **추가** IP 주소 풀을 구성 합니다.<p>고정 주소 풀 내부 경계 네트워크의 주소를 포함 해야 합니다. 이러한 주소는 VPN 서버의 회사 네트워크가 아니라 내부 전용 네트워크 연결 합니다.
    
    다. **시작 IP 주소**, VPN 클라이언트에 할당 하려는 범위 시작 IP 주소를 입력 합니다.
    
    d. **끝 IP 주소**, 또는 VPN 클라이언트에 할당 하려는 범위 끝 IP 주소를 입력 **주소 수가**를 사용할 수 있도록 하려는 주소를 입력 합니다. DHCP를 사용 하 여이 서브넷에 대 한 경우에 DHCP 서버에서 해당 주소 제외를 구성 하는 확인 합니다.
    
    e. (선택 사항) DHCP를 사용 하는 경우 클릭 **어댑터**, 결과 목록에서 내부 경계 네트워크에 연결 되는 이더넷 어댑터를 클릭 합니다.

16. (선택 사항) *VPN 연결에 대 한 조건부 액세스를 구성 하는 경우*에서 **인증서** 드롭 다운 목록의 **SSL 인증서 바인딩**를 VPN 서버를 선택 합니다. 인증 합니다.

17. (선택 사항) *VPN 연결에 대 한 조건부 액세스를 구성 하는 경우*, NPS MMC에서 확장 **정책을\\네트워크 정책** 하 고 실행 합니다. 

    a. 오른쪽의 **Microsoft 라우팅 및 원격 액세스 서버에 연결** 선택한 네트워크 정책 **속성**합니다.
    
    b. 선택 된 **액세스 권한을 부여 합니다. 연결 요청에이 정책과 일치 하는 경우 액세스 권한을 부여** 옵션입니다.
    
    다. 네트워크 액세스 서버 유형 선택 **원격 액세스 서버 (VPN 전화 접속)** 드롭다운 목록에서.

3.  라우팅 및 원격 액세스 MMC를 마우스 오른쪽 단추로 클릭 **포트** 을 클릭 한 다음 **속성**합니다. <p>포트 속성 대화 상자가 열립니다.

4.  클릭 **WAN 미니 포트 (SSTP)** 누릅니다 **구성**합니다. 장치 구성-WAN 미니 포트 (SSTP) 대화 상자가 열립니다.

    a. 선택을 취소 합니다 **원격 액세스 연결 (인바운드 전용)** 하 고 **필요 시 전화 접속 라우팅 연결 (인바운드 및 아웃 바운드)** 확인란 합니다.
    
    b. **확인**을 클릭합니다.

5.  클릭 **WAN 미니 포트 (l2tp)** 누릅니다 **구성**합니다. 장치 구성-WAN 미니 포트 (L2TP) 대화 상자가 열립니다.

    a. **최대 포트**를 지원 하 고 동시 VPN 연결의 최대 수와 일치 하는 포트 번호를 입력 합니다.
    
    b. **확인**을 클릭합니다.

6.  클릭 **WAN 미니 포트 (PPTP)** 누릅니다 **구성**합니다. 장치 구성-WAN 미니 포트 (PPTP) 대화 상자가 열립니다.

    a. **최대 포트**를 지원 하 고 동시 VPN 연결의 최대 수와 일치 하는 포트 번호를 입력 합니다.
    
    b. **확인**을 클릭합니다.
    
7. 클릭 **WAN 미니 포트 (IKEv2)** 누릅니다 **구성**합니다. 장치 구성-WAN 미니 포트 (IKEv2) 대화 상자가 열립니다.

    a. **최대 포트**를 지원 하 고 동시 VPN 연결의 최대 수와 일치 하는 포트 번호를 입력 합니다.
    
    b. **확인**을 클릭합니다.

7.  메시지가 표시 되 면 클릭 **예** 고 서버를 다시 시작을 확인 하려면 **닫기** 서버 다시 시작 합니다.

## <a name="next-step"></a>다음 단계
[4 단계입니다. 설치 및 구성 (NPS (네트워크 정책 서버)](vpn-deploy-nps.md): 이 단계에서는 Windows PowerShell 또는 서버 관리자 추가 역할 및 기능 마법사 중 하나를 사용 하 여 네트워크 정책 (NPS 서버)를 설치 합니다. 모든 인증, 권한 부여 및 연결에 대 한 회계 업무를 처리 하는 NPS를 구성할 수도 있습니다는 VPN 서버에서 수신한 요청 합니다.





---