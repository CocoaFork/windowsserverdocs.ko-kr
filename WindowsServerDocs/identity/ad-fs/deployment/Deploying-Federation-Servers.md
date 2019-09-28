---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: 페더레이션 서버 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 785dcad4ac8e03cc59730fb533e30a001569dd63
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359635"
---
# <a name="deploying-federation-servers"></a>페더레이션 서버 배포

Active Directory Federation Services \(AD FS @ no__t-1에서 페더레이션 서버를 배포 하려면 [ 검사 목록의 각 작업을 완료 합니다. 페더레이션 서버 설정 @ no__t-0.  
  
> [!NOTE]  
> 이 검사 목록을 사용 하는 경우 서버를 구성 하는 절차를 시작 하기 전에 먼저 [Windows server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 에서 페더레이션 서버 계획에 대 한 참조를 읽어 보는 것이 좋습니다. 이러한 방식으로 검사 목록에 따라 페더레이션 서버에 대 한 디자인 및 배포 프로세스를 보다 잘 이해할 수 있습니다.  
  
## <a name="about-federation-servers"></a>페더레이션 서버 정보  
페더레이션 서버는 페더레이션 서버 역할을 수행 하도록 구성 된 AD FS 소프트웨어를 설치 하 고 Windows Server 2008를 실행 하는 컴퓨터입니다. 페더레이션 서버는 다른 조직의 사용자 계정 및 인터넷의 모든 위치에서 찾을 수 있는 클라이언트 컴퓨터의 사용자 계정에서 요청을 인증 하거나 라우팅합니다.  
  
컴퓨터에 AD FS 소프트웨어를 설치 하 고 페더레이션 서버 구성 마법사를 사용 AD FS 하 여 페더레이션 서버 역할에 대해 구성 하는 작업을 수행 하면 해당 컴퓨터가 페더레이션 서버가 됩니다. 또한이 도구를 사용 하 여 다음을 지정할 수 있도록 **Start @ no__t-2administrative 관리 도구 @ no__t-3** 메뉴에서 해당 컴퓨터에 대 한 AD FS Management snap @-0in 사용할 수 있습니다.  
  
-   파트너 조직 및 응용 프로그램이 토큰 요청 및 응답을 보낼 AD FS 호스트 이름  
  
-   파트너 조직 및 응용 프로그램이 조직의 고유한 이름 또는 위치를 식별 하는 데 사용 하는 AD FS 식별자  
  
-   서버 팜의 모든 페더레이션 서버가 토큰을 발급 및 서명 하는 데 사용 하는 토큰 @ no__t-0signing 인증서  
  
-   클라이언트 로그온, 로그 오프 및 계정 파트너 검색에 대 한 사용자 지정 된 ASP.NET 웹 페이지의 위치로, 클라이언트 환경을 향상 시킬 수 있습니다.  
  
    > [!NOTE]  
    > 이러한 핵심 사용자 인터페이스 \(UI @ no__t 설정 대부분은 각 페더레이션 서버의 web.config 파일에 포함 되어 있습니다. AD FS 호스트 이름 및 AD FS 식별자 값이 web.config 파일에 지정 되어 있지 않습니다.  
  
페더레이션 서버는 @no__t 자격 증명을 기반으로 토큰을 발급 하는 클레임 발급 엔진을 호스트 합니다. 예를 들어 사용자 이름 및 암호 @ no__t-1과 같은 자격 증명을 제공 합니다. 보안 토큰은 하나 이상의 클레임을 표현 하는 암호화 된 서명 된 데이터 단위입니다. 클레임은 서버에서 이름, id, 키, 그룹, 권한 또는 클라이언트에 대해 @ no__t-1과 같은 @no__t를 수행 하는 문입니다. 페더레이션 @no__t 서버에서 자격 증명을 확인 한 후 사용자 로그온 프로세스 @ no__t-1을 통해 사용자에 대 한 클레임이 지정 된 특성 저장소에 저장 된 사용자 특성을 검사 하 여 수집 됩니다.  
  
페더레이션된 웹 단일 @ no__t-0Sign @ no__t-1On \(SSO @ no__t 디자인에서 두 개 이상의 조직이 @ no__t-5와 관련 된 \(AD FS 디자인은 특정 신뢰 당사자에 대 한 클레임 규칙에 따라 클레임을 수정할 수 있습니다. 클레임은 리소스 파트너 조직의 페더레이션 서버에 전송 되는 토큰에 기본 제공 됩니다. 리소스 파트너의 페더레이션 서버는 들어오는 클레임으로 클레임을 수신 하 고 나면 클레임 발급 엔진을 실행 하 여 클레임 규칙 집합을 실행 하 여 해당 클레임을 필터링, 통과 또는 변환 합니다. 그런 다음 클레임은 리소스 파트너의 웹 서버로 전송 되는 새 토큰에 기본 제공 됩니다.  
  
웹 SSO 디자인 \( 하나의 조직에만 관련 된 AD FS 디자인은 단일 페더레이션 서버를 사용 하 여 직원 들이 한 번 로그온 하 여 여러 응용 프로그램에 계속 액세스할 수 있습니다.  
  
