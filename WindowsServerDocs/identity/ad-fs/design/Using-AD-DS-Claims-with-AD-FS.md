---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: AD FS 배포 토폴로지 고려 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2af0950e52d800202235bf674545f6c47e9cd88
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190785"
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>AD FS와 함께 AD DS 클레임 사용
  
  
Active Directory Domain Services를 사용 하 여 페더레이션된 응용 프로그램에 대 한 다양 한 액세스 제어를 설정할 수 있습니다 \(AD DS\)\-Active Directory Federation Services와 함께 사용자 및 장치 클레임을 발급 한 \(AD FS \).  
  
## <a name="about-dynamic-access-control"></a>동적 액세스 제어에 대 한  
Windows Server® 2012 동적 액세스 제어 기능 사용 하면 사용자 클레임을 기반으로 하는 파일에 대 한 액세스 권한을 부여 하는 조직이 \(사용자 계정 특성에 의해 발생 되는\) 및 장치 클레임 \(컴퓨터 계정 특성에 의해 발생 하\) Active Directory 도메인 서비스에서 발급 하는 \(AD DS\)합니다. AD DS 클레임을 발급 한 Kerberos 인증 프로토콜을 통해 Windows 통합된 인증에 통합 됩니다.  
  
동적 액세스 제어에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)합니다.  
  
### <a name="whats-new-in-ad-fs"></a>AD FS의 새로운 기능은 무엇입니까?  
동적 액세스 제어 시나리오에 대 한 확장,으로 Windows Server 2012의 AD FS 이제 수행할 수 있습니다.  
  
-   AD DS에서 사용자 계정 속성 외에도 액세스 컴퓨터 계정 특성입니다. AD FS의 이전 버전에서 페더레이션 서비스 액세스 하지 못했습니다 컴퓨터 계정 특성에 AD DS에서.  
  
-   AD DS는 Kerberos 인증 티켓에 상주 하는 사용자 또는 장치 클레임을 발급을 사용 합니다. AD FS의 이전 버전에서는 클레임 엔진이 사용자 및 그룹 보안 식별자를 읽을 수 \(Sid\) 에서 Kerberos 하지만 수 없었습니다 읽을 Kerberos 티켓에 포함 된 정보를 요구 합니다.  
  
-   AD DS 신뢰 응용 프로그램은 다양 한 액세스 제어를 수행 하는 데 사용할 수 있는 SAML 토큰에 사용자 또는 장치 클레임을 발급 변환 합니다.  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>AD DS를 사용할 경우의 이점 AD fs 클레임  
이러한 AD DS 클레임을 발급 한 Kerberos 인증 티켓에 삽입와 다음과 같은 이점을 제공 하기 위해 AD FS와 함께 사용 될 수 있습니다.  
  
-   다양 한 액세스 제어 정책을 해야 하는 조직 클레임 사용 하도록 설정할 수\-응용 프로그램 및 AD DS를 사용 하 여 리소스에 대 한 액세스를 기반으로 특정 사용자 또는 컴퓨터 계정이 AD DS에 저장 된 특성 값을 기반으로 하는 클레임을 발급 합니다. 이 경우 만들기 및 관리와 관련 된 추가 오버 헤드를 줄이기 위해 관리자가 도움이 됩니다.  
  
    -   응용 프로그램 및 Windows 통합 인증을 통해 액세스할 수 있는 리소스에 대 한 액세스를 제어 하기 위한 사용 되는 AD DS 보안 그룹  
  
    -   포리스트 트러스트 비즈니스에 대 한 액세스를 제어 하기 위한 사용 되는\-하\-비즈니스 \(B2B\) \/ 인터넷 액세스 가능한 응용 프로그램 및 리소스입니다.  
  
-   조직에서는 이제 액세스를 방지할 수 무단 네트워크 리소스에 특정 컴퓨터 계정이 AD DS에 저장 된 값을 특성 여부에 따라 클라이언트 컴퓨터에서 \(예를 들어 컴퓨터의 DNS 이름을\) 일치 하는 리소스의 액세스 제어 정책 \(클레임 ACLd 된 파일 서버 예를 들어\) 또는 신뢰 당사자 정책 \(클레임 예를 들어\-인식 웹 응용 프로그램\)합니다. 이 리소스 또는 응용 프로그램을 실행 하는 것에 대 한 세부적인 액세스 제어 정책을 설정 하려면 관리자가 도움이 됩니다.  
  
    -   Windows 통합 인증을 통해 액세스할 수 있습니다.  
  
    -   인터넷 AD FS 인증 메커니즘을 통해 액세스할 수 있습니다. AD FS는 사용 하는 인터넷 액세스 가능한 리소스 또는 신뢰 당사자 응용 프로그램에서 사용할 수 있는 SAML 토큰을 암호화할 수 있는 AD FS 클레임으로 장치 클레임을 발급 하는 AD DS를 변환할 수 있습니다.  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>AD DS 및 AD FS 간의 차이점 클레임이 발급  
