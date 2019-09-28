---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: 페더레이션 서버 프록시를 배치하는 위치
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 73e68d03e4f2f76dbaf4a497da551640476d0438
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407825"
---
# <a name="where-to-place-a-federation-server-proxy"></a>페더레이션 서버 프록시를 배치하는 위치

Active Directory Federation Services \(AD FS @ no__t-1federation 서버 프록시를 경계 네트워크에 추가 하 여 인터넷에서 들어오는 악의적인 사용자에 대 한 보호 계층을 제공할 수 있습니다. 페더레이션 서버 프록시는 토큰을 만드는 데 사용되는 프라이빗 키에 액세스할 수 없으므로 경계 네트워크 환경에 적합합니다. 그러나 페더레이션 서버 프록시는 들어오는 요청을 이러한 토큰을 생성할 수 있는 권한이 있는 페더레이션 서버로 효율적으로 라우팅할 수 있습니다.  
  
회사 네트워크에 연결 된 클라이언트 컴퓨터가 페더레이션 서버와 직접 통신할 수 있으므로 계정 파트너 또는 리소스 파트너에 대해 페더레이션 서버 프록시를 회사 네트워크 내부에 저장할 필요가 없습니다. 이 시나리오에서 페더레이션 서버는 회사 네트워크에서 들어오는 클라이언트 컴퓨터에도 페더레이션 서버 프록시 기능을 제공 합니다.  
  
경계 네트워크와 마찬가지로 인트라넷 @ no__t-0facing 방화벽은 경계 네트워크와 회사 네트워크 간에 설정 되 고 인터넷 @ no__t-1은 경계 네트워크와 인터넷 간에 설정 되는 경우가 많습니다. 이 시나리오에서 페더레이션 서버 프록시는 경계 네트워크에 있는 두 방화벽 사이에 있습니다.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>페더레이션 서버 프록시에 대한 방화벽 서버 구성  
페더레이션 서버 프록시 리디렉션 프로세스가 성공 하려면 모든 방화벽 서버에서 보안 하이퍼텍스트 전송 프로토콜 \(HTTPS @ no__t-1 트래픽을 허용 하도록 구성 해야 합니다. 방화벽 서버는 경계 네트워크의 페더레이션 서버 프록시가 회사 네트워크의 페더레이션 서버에 액세스할 수 있도록 포트 443을 사용 하 여 페더레이션 서버 프록시를 게시 해야 하므로 HTTPS를 사용 해야 합니다.  
  
> [!NOTE]  
> 클라이언트 컴퓨터와의 모든 통신도 HTTPS를 통해 발생합니다.  
  
또한 Microsoft Internet Security 및 가속화 \(ISA @ no__t-2 Server를 실행 하는 컴퓨터와 같은 Internet @ no__t-0wwwserver는 서버 게시 라는 프로세스를 사용 하 여 인터넷 클라이언트 요청을 적절 한에 배포 합니다. 경계 및 회사 네트워크 서버 (예: 페더레이션 서버 프록시 또는 페더레이션 서버).  
  
서버 게시 규칙은 서버 게시의 작동 방식을 결정하며, 기본적으로 ISA Server 컴퓨터를 통해 들어오고 나가는 모든 요청을 필터링합니다. 서버 게시 규칙은 들어오는 클라이언트 요청을 ISA Server 컴퓨터 뒤의 해당 서버에 매핑합니다. 서버를 게시 하도록 ISA Server를 구성 하는 방법에 대 한 자세한 내용은 [안전한 웹 게시 규칙 만들기](https://go.microsoft.com/fwlink/?LinkId=75182)를 참조 하세요.  
  
AD FS의 페더레이션된 세계에서 이러한 클라이언트 요청은 일반적으로 특정 URL (예: http: \//s s o. s s o. s s o. c o s. c o s. c o n t e n t e r: 이러한 클라이언트 요청은 인터넷에서 제공 되기 때문에 경계 네트워크에 배포 된 각 페더레이션 서버 프록시에 대 한 페더레이션 서버 식별자 URL을 게시 하도록 Internet @ no__t-0abfirewall 서버를 구성 해야 합니다.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>SSL을 허용하도록 ISA Server 구성  
보안 AD FS 통신을 용이 하 게 하려면 ISA Server를 구성 하 여 다음 간에 SSL(Secure Sockets Layer) \(SSL @ no__t-1 통신을 허용 해야 합니다.  
  
-   **페더레이션 서버 및 페더레이션 서버 프록시.** 페더레이션 서버와 페더레이션 서버 프록시 간의 모든 통신에 SSL 채널이 필요 합니다. 따라서 회사 네트워크와 경계 네트워크 간에 SSL 연결을 허용하도록 ISA Server를 구성해야 합니다.  
  
-   **클라이언트 컴퓨터, 페더레이션 서버 및 페더레이션 서버 프록시** 클라이언트 컴퓨터와 페더레이션 서버 간에 또는 클라이언트 컴퓨터와 페더레이션 서버 프록시 간에 통신이 발생할 수 있도록 ISA Server를 실행 하는 컴퓨터를 페더레이션 서버 또는 페더레이션 서버 프록시 앞에 둘 수 있습니다.  
  
    조직에서 페더레이션 서버 또는 페더레이션 서버 프록시에 대 한 SSL 클라이언트 인증을 수행 하는 경우 ISA Server를 실행 하는 컴퓨터를 페더레이션 서버 또는 페더레이션 서버 프록시 앞에 두면 pass @ no__에 대해 서버를 구성 해야 합니다. ssl 연결이 페더레이션 서버 또는 페더레이션 서버 프록시에서 종료 되어야 하므로 SSL 연결의 t-0에서  
  
    조직에서 페더레이션 서버 또는 페더레이션 서버 프록시에 대 한 SSL 클라이언트 인증을 수행 하지 않는 경우에는 ISA Server를 실행 하는 컴퓨터에서 SSL 연결을 종료 한 다음 다시 @ no__t-0으로 설정 하 여 ssl 연결을 페더레이션 서버 또는 페더레이션 서버 프록시.  
  
> [!NOTE]  
> 페더레이션 서버 또는 페더레이션 서버 프록시는 보안 토큰의 내용을 보호 하기 위해 연결을 SSL로 보호 해야 합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
