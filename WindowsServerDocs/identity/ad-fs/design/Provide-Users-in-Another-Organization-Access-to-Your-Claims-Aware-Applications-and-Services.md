---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: 다른 조직의 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4a13332cd7cf6361824f05ead4568a45211cc70a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191022"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>다른 조직의 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공


Active Directory Federation Services에서 리소스 파트너 조직의 관리자 인 경우 \(AD FS\) 다른 조직의 사용자에 대 한 페더레이션된 액세스 권한을 제공 하려는 배포 목표가 있고 \(합니다 계정 파트너 조직\) 을 클레임\-인식 응용 프로그램 또는 웹\-기반 조직에 있는 서비스 \(리소스 파트너 조직의\):  
  
-   사용자 조직 및 페더레이션을 구성 하는 조직과에서 트러스트를 페더레이션 \(계정 파트너 조직\) 에서 호스트 되는 AD FS 보안 응용 프로그램이 나 서비스에 액세스할 수 있습니다 프로그램 조직입니다. 자세한 내용은 참조 [페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)합니다.  
  
    예를 들어, Fabrikam이 자기 회사 네트워크 직원에게 Contoso에서 호스트되는 웹 서비스에 대해 페더레이션 액세스 권한을 갖게 하고 싶을 수 있습니다.  
  
-   페더레이션된 사용자는 신뢰할 수 있는 조직과 직접적인 관련이 없으면 \(예: 개별 고객\), 경계 네트워크에서 호스트 되는 특성 저장소에 로그온 하는 여러 AD FS에 액세스할 수 있습니다\- 또한 인터넷에 있는 클라이언트 컴퓨터에서 한 번에 로그온 하 여 경계 네트워크에서 호스트 되는 보안된 응용 프로그램입니다. 즉, 고객 계정이 경계 네트워크의 응용 프로그램 또는 서비스에 액세스할 수 있도록 호스트하는 경우 특성 저장소에서 호스트하는 고객은 한 번 로그인하기만 하면 경계 네트워크에서 하나 이상의 응용 프로그램 또는 서비스에 액세스할 수 있습니다. 자세한 내용은 참조 [웹 SSO 디자인](Web-SSO-Design.md)합니다.  
  
    예를 들어 Fabrikam 수도 있어야 고객 단일\-기호\-에 \(SSO\) 여러 응용 프로그램이 나 해당 경계 네트워크에 호스팅되는 서비스에 액세스할 수 있습니다.  
  
이 배포 목표를 달성하려면 다음 구성 요소가필요 합니다.  
  
-   **Active Directory Domain Services \(AD DS\):** 리소스 파트너 페더레이션 서버는 Active Directory 도메인에 가입 해야 합니다.  
  
-   **경계 DNS:** Domain Name System \(DNS\) 간단한 호스트 있어야 \(는\) 클라이언트 컴퓨터 리소스 파트너 페더레이션 서버 및 웹 서버를 찾을 수 있도록 하는 리소스를 기록 합니다. DNS 서버는 경계 네트워크에서도 필요한 다른 DNS 레코드를 호스트할 수 있습니다. 자세한 내용은 참조 [페더레이션 서버에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   **리소스 파트너 페더레이션 서버:** 리소스 파트너 페더레이션 서버는 계정 파트너 송신 하는 AD FS 토큰의 유효성을 검사 합니다. 계정 파트너 검색이 페더레이션 서버를 통해 수행 됩니다. 자세한 내용은 [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)를 참조하세요.  
  
-   **웹 서버:** 웹 서버는 웹 응용 프로그램 또는 웹 서비스를 호스트할 수 있습니다. 웹 서버는 수신한 유효한 AD FS 토큰 페더레이션된 사용자의 보호 된 웹 응용 프로그램 또는 웹 서비스에 대 한 액세스를 허용 하기 전에 확인 합니다.  
  
    Windows Identity Foundation을 사용 하 여 \(WIF\), 웹 응용 프로그램을 개발할 수 또는 사용자 이름 및 암호와 같은 모든 표준 로그온 방법으로 만들어진 사용자 로그온 요청을 페더레이션 하는 서비스를 허용 하도록 합니다.  
  
연결 된 항목의 정보를 검토 한 후 시작할 수 있습니다이 목표의 단계를 수행 하 여 배포 [검사 목록: 페더레이션된 웹 SSO 디자인 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) 고 [검사 목록: 웹 SSO 디자인 구현](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)합니다.  
  
다음 그림에서는이 AD FS 배포 목표에 대 한 필수 구성 요소 각각을 보여 줍니다.  
  
![사용자 클레임에 대 한 액세스](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
