---
title: Windows 인증에서 자격 증명 프로세스
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48c60816-fb8b-447c-9c8e-800c2e05b14f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 52d50a1bb6bfbe9d35146f362a2a5184df0a6504
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839864"
---
# <a name="credentials-processes-in-windows-authentication"></a>Windows 인증에서 자격 증명 프로세스

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 참조 항목에서는 Windows 인증 자격 증명을 처리 하는 방법을 설명 합니다.

Windows 자격 증명 관리는 사용 되는 운영 체제 서비스 또는 사용자의 자격 증명을 받는 및 향후 프레젠테이션 인증 대상에 대 한 정보를 보호 하는 프로세스입니다. 도메인에 가입 된 컴퓨터의 경우 인증 대상 도메인 컨트롤러입니다. 인증에 사용 된 자격 증명에는 일종의 인증서, 암호 또는 PIN 같은 신뢰성을 증명 하는 사용자의 id를 연결 하는 디지털 문서입니다.

기본적으로 Windows 자격 증명을 Winlogon 서비스를 통해 도메인에 가입 된 컴퓨터에서 Active Directory 또는 로컬 컴퓨터의 보안 계정 관리자 (SAM) 데이터베이스에 대해 유효성이 검사 됩니다. 자격 증명 로그온 사용자 인터페이스 또는 프로그래밍 방식으로 API (응용 프로그래밍 인터페이스) 인증 대상에 게 표시할을 통해 사용자 입력을 통해 수집 됩니다.

로컬 보안 정보는 레지스트리의 아래에 저장 됩니다 **HKEY_LOCAL_MACHINE\SECURITY**합니다. 저장 된 정보에는 정책 설정, 기본 보안 값 및 캐시 된 로그온 자격 증명과 같은 계정 정보를 포함합니다. 또한 SAM 데이터베이스의 복사본 쓰기 금지 되어 있지만 여기에 저장 됩니다.

다음 다이어그램은 사용자 또는 프로세스는 성공적인 로그온에 대 한 인증 자격 증명 시스템을 통해 수행 필요한 구성 요소 및 경로 보여줍니다.

![필요한 구성 요소를 보여 주는 다이어그램 및 사용자 또는 프로세스는 성공적인 로그온에 대 한 인증 자격 증명 시스템을 통해 수행 하는 경로입니다.](../media/credentials-processes-in-windows-authentication/AuthN_LSA_Architecture_Client.gif)

다음 표에서 로그온 시 인증 프로세스에서 자격 증명을 관리 하는 각 구성 요소를 설명 합니다.

**모든 시스템에 대 한 인증 구성 요소**

|구성 요소|설명|
|-------|--------|
|사용자 로그온|Winlogon.exe 파일이 실행 보안 사용자 상호 작용을 관리 하는 일을 담당 합니다. Winlogon 서비스 전용 Secur32.dll 통해 로컬 보안 기관 (LSA)를 보안 된 데스크톱 (로그온 UI)에서 사용자 동작으로 수집 하는 자격 증명을 전달 하 여 Windows 운영 체제에 대 한 로그온 프로세스를 시작 합니다.|
|응용 프로그램에 로그온|응용 프로그램 또는 대화형 로그온 하지 않아도 되는 서비스 로그온 합니다. 대부분의 사용자가 시작한 프로세스 Ksecdd.sys를 사용 하 여 커널 모드에서 서비스와 같은 시작 시 시작 하는 프로세스를 실행 하는 반면 Secur32.dll을 사용 하 여 사용자 모드에서 실행 합니다.<br /><br />사용자 모드와 커널 모드에 대 한 자세한 내용은이 항목의 응용 프로그램 및 사용자 모드 또는 서비스 및 커널 모드를 참조 합니다.|
|Secur32.dll|인증 프로세스의 기초를 형성 하는 여러 인증 공급자입니다.|
|Lsasrv.dll|LSA 서버 서비스에서 보안 정책을 적용 및 LSA에 대 한 보안 패키지 관리자 역할을 하는입니다. LSA는 프로토콜 성공 하는 것을 확인 한 후 NTLM 또는 Kerberos 프로토콜을 선택 하는 협상 함수를 포함 합니다.|
|보안 지원 공급자|집합 하나 이상의 인증 프로토콜을 개별적으로 호출할 수 있는 공급자입니다. 각 버전의 Windows 운영 체제를 사용 하 여 공급자의 기본 집합을 변경 하 고 사용자 지정 공급자를 작성할 수 있습니다.|
|Netlogon.dll|Net Logon 서비스가 수행 하는 서비스는 다음과 같습니다.<br /><br />-컴퓨터의 보안 채널 (필요가 Schannel을 함께 혼동)을 도메인 컨트롤러 유지 관리 합니다.<br />-도메인 컨트롤러에 보안 채널을 통해 사용자의 자격 증명을 전달 하 고 사용자에 대 한 사용자 권한을 확인 하 고 도메인 Sid (보안 식별자)를 반환 합니다.<br />-게시 서비스 리소스 레코드에서 도메인 이름 시스템 (DNS) 하 고 DNS를 사용 하 여 도메인 컨트롤러의 IP (인터넷 프로토콜) 주소 이름을 확인 하도록 합니다.<br />-주 도메인 컨트롤러 (Pdc)와 백업 도메인 컨트롤러 (Bdc)를 동기화 하는 것에 대 한 원격 프로시저 호출 (RPC)에 따라 복제 프로토콜을 구현 합니다.|
|Samsrv.dll|보안 계정 관리자 (SAM), 보안 로컬 계정에 저장 하는 로컬에 저장 된 정책을 적용 하 고 Api를 지원 합니다.|
|레지스트리|레지스트리는 SAM 데이터베이스, 로컬 보안 정책 설정, 기본 보안 값 및 계정 정보 시스템에 액세스할 수 있는 복사본을 포함 합니다.|

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

