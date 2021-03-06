---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: 주요 Active Directory Federation Services 개념 이해
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d212c2f820204bae8e1e55dc1ebc44200e266a18
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407319"
---
# <a name="understanding-key-ad-fs-concepts"></a>주요 AD FS 개념 이해
Active Directory Federation Services에 대 한 중요 한 개념에 대해 알아보고 기능 집합에 익숙해지는 것이 좋습니다.  
  
> [!TIP]  
> 추가 AD FS 리소스 링크는 Microsoft TechNet WiKi의 [AD FS 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) (영문) 페이지에서 확인할 수 있습니다. 이 페이지는 AD FS 커뮤니티의 회원이 관리하며, AD FS 제품 팀이 정기적으로 모니터링합니다.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>이 가이드에서 사용되는 AD FS 용어  
  
|AD FS 용어|정의|  
|--------------|--------------|  
|계정 파트너 조직|페더레이션 서비스에서 클레임 공급자 트러스트로 표시되는 페더레이션 파트너 조직입니다. 계정 파트너 조직의 웹에 액세스 하는 사용자가 포함\-리소스 파트너에 대 한 응용 프로그램을 기반으로 합니다.|  
|계정 페더레이션 서버|계정 파트너 조직의 페더레이션 서버입니다. 계정 페더레이션 서버는 사용자 인증을 기반으로 사용자에게 보안 토큰을 발급합니다. 서버는 사용자를 인증 하 고, 특성 저장소에서 관련 특성 및 그룹 멤버 자격 정보를 추출 하 고,이 정보를 클레임에 패키지 하 고, 사용자에 게 반환할 클레임\) 포함 하는 보안 토큰 \(를 생성 하 고 서명 합니다 .이를 통해 자체 조직에서 사용 하거나 파트너 조직으로 보낼 수 있습니다.|  
|AD FS 구성 데이터베이스|단일 AD FS 인스턴스 또는 페더레이션 서비스를 나타내는 모든 구성 데이터를 저장하는 데 사용되는 데이터베이스입니다. 이 구성 데이터는 SQL Server 데이터베이스에 저장 하거나 Windows Server 2016, Windows Server 2012 및 2012 r 2와 windows Server 2008 및 2008 r 2에 포함 된 Windows 내부 데이터베이스 기능을 사용 하 여 저장할 수 있습니다. </br></br>AD FS 페더레이션 서버 구성 마법사를 사용 하 여 SQL Server에 대 한 AD FS 구성 데이터베이스를 만들 수 있습니다\-.|  
|클레임 공급자|해당 사용자에게 클레임을 제공하는 조직입니다. 계정 파트너 조직을 참조하세요.|  
|클레임 공급자 트러스트|의 AD FS 관리\-스냅인에서 클레임 공급자 트러스트는 일반적으로 리소스 파트너 조직의 리소스에 액세스 하는 계정을 가진 트러스트 관계의 조직을 나타내기 위해 리소스 파트너 조직에서 만들어지는 트러스트 개체입니다. 클레임 공급자 트러스트 개체는 로컬 페더레이션 서비스에 이 파트너를 식별하는 다양한 식별자, 이름 및 규칙으로 구성됩니다.|  
|로컬 클레임 공급자 트러스트|AD FS 팜의 디렉터리 AD LDS 또는\-타사 LDAP\-기반 디렉터리를 나타내는 트러스트 개체입니다. 로컬 클레임 공급자 트러스트 개체는이 LDAP\-기반 디렉터리를 로컬 페더레이션 서비스에 식별 하는 다양 한 식별자, 이름 및 규칙으로 구성 됩니다.|  
|페더레이션 메타데이터|클레임 공급자 트러스트와 신뢰 당사자 트러스트의 적절한 구성을 용이하게 하기 위해 클레임 공급자와 신뢰 당사자 간에 구성 정보를 전달하는 데이터 형식입니다. 데이터 형식은 SAML\) 2.0 \(Security Assertion Markup Language에 정의 되 고 WS\-페더레이션에서 확장 됩니다.|  
|페더레이션 서버|페더레이션 서버 역할을 수행 하도록 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 구성 된 Windows Server입니다. 페더레이션 서버는 토큰을 발급 하 고 페더레이션 서비스의 일부로 사용 됩니다.|  
|페더레이션 서버 프록시|AD FS 페더레이션 서버 프록시 구성 마법사를 사용 하 여 인터넷 클라이언트와 회사 네트워크의 방화벽 뒤에 있는 페더레이션 서비스 사이에서 중간 프록시 서비스 역할을 하도록 구성 된 Windows Server입니다.|  
|기본 페더레이션 서버|AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버 역할에 구성 되 고 AD FS 구성 데이터베이스의 읽기\/쓰기 복사본을 포함 하는 Windows 서버입니다. </br></br> 기본 페더레이션 서버는 AD FS 페더레이션 서버 구성 마법사를 사용 하 고 새 페더레이션 서비스을 만드는 옵션을 선택 하 고 해당 컴퓨터를 팜의 첫 번째 페더레이션 서버로 만들 때 생성 됩니다. 이 팜의 다른 모든 페더레이션 서버는 로컬에 저장 된 AD FS 구성 데이터베이스의 읽기\-전용 복사본에 기본 페더레이션 서버에 적용 된 변경 내용을 복제 해야 합니다. "기본 페더레이션 서버"라는 용어는 AD FS 구성 데이터베이스가 SQL Server에 저장된 경우에는 적용되지 않습니다. 이 경우에는 모든 페더레이션 서버에서 SQL Server에 저장된 구성 데이터베이스를 동일하게 읽고 쓸 수 있기 때문입니다.|  
|신뢰 당사자|클레임을 받고 처리하는 조직입니다. 리소스 파트너 조직을 참조하세요.|  
|신뢰 당사자 트러스트|의 AD FS 관리\-스냅인에서 신뢰 당사자 트러스트는 일반적으로에서 만든 트러스트 개체입니다.<br /><br />-계정 파트너 조직에서 계정이 리소스 파트너 조직의 리소스에 액세스 하는 트러스트 관계에서 조직을 나타내는 데 사용할 수 있습니다.<br />-페더레이션 서비스와 단일 웹\-기반 응용 프로그램 간의 트러스트를 나타내는 리소스 파트너 조직입니다.<br /><br />신뢰 당사자 트러스트 개체는이 파트너 또는 웹\-응용 프로그램을 로컬 페더레이션 서비스 식별 하는 다양 한 식별자, 이름 및 규칙으로 구성 됩니다.|  
|리소스 페더레이션 서버|리소스 파트너 조직의 페더레이션 서버입니다. 리소스 페더레이션 서버는 일반적으로 계정 페더레이션 서버에서 발급한 보안 토큰에 따라 사용자에게 보안 토큰을 발급합니다. 서버는 보안 토큰을 받고, 서명을 확인 하 고, 패키지 되지 않은 클레임에 클레임 규칙 논리를 적용 하 여 원하는 나가는 클레임을 생성 하 고, 들어오는 보안 토큰의 정보를 기반으로\) 나가는 클레임을 사용 하 여 \(새 보안 토큰을 생성 하 고, 사용자와 궁극적으로 웹 응용 프로그램에 반환할 새 토큰에 서명 합니다.|  
|리소스 파트너 조직|페더레이션 서비스에서 신뢰 당사자 트러스트로 표시되는 페더레이션 파트너입니다. 리소스 파트너는 계정 파트너의 사용자가 액세스할 수 있는 게시 된 웹\-기반 응용 프로그램을 포함 하는 클레임\-기반 보안 토큰을 발급 합니다.|  
  
## <a name="overview-of-ad-fs"></a>AD FS 개요  
AD FS는 사용자 계정 및 응용 프로그램이 완전히 다른 네트워크나 조직에 있는 경우에도 보호 된 인터넷\-연결 된 응용 프로그램 또는 서비스에 대 한 원활한 SSO 액세스를\) \(제공 하는 id 액세스 솔루션입니다.  
  
응용 프로그램이나 서비스가 하나의 네트워크에 있고 사용자 계정이 다른 네트워크에 있는 경우 사용자가 응용 프로그램 또는 서비스에 액세스하려고 하면 일반적으로 보조 자격 증명을 묻는 메시지가 표시됩니다. 이러한 보조 자격 증명은 응용 프로그램이나 서비스가 있는 영역에서 사용자의 ID를 나타냅니다. 일반적으로 응용 프로그램 또는 서비스를 호스트하는 웹 서버에서 가장 적절한 권한 부여 결정을 내리는 데 필요합니다.  
  
AD FS를 사용 하는 조직은 사용자의 디지털 id 및 액세스 권한을 트러스트 된 파트너에 게 프로젝션 하는 데 사용할 수\) 페더레이션 트러스트 \(신뢰 관계를 제공 하 여 보조 자격 증명에 대 한 요청을 무시할 수 있습니다. 이 페더레이션된 환경에서 각 조직은 고유한 ID를 계속 관리하지만 다른 조직의 ID를 안전하게 적용하고 수용할 수 있습니다.  
  
-   [특성 저장소의 역할](The-Role-of-Attribute-Stores.md)  
  
-   [AD FS 구성 데이터베이스의 역할](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [클레임의 역할](The-Role-of-Claims.md)  
  
-   [클레임 규칙의 역할](The-Role-of-Claim-Rules.md)  
  
-   [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)  
  
-   [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)  
  
-   [클레임 규칙 언어의 역할](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [사용할 클레임 규칙 템플릿 유형 결정](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [AD FS에서 URI를 사용하는 방법](How-URIs-Are-Used-in-AD-FS.md)  
  