AD DS vs에서 발행 한 클레임에 대해 이해 하는 중요 한 차별화 요소 두 개 있습니다. AD FS 합니다. 이러한 차이점은 다음과 같습니다.  
  
-   AD DS 하지 SAML 토큰, Kerberos 티켓에 캡슐화 되는 클레임을 발급할 수 있습니다. AD DS 클레임을 발급 하는 방법에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)합니다.  
  
-   AD FS SAML 토큰, Kerberos 티켓 하지에 캡슐화 되는 클레임을 발급할 수 있습니다. AD FS 클레임을 발급 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)합니다.  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>AD DS에서 발급한 클레임이 AD FS와 작동하는 방식  
AD DS 클레임을 발급 한 클레임을 사용자와 장치 모두에서 직접 액세스 하려면 사용자의 인증 컨텍스트를 만드는 대신 별도 LDAP 호출을 Active Directory에 AD FS와 함께 사용할 수 있습니다. 다음 그림 및 해당 단계에 설명 자세히 클레임을 사용 하도록 설정 하려면이 프로세스가 작동 하는 방법을\-기반 동적 액세스 제어 시나리오에 대 한 액세스를 제어 합니다.  
  
![클레임 사용](media/UsingADDSClaimswithADFS.gif)  
  
1.  AD DS 관리자가 AD DS 스키마에서 Active Directory 관리 센터 콘솔 또는 PowerShell cmdlet을 사용 하면 특정 클레임 유형 개체를 사용합니다.  
  
2.  AD FS 관리자가 AD FS 관리 콘솔을 사용 하 여 만들고 클레임 공급자와 신뢰 당사자를 구성 하 전달 하거나 트러스트\-를 통해 또는 변환 클레임 규칙입니다.  
  
3.  Windows 클라이언트는 네트워크에 액세스 하려고 합니다. Kerberos 인증 프로세스의 일부로, 클라이언트는 해당 사용자 및 컴퓨터 티켓 제공\-티켓 부여 \(TGT\) 도메인 컨트롤러에 모든 청구에 아직 포함 하지 않는 합니다. 그런 다음 도메인 컨트롤러는 활성화 된 클레임 형식에 대 한 AD DS에서에서 찾습니다 하 고 결과 클레임 반환 된 Kerberos 티켓에 포함 됩니다.  
  
4.  때 사용자\/ACLd 클레임을 요구할 수 있는 파일 리소스 액세스 시도, 복합 ID가 Kerberos에서 노출 되는 이러한 클레임에 있기 때문에 리소스에 액세스할 수 있습니다.  
  
5.  동일한 클라이언트를 AD FS 인증을 위해 구성 된 웹 사이트 또는 웹 응용 프로그램에 액세스 하려고 하면 Windows 통합된 인증을 위해 구성 된 AD FS 페더레이션 서버에 리디렉션됩니다. 클라이언트는 Kerberos를 사용 하 여 도메인 컨트롤러에 요청을 보냅니다. 도메인 컨트롤러가 클라이언트 페더레이션 서버에 제출할 수 있는 요청 된 클레임을 포함 하는 Kerberos 티켓을 발급 합니다.  
  
6.  클레임 규칙 클레임 공급자에 구성 된 방식에 따라 및 신뢰 당사자 트러스트는 관리자가 이전에 구성한 AD FS 클레임에서 Kerberos 티켓을 읽고에서 클라이언트에 발급 하는 SAML 토큰에 포함 합니다.  
  
7.  클라이언트는 올바른 클래임이 포함 된 SAML 토큰을 수신 하 고 웹 사이트로 리디렉션됩니다.  
  
AD FS와 작동 하도록 클레임을 발급 하는 AD DS에 필요한 클레임 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [들어오는 클레임 변환 규칙을 만들](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