-   [사용자 로그온에 대 한 자격 증명 입력](#BKMK_CrentialInputForUserLogon)

-   [응용 프로그램 및 서비스 로그온 자격 증명 입력](#BKMK_CredentialInputForApplicationAndServiceLogon)

-   [로컬 보안 기관](#BKMK_LSA)

-   [캐시 된 자격 증명 및 유효성 검사](#BKMK_CachedCredentialsAndValidation)

-   [자격 증명 저장 및 유효성 검사](#BKMK_CredentialStorageAndValidation)

-   [보안 계정 관리자 데이터베이스](#BKMK_SAM)

-   [로컬 도메인 및 트러스트 된 도메인](#BKMK_LocalDomainsAndTrustedDomains)

-   [Windows 인증에 인증서](#BKMK_CertificatesInWindowsAuthentication)

## <a name="BKMK_CrentialInputForUserLogon"></a>사용자 로그온에 대 한 자격 증명 입력
Windows Server 2008 및 Windows Vista에서는 Graphical Identification and Authentication (GINA) 아키텍처는 로그온 타일 사용 하 여 다른 로그온 유형을 열거 수 있게 하는 자격 증명 공급자 모델을 사용 하 여 대체 되었습니다. 두 모델에 대 한 설명은 다음과 같습니다.

**그래픽 식별 및 인증 아키텍처**

Graphical Identification and Authentication (GINA) 아키텍처는 Windows Server 2003, Microsoft Windows 2000 Server, Windows XP 및 Windows 2000 Professional 운영 체제에 적용 됩니다. 이러한 시스템에서 모든 대화형 로그온 세션 Winlogon 서비스 전용의 별도 인스턴스를 만듭니다. GINA 아키텍처는 Winlogon에 의해 사용 된 프로세스 공간에 로드, 수신 및 자격 증명을 처리 하는 인 lsalogonuser가 통해 인증 인터페이스를 호출 합니다.

대화형 로그온에 Winlogon 인스턴스가 세션 0에서에서 실행 합니다. 시스템 서비스를 호스트 하는 세션 0 및 로컬 보안 기관 (LSA) 프로세스를 비롯 한 다른 중요 한 프로세스입니다.

다음 다이어그램은 Windows Server 2003, Microsoft Windows 2000 Server, Windows XP 및 Microsoft Windows 2000 Professional에 대 한 자격 증명 프로세스를 보여줍니다.

![Windows Server 2003, Microsoft Windows 2000 Server, Windows XP 및 Microsoft Windows 2000 Professional에 대 한 자격 증명 프로세스를 보여 주는 다이어그램](../media/credentials-processes-in-windows-authentication/AuthN_GINA_Architecture.gif)

**자격 증명 공급자 아키텍처**

자격 증명 공급자 아키텍처에서 지정 된 버전에 적용 됩니다는 **적용 대상** 이 항목의 시작 부분에 있는 목록입니다. 이러한 시스템에서 자격 증명 공급자를 사용 하 여 자격 증명 입력된 아키텍처를 확장할 수 있는 디자인 변경 합니다. 이러한 공급자 개수에 관계 없이 동일한 사용자 및 암호, 스마트 카드 생체 인식 등의 다양 한 인증 방법에 대 한 서로 다른 계정 로그온 시나리오를 허용 하는 보안 된 데스크톱에서 다른 로그온 타일이 표시 됩니다.

자격 증명 공급자 아키텍처를 사용 하 여 Winlogon 항상 시작 로그온 UI 안전 주의 시퀀스 이벤트를 받은 후 합니다. 로그온 UI는 다른 자격 증명 형식 열거 하는 공급자가 구성 수에 대 한 각 자격 증명 공급자를 쿼리 합니다. 자격 증명 공급자는 기본적으로 이러한 타일 중 하나를 지정 하는 옵션이 있습니다. 모든 공급자가 해당 타일 열거 한 후 로그온 UI를 사용자에 게 표시 합니다. 자격 증명을 제공 하는 타일을 사용 하 여 사용자 상호 작용 합니다. 로그온 UI에 이러한 자격 증명 인증을 위해 제출합니다.

자격 증명 공급자 적용 메커니즘 않습니다. 수집 하 고 자격 증명을 직렬화에 사용 됩니다. 로컬 보안 기관 및 인증 패키지를 보안을 적용 합니다.

자격 증명 공급자는 컴퓨터에 등록 된 되며 다음 작업을 수행 합니다.

-   인증에 필요한 자격 증명 정보를 설명 합니다.

-   통신 및 외부 인증 기관 사용 하 여 논리를 처리 합니다.

-   패키징 자격 증명에 대 한 대화형 및 네트워크 로그온입니다.

패키징 자격 증명에 대 한 대화형 및 serialization 프로세스를 포함 하는 네트워크 로그온입니다. 자격 증명을 직렬화 하 여 여러 로그온 타일 로그온 UI에 표시할 수 있습니다. 따라서 조직 사용자가 로그온에 대 한 대상 시스템, 네트워크 및 워크스테이션을 잠갔다가 잠금을 정책-사용자 지정된 자격 증명 공급자를 사용 하 여 사전 로그온 액세스 등 로그온 표시를 제어할 수 있습니다. 여러 자격 증명 공급자는 동일한 컴퓨터에 공존할 수 있습니다.

표준 자격 증명 공급자로 또는 사전 로그온 액세스 공급자로 단일의 로그온 (SSO) 공급자를 개발할 수 있습니다.

Windows의 각 버전에는 하나의 기본 자격 증명 공급자 및 하나의 기본 사전으로 로그온 액세스 포함 되어 공급자 PLAP (), SSO 공급자 라고도 합니다. SSO 공급자는 사용자가 로컬 컴퓨터에 로그온 하기 전에 네트워크를 연결할 수 있도록 허용 합니다. 이 공급자가 구현 되는 경우 공급자는 로그온 UI 타일을 열거 하지 않습니다.

다음 시나리오에 사용할 SSO 공급자 것:

-   **네트워크 인증 및 컴퓨터 로그온 다른 자격 증명 공급자에 의해 처리 됩니다.** 변형이 시나리오는 다음과 같습니다.

    -   사용자는 컴퓨터에 로그온 하기 전에 가상 사설망 (VPN)에 연결 하는 같은 네트워크에 연결할 수 있지만이 연결을 만들 필요가 없습니다.

    -   로컬 컴퓨터의 대화형 인증 중에 사용 되는 정보를 검색 하려면 네트워크 인증이 필요 합니다.

    -   여러 네트워크 인증 뒤에 다른 시나리오 중 하나입니다. 예를 들어, 사용자 (ISP) 인터넷 서비스 공급자가 인증, 인증 하는 VPN 및를 사용 하 여 사용자 계정 자격 증명 로그온 로컬로

    -   캐시 된 자격 증명은 사용 하지 않도록 설정 하 고 사용자 인증을 위해 로컬 로그온 하기 전에 VPN 통해 원격 액세스 서비스 연결 해야 합니다.

    -   도메인 사용자는 도메인에 가입 된 컴퓨터에 설치 하는 로컬 계정이 없는 및 대화형 로그온을 완료 하기 전에 VPN 연결을 통해 원격 액세스 서비스 연결을 설정 해야 합니다.

-   **네트워크 인증 및 컴퓨터 로그온 동일한 자격 증명 공급자에 의해 처리 됩니다.** 이 시나리오에서는 사용자가 컴퓨터에 로그온 하기 전에 네트워크에 연결 해야 합니다.

**로그온 타일 열거형**

자격 증명 공급자는 다음과 같은 경우 로그온 타일 열거:

-   에 지정 된 이러한 운영 체제는 **에 적용 됩니다** 이 항목의 시작 부분에 있는 목록입니다.

-   자격 증명 공급자를 워크스테이션 로그온에 대 한 타일을 열거합니다. 자격 증명 공급자는 일반적으로 로컬 보안 기관에 인증을 위한 자격 증명을 serialize합니다. 이 프로세스는 각 사용자의 대상 시스템에 각 사용자에 대 한 구체적이 고 특정 타일을 표시합니다.

-   로그온 및 인증 아키텍처는 사용자를 자격 증명 공급자가 열거 하는 타일을 사용 하 여 워크스테이션을 잠금 해제할 수 있습니다. 일반적으로 현재 로그인 한 사용자가 있는 기본 타일을 하지만 둘 이상의 사용자가 로그온 하 고, 다양 한 타일이 표시 됩니다.

-   자격 증명 공급자가 암호 또는 PIN 같은 기타 개인 정보를 변경 하는 사용자 요청에 대 한 응답에서 타일을 열거 합니다. 일반적으로 현재 로그온 한 사용자는 기본 타일입니다. 그러나 둘 이상의 사용자가 로그온 하 고, 다양 한 타일이 표시 됩니다.

-   자격 증명 공급자는 원격 컴퓨터에서 인증에 사용할 직렬화 된 자격 증명에 따라 타일을 열거 합니다. 자격 증명 UI 로그온 UI, 워크스테이션 잠금 해제 또는 암호 변경으로 공급자의 동일한 인스턴스를 사용 하지 않습니다. 따라서 상태 정보가 공급자 자격 증명 UI의 인스턴스 사이에서 유지 관리할 수 없습니다. 이 구조는 자격 증명을 올바르게 serialize 된 경우 각 원격 컴퓨터 로그온에 대해 하나의 타일로 발생 합니다. 이 시나리오에서 계정 컨트롤 (UAC (사용자), 컴퓨터의 작업에 잠재적으로 영향을 줄 수 있는 작업을 허용 하기 전에 사용 권한이 나 관리자 암호를 사용자에 게 컴퓨터에 무단된 변경을 방지 하는 데 도움이 되는 에서도 또는 컴퓨터의 다른 사용자에 영향을 주는 설정을 변경할 수는 있습니다.

다음 다이어그램에 지정 된 운영 체제에 대 한 자격 증명 프로세스를 보여 줍니다.는 **적용 대상** 이 항목의 시작 부분에 있는 목록입니다.

![지정 된 운영 체제에 대 한 자격 증명 프로세스를 보여 주는 다이어그램은 * *에 적용 됩니다. * *이 항목의 시작 부분에 있는 목록](../media/credentials-processes-in-windows-authentication/AuthN_CredMan_CredProv.gif)

## <a name="BKMK_CredentialInputForApplicationAndServiceLogon"></a>응용 프로그램 및 서비스 로그온 자격 증명 입력
Windows 인증 사용자 상호 작용 하지 않아도 되는 서비스나 응용 프로그램에 대 한 자격 증명을 관리 하도록 설계 되었습니다. 사용자 모드에서 응용 프로그램은 시스템 리소스에 액세스할 수, 서비스 수에 무제한 액세스할 수는 시스템 메모리와 외부 장치 동안 기준으로 제한 됩니다.

시스템 서비스 전송 수준 응용 프로그램 액세스 및 보안 지원 공급자 (SSP) 보안 지원 공급자 인터페이스 (SSPI)를 통해 시스템에서 사용할 수 있는 보안 패키지를 열거 하는 것에 대 한 함수를 제공 하는 Windows에서 선택 하는 패키지 및 해당 패키지를 사용 하 여 인증된 된 연결을 가져옵니다.

클라이언트/서버 연결을 인증 하면:

-   연결의 클라이언트 쪽 응용 프로그램의 SSPI 함수를 사용 하 여 서버에 자격 증명을 보낼 `InitializeSecurityContext (General)`합니다.

-   SSPI 함수를 사용 하 여 연결의 서버 쪽에서 응용 프로그램 응답 `AcceptSecurityContext (General)`합니다.

-   SSPI 함수 `InitializeSecurityContext (General)` 고 `AcceptSecurityContext (General)` 성공 또는 실패 인증에 필요한 인증 메시지를 모두가 교환 될 때까지 반복 됩니다.

-   연결이 인증 된 후 LSA 서버에서 액세스 토큰을 포함 하는 보안 컨텍스트를 작성 하는 클라이언트에서 정보를 사용 합니다.

-   서버는 SSPI 함수를 호출할 수 있습니다 `ImpersonateSecurityContext` 액세스 토큰을 서비스에 대 한 가장 스레드를 연결할 수 있습니다.

**응용 프로그램 및 사용자 모드**

Windows의 사용자 모드는 적절 한 커널 모드 드라이버 I/O 요청을 전달할 수 있는 두 시스템의 구성 됩니다: 다양 한 운영 체제에 대해 작성 된 응용 프로그램을 실행 하는 환경 시스템과 작동 하는 정수 계열 시스템 환경 시스템 대신 시스템 관련 기능입니다.

정수 계열 시스템 환경 시스템 대신 운영 system'specific 기능을 관리 하 고 보안 시스템 프로세스 (LSA), 워크스테이션 서비스 및 server 서비스를 구성 합니다. 보안 시스템 프로세스를 보안 토큰을 사용 하 여 처리, 부여 또는 리소스 사용 권한을 기반으로 하는 사용자 계정에 액세스 하려면 사용 권한을 거부, 로그온 요청을 처리 하 고 로그온 인증을 시작 및 운영 체제는 시스템 리소스를 결정 감사 해야 합니다.

응용 프로그램은 응용 프로그램이 로컬 시스템 (SYSTEM)의 보안 컨텍스트에서 비롯 한 모든 주체로 실행할 수 있는 사용자 모드에서 실행할 수 있습니다. 응용 프로그램 실행할 수도 커널 모드에서 로컬 시스템 (SYSTEM)의 보안 컨텍스트에서 응용 프로그램 실행할 수 있습니다.

SSPI 인증, 메시지 무결성 및 메시지 개인 정보 보호에 대 한 통합된 보안 서비스를 가져오는 데 사용 되는 API가 Secur32.dll 모듈을 통해 제공 됩니다. 응용 프로그램 수준 프로토콜 및 보안 프로토콜 간에 추상화 계층을 제공합니다. SSPI는 다양 한 인증을 포함 하는 동적 연결 라이브러리 (Dll)를 액세스 하는 방법도 제공 서로 다른 응용 프로그램 식별 하거나 사용자를 인증 하는 네트워크를 통해 이동할 때 데이터를 암호화 하는 여러 가지는 여러 가지를 되어야 하므로 및 암호화 기능을 추가 합니다. 이러한 Dll 보안 지원 공급자 (Ssp) 라고 합니다.

관리 서비스 계정 및 가상 계정 자체 도메인 계정의 격리를 사용 하 여 Microsoft SQL Server 및 인터넷 정보 서비스 (IIS)와 같은 중요 한 응용 프로그램을 제공 하는 Windows Server 2008 R2 및 Windows 7에 도입 하는 동안 이러한 계정에 대 한 자격 증명 및 서비스 주체 이름 (SPN)을 수동으로 관리 하려면 관리자에 대 한 필요를 제거 합니다. 이러한 기능 및 인증에서 해당 역할에 대 한 자세한 내용은 참조 하세요. [관리 서비스 계정 설명서에 대 한 Windows 7 및 Windows Server 2008 R2](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx) 고 [그룹 관리 서비스 계정 개요](../group-managed-service-accounts/group-managed-service-accounts-overview.md).

**서비스 및 커널 모드**

대부분의 Windows 응용 프로그램을 시작 하는 사용자의 보안 컨텍스트에서 실행 하는 경우에 서비스는 그렇지 않습니다. 네트워크 및 인쇄 서비스와 같은 많은 Windows 서비스는 사용자가 컴퓨터를 시작 하는 경우 서비스 컨트롤러에 의해 시작 됩니다. 이러한 서비스는 로컬 서비스 또는 로컬 시스템으로 실행 될 수 있습니다 하 고 마지막 사용자 로그 오프 한 후 실행 계속 될 수 있습니다.

> [!NOTE]
> 서비스는 일반적으로 로컬 시스템 (SYSTEM), Network Service 또는 Local Service 라고 하는 보안 컨텍스트에서 실행 합니다.  Windows Server 2008 R2 도메인 보안 주체는 관리 되는 서비스 계정으로 실행 되는 서비스를 도입 합니다.

서비스를 시작 하기 전에 서비스 컨트롤러 서비스에 지정 되 고 다음 LSA 통해 인증 서비스의 자격 증명을 제공 하는 계정을 사용 하 여 로그온 합니다. Windows 서비스에 서비스 제어 관리자 서비스를 제어 하는 데 사용할 수 있는 프로그래밍 인터페이스를 구현 합니다. 시스템 시작 될 때 또는 수동으로 서비스 제어 프로그램을 사용 하 여 Windows 서비스를 자동으로 시작할 수 있습니다. 예를 들어, Windows 클라이언트 컴퓨터를 도메인에 가입 메신저 서비스 컴퓨터의 도메인 컨트롤러에 연결 하 고 보안 채널에 열립니다. 인증된 된 연결을 가져오려면 서비스에 원격 컴퓨터의 로컬 보안 기관 (LSA)에서 신뢰 하는 자격 증명이 있어야 합니다. 네트워크의 다른 컴퓨터와 통신 하는 경우 LSA 로컬 시스템 및 네트워크 서비스의 보안 컨텍스트에서 실행 되는 다른 모든 서비스와 마찬가지로 로컬 컴퓨터의 도메인 계정에 대 한 자격 증명을 사용 합니다. 로컬 컴퓨터에서 서비스 자격 증명이 LSA에 게 표시 하지 않아도 되므로 시스템으로 실행 합니다.

Ksecdd.sys 파일 관리 되어 이러한 자격 증명을 암호화 하 고 LSA로 로컬 프로시저 호출을 사용 합니다. 파일 형식 (드라이버) DRV 이며 커널 모드 보안 지원 공급자 (SSP)으로 및에서 지정 된 버전 이라고 합니다 **에 적용 됩니다.** 는 FIPS 140-2 수준 1 규격,이 항목의 시작 부분에 나열 합니다.

커널 모드는 컴퓨터의 하드웨어 및 시스템 리소스에 대 한 전체 액세스 합니다. 사용자 모드 서비스 및 응용 프로그램에 대 한 액세스 하지 않아야 하는 운영 체제의 중요 한 영역에 액세스 하지 못하도록 커널 모드를 중지 합니다.

## <a name="BKMK_LSA"></a>로컬 보안 기관
로컬 보안 기관 (LSA)에 인증 하 고 로컬 컴퓨터에 사용자를 로그 하는 보호 된 시스템 프로세스입니다. 또한 LSA (이러한 측면 이라고 통칭 로컬 보안 정책) 컴퓨터에서 로컬 보안의 모든 측면에 대 한 정보를 유지 관리 하 고 이름 및 보안 식별자 (Sid) 간의 변환에 대 한 다양 한 서비스를 제공 합니다. 보안 정책 및 컴퓨터 시스템에 적용 되는 계정이 로컬 보안 기관 서버 서비스 (LSASS), 보안 시스템 프로세스는 추적 합니다.

LSA는 사용자의 계정에 발급 하는 다음 두 엔터티가 기반으로 하는 사용자의 id의 유효성을 검사 합니다.

-   **로컬 보안 기관입니다.** LSA는 동일한 컴퓨터에 있는 보안 계정 관리자 (SAM) 데이터베이스를 확인 하 여 사용자 정보를 확인할 수 있습니다. 모든 워크스테이션 또는 구성원 서버 로컬 사용자 계정 및 로컬 그룹에 대 한 정보를 저장할 수 있습니다. 그러나 이러한 계정은 해당 워크스테이션 또는 컴퓨터에 액세스 하기 위해 사용할 수 있습니다.

-   **트러스트 된 도메인 또는 로컬 도메인에 대 한 보안 권한입니다.** LSA는 계정이 유효 하 고 계정 소유자에서 요청이 시작 된 요청 확인 고 계정에 발급 한 엔터티를 연결 합니다.

LSASS(Local Security Authority Subsystem Service)는 활성 Windows 세션의 사용자를 위해 메모리에 자격 증명을 저장합니다. 저장된 된 자격 증명 사용 사용자가 원활 하 게 각 원격 서비스에 대 한 자격 증명을 다시 입력 하지 않고도 파일 공유, Exchange Server 사서함 및 SharePoint 사이트와 같은 네트워크 리소스에 액세스할 수 있습니다.

LSASS는 다음을 비롯한 여러 가지 형식으로 자격 증명을 저장할 수 있습니다.

-   역방향으로 암호화된 일반 텍스트

-   Kerberos 티켓 (티켓 부여 티켓 (Tgt), 서비스 티켓)

-   NT 해시

-   LM (LAN Manager) 해시

사용자 Windows 스마트 카드를 사용 하 여에 로그온 하는 경우 LSASS는 일반 텍스트 암호를 저장 하지 않습니다 하지만 계정과 스마트 카드에 대 한 일반 텍스트 PIN에 대 한 해당 NT 해시 값을 저장 합니다. 대화형 로그온에 필요한 계정 특성이 스마트 카드에 사용하도록 설정된 경우 계정에 대해 원래 암호 해시 대신 임의의 NT 해시 값이 자동으로 생성됩니다. 특성이 설정될 때 자동으로 생성된 암호는 변경되지 않습니다.

사용자가 LM (LAN Manager) 해시와 호환 되는 암호를 사용 하 여 Windows 기반 컴퓨터에 로그온 하는 경우이 인증 자가 메모리에 보관 됩니다.

메모리의 일반 텍스트 자격 증명 저장소는 이를 필요로 하는 자격 증명 공급자가 사용되지 않는 경우에도 비활성화할 수 없습니다.

저장된 된 자격 증명 직접 연결 된 마지막 시작 된 로컬 보안 기관 하위 시스템 서비스 (LSASS) 로그온 세션 다시 시작 하 고 종결 되지 않은 합니다. 예를 들어 사용자가 다음 중 하나를 수행하는 경우 저장된 LSA 자격 증명을 사용하는 LSA 세션이 만들어집니다.

-   로컬 세션 또는 컴퓨터의 원격 데스크톱 프로토콜 (RDP) 세션에 로그온

-   **RunAs** 옵션을 사용하여 작업을 실행하는 경우

-   컴퓨터에서 활성 Windows 서비스를 실행하는 경우

-   예약된 작업 또는 일괄 처리 작업을 실행하는 경우

-   원격 관리 도구를 사용하여 로컬 컴퓨터에서 작업을 실행하는 경우

일부 경우에는 SYSTEM 계정 프로세스에만 액세스할 수 있는 데이터의 암호 부분 lsa 하드 디스크 드라이브에 저장 됩니다. 이러한 암호 중 일부는 다시 부팅 후 유지해야 하는 자격 증명이며, 하드 디스크 드라이브에 암호화된 형식으로 저장됩니다. LSA 암호로 저장될 수 있는 자격 증명은 다음과 같습니다.

-   컴퓨터의 Active Directory Domain Services (AD DS) 계정에 대 한 계정 암호

-   컴퓨터에 구성되어 있는 Windows 서비스에 대한 계정 암호

-   구성된 예약된 작업에 대한 계정 암호

-   IIS 응용 프로그램 풀 및 웹 사이트에 대한 계정 암호

-   Microsoft 계정의 암호

Windows 8.1 도입 된, 클라이언트 운영 체제 메모리 읽기를 방지 하 고 보호 되지 않은 프로세스에 의해 코드 삽입을 위해 LSA에 대 한 추가 보호를 제공 합니다. 이 보호 LSA 저장 하 고 관리 하는 자격 증명에 대 한 보안을 향상 시킵니다.

이러한 추가 보호에 대 한 자세한 내용은 참조 하세요. [Configuring Additional LSA Protection](../credentials-protection-and-management/configuring-additional-lsa-protection.md)합니다.

## <a name="BKMK_CachedCredentialsAndValidation"></a>캐시 된 자격 증명 및 유효성 검사
유효성 검사 메커니즘 로그온 시 자격 증명에 의존합니다. 그러나 도메인 컨트롤러에서 컴퓨터 연결이 끊어져도 사용자는 도메인 자격 증명을 제공 하 고 하는 경우 Windows 유효성 검사 메커니즘에서 캐시 된 자격 증명 프로세스를 사용 합니다.

사용자가 도메인에 로그온 때마다 Windows 제공 된 자격 증명을 캐시 하 고 운영 체제의 레지스트리에 보안 hive에 저장 합니다.

캐시 된 자격 증명을 사용 하 여 사용자 수에 로그온 도메인 구성원이 해당 도메인 내의 도메인 컨트롤러에 연결 하지 않고 합니다.


## <a name="BKMK_CredentialStorageAndValidation"></a>자격 증명 저장 및 유효성 검사
항상 다양 한 리소스에 대 한 액세스 자격 증명 집합을 사용 하는 것이 바람직 있는 것은 아닙니다. 예를 들어 관리자가 사용할 수도 사용자 자격 증명 대신 관리 원격 서버에 액세스 하는 경우. 마찬가지로, 사용자는 은행 계좌와 같은 외부 리소스에 액세스 하는 경우 자신이 사용할 수 해당 도메인 자격 증명을 다른 자격 증명. 다음 섹션에서는 최신 버전의 Windows 운영 체제와 Windows Vista 및 Windows XP 운영 체제 간의 자격 증명 관리의 차이점에 설명 합니다.

### <a name="remote-logon-credential-processes"></a>원격 로그온 자격 증명 프로세스
원격 데스크톱 프로토콜 (RDP) Windows 8에 도입 된 원격 데스크톱 클라이언트를 사용 하 여 원격 컴퓨터에 연결 하는 사용자의 자격 증명을 관리 합니다. 일반 텍스트 형식으로 자격 증명을 대상 호스트는 호스트 인증 프로세스를 수행 하려고 시도 성공 하면 허용 된 리소스에 사용자를 연결에 전송 됩니다. 클라이언트에서 RDP 자격 증명을 저장 하지 않습니다 하지만 사용자의 도메인 자격 증명 LSASS 저장 됩니다.

Windows Server 2012 R2 및 Windows 8.1 도입 된, 제한 된 관리자 모드 원격 로그온 시나리오에 대 한 추가 보안을 제공 합니다. 이 모드의 원격 데스크톱 클라이언트 응용 프로그램을 네트워크 로그온 시도-응답 (NTOWF) NT 단방향 함수를 사용 하 여 수행 하거나 원격 호스트에 인증할 때 Kerberos 서비스 티켓을 사용 하면 됩니다. 관리자가 인증 되 면 관리자가 없는 각 계정 자격 증명을 LSASS 원격 호스트에 제공 되지 않아. 대신 관리자는 세션에 대 한 컴퓨터 계정 자격 증명을 갖습니다. 컴퓨터 계정으로 작업을 수행 하므로 관리자 자격 증명을 원격 호스트에 제공 되지 않습니다. 리소스 컴퓨터 계정으로 제한 하며 관리자가 자신의 계정 사용 하 여 리소스에 액세스할 수 없습니다.

### <a name="automatic-restart-sign-on-credential-process"></a>자동 다시 시작 로그온 자격 증명 프로세스
사용자가 Windows 8.1 장치에 로그인 하는 경우 LSA는 LSASS.exe에 의해서만 액세스할 수 있는 암호화 된 메모리에 사용자 자격 증명을 저장 합니다. Windows Update가 사용자 망이 자동으로 다시 시작을 시작 하는 경우 사용자에 대 한 자동 로그온을 구성 하려면 이러한 자격 증명이 사용 됩니다.

다시 시작 로그온 메커니즘을 통해 사용자가 자동으로 로그인 하 고 컴퓨터 사용자의 세션을 보호 하려면 또한 잠겨 되는 다음입니다. 자격 증명 관리 LSA에 의해 이루어지는 반면 Winlogon 통해 잠금을 시작 됩니다. 자동으로 로그인 하 고 콘솔에서 사용자의 세션 잠금를 사용자의 잠금 화면 응용 프로그램은 다시 시작 하 고 사용할 수 있습니다.

ARSO에 대 한 자세한 내용은 참조 하세요. [Winlogon 자동 다시 시작 로그온 &#40;ARSO&#41;](winlogon-automatic-restart-sign-on-arso.md)합니다.

### <a name="stored-user-names-and-passwords-in-windows-vista-and-windows-xp"></a>Windows Vista 및 Windows XP에 저장 된 사용자 이름 및 암호
Windows Server 2008, Windows Server 2003, Windows Vista 및 Windows XP **저장 된 사용자 이름 및 암호** 제어판의 여러 집합이 사용 되는 X.509 인증서를 포함 하 여 로그온 자격 증명을 사용 하 고 관리 간소화 스마트 카드와 Windows Live 자격 증명 (이제 Microsoft 계정 이라고 함). 자격 증명-사용자의 프로필의 일부로-필요할 때까지 저장 됩니다. 이 그러면 하나의 암호 보안이 손상 되 면이 영향을 주지는 모든 보안을 보장 리소스별 기준 보안을 높일 수 있습니다.

사용자가 로그온 하 고 서버의 공유와 같은 추가 암호로 보호 된 리소스에 액세스 하려고 하 고 사용자의 기본 로그온 자격 증명 액세스를 얻기 위해 권한이 없는 경우 **저장 된 사용자 이름 및 암호** 쿼리 . 올바른 로그온 정보를 사용 하 여 대체 자격 증명에 저장 된 경우 **저장 된 사용자 이름 및 암호**에 액세스 하려면 이러한 자격 증명이 사용 됩니다. 그렇지 않으면 메시지가 표시 됩니다 후속 세션 중 또는 로그온 세션에서 나중에 다시 사용 하기 위해 저장할 수 있습니다 새 자격 증명을 제공 합니다.

다음과 같은 제한 사항이 있습니다.

-   하는 경우 **저장 된 사용자 이름 및 암호** 특정 리소스를 리소스에 대 한 액세스 거부 되 면에 대해 잘못 되었거나 잘못 된 자격 증명을 포함 하며 **저장 된 사용자 이름 및 암호** 않습니다 대화 상자 표시 됩니다.

-   **사용자 이름 및 암호 저장** NTLM, Kerberos 프로토콜에 대해서만 자격 증명을 저장 합니다. Microsoft 계정 (이전의 Windows Live ID) 및 Secure Sockets Layer (SSL) 인증 합니다. 일부 버전의 Internet Explorer는 기본 인증에 대 한 자체 캐시를 유지합니다.

이러한 자격 증명 \Documents and 추가 Data\Microsoft\Credentials 디렉터리에서 사용자의 로컬 프로필의 암호화 된 부분이 있습니다. 결과적으로, 사용자의 네트워크 정책에서 로밍 사용자 프로필을 지 원하는 경우 이러한 자격 증명 사용자와 로밍할 수 있습니다. 그러나 사용자가 복사본 **저장 된 사용자 이름 및 암호** 두 개의 서로 다른 컴퓨터에 변경 내용을 이러한 컴퓨터 중 하나에서 리소스와 연결 된 자격 증명 변경 전파 되지 않으므로  **사용자 이름 및 암호 저장** 두 번째 컴퓨터입니다.

### <a name="windows-vault-and-credential-manager"></a>Windows 자격 증명 모음 및 자격 증명 관리자
자격 증명 관리자 제어판 저장 하 고 사용자 이름 및 암호 관리 기능으로 Windows Server 2008 R2 및 Windows 7에서 도입 되었습니다. Credential Manager 사용자가 안전한 Windows 자격 증명 모음에 다른 시스템 및 웹 사이트와 관련 된 자격 증명을 저장할 수 있습니다. 일부 버전의 Internet Explorer 웹 사이트에 인증을 위해이 기능을 사용 합니다.

자격 증명 관리자를 사용한 자격 증명 관리는 로컬 컴퓨터의 사용자에 의해 제어됩니다. 사용자는 지원되는 브라우저 및 Windows 응용 프로그램에 자격 증명을 저장하여 이러한 리소스에 로그인해야 할 때 편리하게 사용할 수 있습니다. 자격 증명은 사용자의 프로필에서 컴퓨터의 암호화 된 특수 폴더에 저장 됩니다. 웹 브라우저 등 앱 (자격 증명 관리자 Api의 경우)를 사용 하 여이 기능을 지 원하는 응용 프로그램 로그온 프로세스 중 다른 컴퓨터 및 웹 사이트에 올바른 자격 증명을 제공할 수 있습니다.

웹 사이트, 응용 프로그램 또는 NTLM 또는 Kerberos 프로토콜을 통해 인증을 다른 컴퓨터 요청에 대화 상자가 나타나면에서 선택 해야 합니다 **기본 자격 증명 업데이트** 또는 **암호 저장**확인란 합니다. 이 대화 상자는 사용자 자격 증명을 로컬로 저장할 수 있는 자격 증명 관리자 Api를 지 원하는 응용 프로그램에서 생성 됩니다. 사용자가 선택 된 **암호 저장** 확인란, 자격 증명 관리자는 추적 하는 사용자의 사용자 이름, 암호 및 사용 중인 인증 서비스에 대 한 관련된 정보입니다.

다음에 서비스를 사용 하 고, 자격 증명 관리자는 Windows 자격 증명 모음에 저장 된 자격 증명을 자동으로 제공 합니다. 확인란을 선택하지 않은 경우에는 올바른 액세스 정보를 입력하라는 메시지가 표시됩니다. 새 자격 증명을 사용 하 여 액세스 부여 되 면 자격 증명 관리자 이전 자격 증명을 새로운 덮어쓰고 Windows 자격 증명 모음에서 새 자격 증명을 저장 합니다.

## <a name="BKMK_SAM"></a>보안 계정 관리자 데이터베이스
보안 계정 관리자 (SAM)는 데이터베이스 저장 로컬 사용자 계정 및 그룹입니다. 모든 Windows 운영 체제;에 있습니다 그러나 컴퓨터를 도메인에 가입 되어 있는 경우 Active Directory 관리 Active Directory 도메인의 도메인 계정.

예를 들어 Windows 운영 체제를 실행 하는 클라이언트 컴퓨터 없는 사용자가 로그온 하는 경우에 도메인 컨트롤러와 통신 하 여 네트워크 도메인에 참여 합니다. 통신을 시작 하려면 컴퓨터를 도메인에는 활성 계정이 있어야 합니다. 컴퓨터에서 통신을 수락 하기 전에 도메인 컨트롤러의 LSA를 컴퓨터의 id를 인증 하 고 사용자 보안 주체와 마찬가지로 다음 컴퓨터의 보안 컨텍스트를 생성 합니다. 이 보안 컨텍스트에서 특정 컴퓨터 또는 사용자, 서비스 또는 네트워크의 컴퓨터에서 id 및 사용자 또는 서비스의 기능을 정의합니다. 보안 컨텍스트 내에 포함 된 액세스 토큰에서 액세스할 수 있는 리소스 (예: 프린터 또는 파일 공유) 및-사용자, 컴퓨터 또는 서비스에는 사용자가 수행할 수 있는 작업 (예: 읽기, 쓰기 또는 수정)을 정의 하는 예를 들어, 리소스입니다.

사용자 또는 컴퓨터의 보안 컨텍스트는 사용자 사용자의 기본 워크스테이션 이외의 워크스테이션 또는 서버에 기록 하는 경우와 같은 다른 한 컴퓨터에서 달라질 수 있습니다. 또한 사용자의 권한과 관리자가 수정 하는 경우와 같은 다른 세션 간에 달라질 수 있습니다. 또한 보안 컨텍스트가 일반적으로 다른 사용자 또는 컴퓨터는 네트워크 또는 Active Directory 도메인의 일부로 독립 실행형으로 작동 하는 경우.

## <a name="BKMK_LocalDomainsAndTrustedDomains"></a>로컬 도메인 및 트러스트 된 도메인
두 도메인 간의 트러스트가 존재 하는, 다른 도메인에서 오는 인증의 유효성을 검사 하는 각 도메인에 대 한 인증 메커니즘 사용 합니다. 신뢰할 수 있는 기관 (신뢰할 수 있는 도메인)에서 제공 되는 들어오는 인증 요청을 확인 하 여 리소스 도메인 (트러스트를 준 도메인)의 공유 리소스에 대 한 액세스 제어를 제공 하는 데 도움이 신뢰 합니다. 이러한 방식으로 트러스트 프록시로 있도록 브리지 도메인 간의 인증 요청이 이동의 유효성을 검사 합니다.

특정 신뢰 인증 요청을 전달 하는 방법을 구성 하는 방법에 따라 달라 집니다. 각 도메인에서 다른 도메인의 리소스에 액세스를 제공 하 여 신뢰할 수 있는 도메인에서 트러스팅 도메인의 리소스에 액세스를 제공 하 여 단방향 또는 양방향 트러스트 관계 수입니다. 트러스트는 또한 트러스트가 두 트러스트 파트너 도메인 사이만 존재 하는 경우에서 비 전이적 또는 전이적 트러스트 파트너 중 하나에서 신뢰 하는 다른 도메인으로 자동으로 확장 경우입니다.

인증에 대 한 도메인 및 포리스트 트러스트 관계에 대 한 정보를 참조 하세요 [위임 된 인증 및 트러스트 관계](https://technet.microsoft.com/library/dn169022.aspx)합니다.

## <a name="BKMK_CertificatesInWindowsAuthentication"></a>Windows 인증에 인증서
공개 키 인프라 (PKI)에 소프트웨어, 암호화 기술, 프로세스 및 조직에서는 해당 비즈니스 트랜잭션과 통신을 보호 하는 서비스의 조합입니다. 비즈니스 트랜잭션과 통신을 보호 하는 PKI의 기능 인증 된 사용자와 신뢰할 수 있는 리소스 간에 디지털 인증서 교환을 기반으로 합니다.

디지털 인증서는 속한 엔터티, 발급자 엔터티, 고유한 일련 번호 또는 기타 고유 id, 발급 및 만료 날짜 및 디지털 지문에 대 한 정보를 포함 하는 전자 문서.

인증은 원격 호스트를 신뢰할 수 있는지를 결정 하는 과정입니다. 해당 신뢰성을 설정 하려면 원격 호스트에 적합 한 인증 인증서를 제공 해야 합니다.

원격 호스트는 해당 인증 기관 (CA)에서 인증서를 가져와 설정 합니다. CA 신뢰 체인을 만드는 높은 기관에서 인증을가지고 차례로 수 있습니다. 신뢰할 수 있는 인증서 인지를 확인 하려면 응용 프로그램 루트 CA의 id를 확인 하 고 신뢰할 수 있는지 확인 해야 합니다.

마찬가지로, 원격 호스트 또는 로컬 컴퓨터 사용자 또는 응용 프로그램에서 제공한 인증서 인증 인지 확인 해야 합니다. LSA 및 SSPI를 통해 사용자가 제공 하는 인증서는 신뢰성 로컬 로그온에 대 한 로컬 컴퓨터, 네트워크 또는 도메인에 대 한 인증서 저장소 Active Directory를 통해 평가 됩니다.

인증서, 인증 데이터를 생성 하기 위해 메시지 다이제스트를 생성 하기 위해 Secure Hash Algorithm 1 (SHA1) 등의 해시 알고리즘을 통해 전달 됩니다. 메시지 다이제스트는 하 고 메시지 다이제스트 보낸 사람에 의해 만들어진 증명 하기 위해 보낸 사람의 개인 키를 사용 하 여 디지털 서명 합니다.

> [!NOTE]
> SHA1은 Windows 7 및 Windows Vista의 기본값 이지만 Windows 8의 SHA2로 변경 되었습니다.

**스마트 카드 인증**

스마트 카드 기술에는 인증서 기반 인증의 예시입니다. 스마트 카드를 사용 하 여 네트워크에 로그온 도메인에 사용자를 인증할 때 암호화를 기반으로 식별 및 소유 증명을 사용 하기 때문에 강력한 형식의 인증을 제공 합니다. Active Directory 인증서 서비스 (AD CS)는 각 스마트 카드 로그온 인증서 발급을 통해 암호화 기반 식별 합니다.

스마트 카드 인증에 대 한 내용은 참조는 [Windows 스마트 카드 기술 참조](https://technet.microsoft.com/library/ff404297.aspx)합니다.

가상 스마트 카드 기술 Windows 8에서 도입 되었습니다. PC에서 스마트 카드의 인증서를 저장 하 고 장치의 변조 방지 모듈 TPM (Trusted Platform) 보안 칩을 사용 하 여 보호 합니다. 이러한 방식으로 PC는 사실상 스마트 카드 인증 하기 위해 사용자의 PIN을 수신 해야 합니다.

**원격 및 무선 인증**

원격 및 무선 네트워크 인증은 인증용 인증서를 사용 하는 다른 기술입니다. 인터넷 인증 서비스 (IAS) 및 가상 개인 네트워크 서버에 Extensible Authentication Protocol-Transport Level Security (EAP-TLS), PEAP Protected Extensible Authentication Protocol (), 또는 인터넷 프로토콜 보안 (IPsec) 사용 다양 한 유형의 네트워크 액세스, 가상 사설망 (VPN) 등 무선 연결에 대 한 인증서 기반 인증을 수행 합니다.

네트워킹의 인증서 기반 인증에 대 한 정보를 참조 하세요 [네트워크 액세스 인증 및 인증서](https://technet.microsoft.com/library/cc759575(WS.10).aspx)합니다.

## <a name="BKMK_SeeAlso"></a>참고 항목
[Windows 인증 개념](https://technet.microsoft.com/library/d169018.aspx)

