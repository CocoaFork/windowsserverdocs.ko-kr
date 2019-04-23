---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: 추가 다단계 인증을 사용하여 중요한 응용 프로그램에 대한 위험 관리
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9ee275e6fe38005394cd071e9cfe9a7999350e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855894"
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>추가 다단계 인증을 사용하여 중요한 응용 프로그램에 대한 위험 관리

>적용 대상: Windows Server 2012 R2


-   [Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [연습 가이드: 추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [AD FS에 대 한 추가 인증 방법 구성](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>이 가이드의 내용
이 가이드에서는 다음 정보를 제공합니다.

-   [AD FS의 인증 메커니즘](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1) -Active Directory Federation Services (AD FS) Windows Server 2012 r 2에서에서 사용할 수 있는 인증 메커니즘을 설명

-   [시나리오 개요](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2) -MFA (다단계 인증)를 사용 하도록 설정 하려면 Active Directory Federation Services (AD FS)을 사용할 경우에 대 한 설명을 사용자의 그룹 구성원 자격에 기반 합니다.

    > [!NOTE]
    > Windows Server 2012 R2의 AD FS에서 네트워크 위치, 장치 id 및 사용자 id 또는 그룹 멤버 자격에 따라 MFA를 사용할 수 있습니다.

    구성 및 확인이 시나리오에 대 한 자세한 단계별 연습 지침을 참조 하세요. [연습 가이드: 추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다.

## <a name="BKMK_1"></a>주요 개념-AD FS의 인증 메커니즘

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>AD FS의 인증 메커니즘 이점
Active Directory Federation Services (AD FS) Windows Server 2012 R2에서 회사 리소스에 액세스 하려는 사용자를 인증 하기 위한 보다 풍부 하 고 유연한 도구 집합을 사용 하 여 IT 관리자를 제공 합니다. 기본 및 추가 인증 방법을 통해 유연한 컨트롤을 사용 하 여 관리자를 통해, 인증을 구성 하기 위한 풍부한 관리 경험을 정책을 (사용자 인터페이스 및 Windows PowerShell을 통해)를 제공 하 고 개선 응용 프로그램 및 AD FS에서 보안이 유지 되는 서비스에 액세스 하는 최종 사용자 환경. 다음은 일부 응용 프로그램 및 Windows Server 2012 R2에서 AD FS 사용 하 여 서비스 보안 이점입니다.

-   전역 인증 정책-중앙 관리 기능, IT 관리자가 선택할 수 있는 어떤 인증 방법이 보호 리소스에 액세스 하는 네트워크 위치에 따라 사용자를 인증 하는 데 사용 됩니다. 이를 통해 관리자는 다음을 수행할 수 있습니다.

    -   엑스트라넷의 액세스 요청에 더욱 보안이 강화된 인증 방법 사용

    -   연속된 두 번째 단계 인증에 장치 인증 사용. 이 사용자의 id 보호 된 리소스에 액세스 하기 전에 보다 안전한 복합 id 확인을 제공 하므로 리소스에 액세스 하는 데 사용 되는 등록 된 장치를 연결 합니다.

        > [!NOTE]
        > 원활한 2 단계 인증 및 SSO로 서 장치 개체, 장치 등록 서비스, 작업 공간 연결 및 장치에 대 한 자세한 내용은 참조 하세요. [SSO 및 원활한 두 번째 단계 인증을 위해 모든 장치에서 작업 공간 연결 회사 응용 프로그램에서](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

    -   모든 엑스트라넷 액세스에 대해 MFA 요구 사항을 설정 또는 사용자의 id, 네트워크 위치 또는 보호 된 리소스에 액세스 하는 데 사용 되는 장치에 따라 조건부로 합니다.

-   인증 정책 구성의 유연성: 비즈니스 가치를 다양 한 AD FS로 보호 된 리소스에 대 한 사용자 지정 인증 정책을 구성할 수 있습니다. 예를 들어 비즈니스 영향력이 높은 응용 프로그램에 MFA를 요구할 수 있습니다.

-   사용 편의성: GUI 기반 AD FS 관리 MMC 스냅인 및 Windows PowerShell cmdlet 등 간단 하 고 직관적인 관리 도구는 IT 관리자는 상대적인 편의성에 인증 정책을 구성 하를 사용 합니다. Windows PowerShell을 사용하여 규모에 따라 사용할 솔루션을 스크립팅하고 일반적인 관리 작업을 자동화할 수 있습니다.

-   회사 자산에 대 한 제어력이: 했으므로 AD FS를 사용 하 여 특정 리소스에 적용 되는 인증 정책을 구성 하려면 관리자 큰 보호는 어떻게 회사 리소스에 대 한 제어 합니다. IT 관리자가 지정한 인증 정책을 응용 프로그램에서 재정의할 수 없습니다. 중요한 응용 프로그램 및 서비스의 경우 리소스에 액세스할 때마다 MFA 요구 사항, 장치 인증 및 새로운 인증(선택 사항)을 사용하도록 설정할 수 있습니다.

-   사용자 지정 MFA 공급자 지원: 타사 MFA 방법을 활용 하는 조직에서 AD FS 통합이 인증 방법을 원활 하 게 사용 하는 기능을 제공 합니다.

### <a name="authentication-scope"></a>인증 범위
Windows Server 2012 R2의 AD FS에서 모든 응용 프로그램 및 AD FS에서 보안이 유지 되는 서비스에 적용 되는 전역 범위의 인증 정책을 지정할 수 있습니다.  또한 특정 응용 프로그램 및 AD FS에서 보안이 유지 되는 서비스 (신뢰 당사자 트러스트)에 대 한 인증 정책을 설정할 수 있습니다. 특정 응용 프로그램(신뢰 당사자 트러스트별)에 대한 인증 정책을 지정해도 전역 인증 정책은 재정의되지 않습니다. 전역 또는 신뢰 당사자 트러스트별 인증 정책에서 MFA를 요구하는 경우에는 사용자가 이 신뢰 당사자 트러스트에 인증하려고 하면 MFA가 트리거됩니다.  특정 인증 정책을 구성하지 않은 신뢰 당사자 트러스트(응용 프로그램 및 서비스)에는 전역 인증 정책이 적용됩니다.

전역 인증 정책은 AD FS에서 보안이 유지 되는 모든 신뢰 당사자에 적용 됩니다. 전역 인증 정책의 일부로 다음 설정을 구성할 수 있습니다.

-   기본 인증에 사용할 인증 방법

-   MFA에 대한 설정 및 방법

-   장치 인증 사용 여부. 자세한 내용은 [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)를 참조하세요.

신뢰 당사자 트러스트별 인증 정책은 신뢰 당사자 트러스트(응용 프로그램 또는 서비스)에 액세스하려는 경우에 특별히 적용됩니다. 신뢰 당사자 트러스트별 인증 정책의 일부로 다음 설정을 구성할 수 있습니다.

-   사용자가 로그인할 때마다 자격 증명을 제공해야 하는지 여부

-   사용자/그룹, 장치 등록 및 액세스 요청 위치 데이터에 따른 MFA 설정

### <a name="primary-and-additional-authentication-methods"></a>기본 및 추가 인증 방법
기본 인증 메커니즘 외에도 Windows Server 2012 R2에서 AD FS를 사용 하 여 관리자는 추가 인증 방법을 구성할 수 있습니다. 기본 인증 방법 기본 제공 되 고 사용자 id의 유효성을 검사 하고자 합니다. 사용자의 id에 대 한 자세한 내용은 제공 되도록 요청 하려면 추가 인증 단계를 구성할 수 있으며 결과적으로 보다 강력한 인증을 확인 합니다.

Windows Server 2012 R2의 AD FS에서 기본 인증을 사용 하 여 다음 옵션 해야 합니다.

-   회사 네트워크 외부에서 액세스할 수 있는 게시된 리소스의 경우 폼 인증이 기본적으로 선택됩니다. 또한 인증서 인증(즉, 스마트 카드 기반 인증 또는 AD DS와 함께 작동하는 사용자 클라이언트 인증서 인증)를 사용할 수도 있습니다.

-   인트라넷 리소스의 경우 Windows 인증이 기본적으로 선택됩니다. 또한 폼 및/또는 인증서 인증을 사용할 수도 있습니다.

둘 이상의 인증 방법을 선택하여 사용자가 응용 프로그램이나 서비스에 대한 로그인 페이지에서 인증 방법을 선택하도록 할 수 있습니다.

또한 연속된 두 번째 단계 인증에 장치 인증을 사용할 수 있습니다. 이 사용자의 id 보호 된 리소스에 액세스 하기 전에 보다 안전한 복합 id 확인을 제공 하므로 리소스에 액세스 하는 데 사용 되는 등록 된 장치를 연결 합니다.

> [!NOTE]
> 원활한 2 단계 인증 및 SSO로 서 장치 개체, 장치 등록 서비스, 작업 공간 연결 및 장치에 대 한 자세한 내용은 참조 하세요. [SSO 및 원활한 두 번째 단계 인증을 위해 모든 장치에서 작업 공간 연결 회사 응용 프로그램에서](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

인트라넷 리소스에 대해 Windows 인증 방법(기본 옵션)을 지정한 경우에는 인증 요청 시 Windows 인증을 지원하는 브라우저에서 이 방법이 연속적으로 실행됩니다.

> [!NOTE]
> 일부 브라우저에서는 Windows 인증이 지원되지 않습니다. Windows Server 2012 R2에서 AD FS의 인증 메커니즘은 사용자의 브라우저 사용자 에이전트 검색 및 구성 가능한 설정을 사용 하 여 사용자 에이전트가 Windows 인증을 지원 하는지 여부를 결정 합니다. 관리자는 Windows PowerShell `Set-AdfsProperties -WIASupportedUserAgents` 명령을 통해 사용자 에이전트 목록에 이를 추가하여 Windows 인증을 지원하는 브라우저에 대해 다른 사용자 에이전트 문자열을 지정할 수 있습니다. 클라이언트의 사용자 에이전트가 Windows 인증을 지원 하지 않으면 기본 대체 방법은 폼 인증입니다.

### <a name="configuring-mfa"></a>MFA 구성
Windows Server 2012 R2에서 AD FS에서 MFA를 구성 하는 방법은 두 가지가:는 MFA가 필요한 조건 지정과 추가 인증 방법을 선택 합니다. 추가 인증 방법에 대 한 자세한 내용은 참조 하세요. [AD FS에 대 한 추가 인증 방법 구성](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)합니다.

**MFA 설정**

다음 옵션을 MFA 설정(MFA를 요구할 조건)에 사용할 수 있습니다.

-   페더레이션 서버가 가입된 AD 도메인의 특정 사용자 및 그룹에 MFA를 요구할 수 있습니다.

-   등록된 장치(작업 공간에 연결된 장치) 또는 등록되지 않은 장치(작업 공간에 연결되지 않은 장치)에 MFA를 요구할 수 있습니다.

    Windows Server 2012 R2는 장치 개체 간의 관계를 나타내는 최신 장치에는 사용자 중심의 접근 방식을 사용 user@device 와 회사입니다. 장치 개체는 응용 프로그램 및 서비스에 대 한 액세스를 제공할 때 복합 id를 제공 하는 Windows Server 2012 R2에서 AD에서 새 클래스. AD FS의 새 구성 요소인 DRS(장치 등록 서비스)는 Active Directory에서 장치 ID를 프로비전하고 소비자 장치에서 장치 ID를 나타내는 데 사용할 인증서를 설정합니다. 그런 다음 이 장치 ID를 사용하여 장치를 작업 공간에 연결할 수 있습니다. 즉, 개인 장치를 작업 공간의 Active Directory에 연결할 수 있습니다. 개인 장치를 작업 공간에 연결한 경우 해당 장치는 알려진 장치가 되며, 보호된 리소스 및 응용 프로그램에 대한 연속된 두 번째 단계 인증을 제공합니다. 즉, 장치가 작업 공간에 연결 되 면 사용자의 id를이 장치에 연결 되 고 보호 된 리소스에 액세스 하기 전에 원활 하 게 복합 id 확인에 사용할 수 있습니다.

    작업 공간 연결 및 연결 해제에 대 한 자세한 내용은 참조 하세요. [SSO 및 원활한 두 번째 단계 인증에서 회사 응용 프로그램에 대 한 모든 장치의 작업 공간 연결](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)합니다.

-   엑스트라넷 또는 인트라넷에서 보호된 리소스에 대한 액세스를 요청한 경우 MFA를 요구할 수 있습니다.

## <a name="BKMK_2"></a>시나리오 개요
이 시나리오에서는 특정 응용 프로그램에 대 한 사용자의 그룹 구성원 자격 데이터에 따라 MFA를 사용 합니다. 즉, 특정 그룹에 속한 사용자가 웹 서버에서 호스팅되는 특정 응용 프로그램에 대한 액세스를 요청할 때 페더레이션 서버에서 MFA를 요구하는 인증 정책을 설정합니다.

구체적으로, 이 시나리오에서는 클레임 기반 테스트 응용 프로그램 **claimapp**에 대한 인증 정책을 설정합니다. 여기서 AD 사용자 **Robert Hatley** 는 AD 그룹 **Finance**에 속해 있으므로 MFA를 진행해야 합니다.

설정 하 고이 시나리오를 확인 하 여 단계 단계 지침을 제공 [연습 가이드: 추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)합니다. 이 연습의 단계를 완료 하려면 랩 환경을 설정 하며의 단계를 따릅니다 [Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)합니다.

AD FS에서 MFA를 사용 하는의 다른 시나리오는 다음과 같습니다.

-   엑스트라넷에서 액세스를 요청한 경우 MFA를 사용합니다. "MFA 정책 설정" 섹션에 나와 있는 코드를 수정할 수 있습니다 [연습 가이드: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용한 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음을 사용 하 여:

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   작업 공간에 연결되지 않은 장치에서 액세스를 요청한 경우 MFA를 사용합니다.  "MFA 정책 설정" 섹션에 나와 있는 코드를 수정할 수 있습니다 [연습 가이드: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용한 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음을 사용 하 여:

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   작업 공간에 연결되어 있지만 해당 사용자에 등록되지 않은 장치의 사용자가 액세스하는 경우 MFA를 사용합니다. "MFA 정책 설정" 섹션에 나와 있는 코드를 수정할 수 있습니다 [연습 가이드: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용한 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 다음을 사용 하 여:

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>관련 항목
[연습 가이드: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용한 위험 관리](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



