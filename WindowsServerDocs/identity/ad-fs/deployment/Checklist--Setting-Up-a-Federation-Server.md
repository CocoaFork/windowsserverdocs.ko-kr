---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: 검사 목록-페더레이션 서버 설정
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d46fc3246ed6ead54d58f44aaed0e8863ea189a6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192341"
---
# <a name="checklist-setting-up-a-federation-server"></a>검사 목록: 페더레이션 서버 설치

이 검사 목록에는 Active Directory Federation Services에서 페더레이션 서버 역할에 대 한 Windows Server® 2012를 실행 하는 서버를 준비 하는 데 필요한 배포 작업이 포함 \(AD FS\)합니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![페더레이션된 서버를 설정할](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 페더레이션 서버 설정**  
  
||태스크|참조|  
|-|--------|-------------|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|AD FS 페더레이션 서버 배포를 시작 하기 전에 검토; 1.\) Windows 내부 데이터베이스 중 하나를 선택의 장점 및 단점 \(WID\) 또는 SQL Server 2의 AD FS 구성 데이터베이스를 저장 합니다.\) AD FS 배포 토폴로지 유형 및 연결 된 서버 배치와 네트워크 레이아웃 권장 합니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 결정](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 고려 사항](https://technet.microsoft.com/library/gg982489.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|프로덕션 환경에서 사용 해야 하는 페더레이션 서버는 적절 한 수를 확인 하려면 AD FS 용량 계획 지침을 검토 합니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 용량 계획](https://technet.microsoft.com/library/gg749917.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|AD FS 디자인 가이드에서 조직의 페더레이션 서버 배치 위치에 대 한 정보를 검토|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx)<br /><br />![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|여부가 스탠드\-단독으로 페더레이션 서버 또는 페더레이션 서버 팜에 배포를 위한 것이 좋습니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버를 만들어야 하는 경우](https://technet.microsoft.com/library/dd807101.aspx)<br /><br />![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 팜을 만들어야 하는 경우](https://technet.microsoft.com/library/dd807062.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|계정 파트너 조직 또는 리소스 파트너 조직에서이 새 페더레이션 서버를 만들 수 있는지 여부를 결정 합니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[계정 파트너에서 페더레이션 서버의 역할 검토](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에 페더레이션 서버의 역할 검토](https://technet.microsoft.com/library/dd807065.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|페더레이션 서버에서 서비스 통신 인증서 및 토큰을 사용 하는 방법에 대 한 정보를 검토\-서명 인증서를 안전 하 게 클라이언트 및 페더레이션 서버 프록시 요청을 인증 합니다. **주의:** 하지만 https와 같은 비 정규화 된 호스트 이름으로 인증서를 사용 하는 것이 오래 된 경우:\/\/myserver 이러한 인증서는 보안 가치가 없으므로 및 공격자가 AD FS 페더레이션 서비스를 가장 하도록 설정할 수 있습니다. 엔터프라이즈 클라이언트입니다. 따라서 것이 좋습니다 정규화 된 도메인 이름을 사용 하는 \(FQDN\) 예: https:\/\/myserver.contoso.com,만 사용 하 여 SSL 인증서 발급 된 페더레이션 서비스의 FQDN입니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|회사 네트워크 도메인 이름 시스템을 업데이트 하는 방법에 대 한 정보를 검토 \(DNS\) 이름 확인이 성공한 페더레이션 서버에 발생할 수 있도록 합니다.|![페더레이션된 서버를 설정할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버에 대 한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807041.aspx)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|계정 파트너 포리스트 또는 위치에 사용할 것 또는 포리스트를 신뢰 하는 해당 포리스트의 사용자를 인증 하는 리소스 파트너 포리스트에 도메인에 페더레이션 서버 될 컴퓨터를 가입 합니다. **참고:** 계정 파트너 조직의 페더레이션 서버를 설정 하려는 경우 페더레이션 서버를 사용 하는 포리스트 또는 포리스트를 신뢰 하는 사용자를 인증 하는 위치 포리스트의 모든 도메인에 컴퓨터 가입 먼저 있어야 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[컴퓨터를 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|회사 네트워크의 페더레이션 서버 DNS 호스트 이름을 페더레이션 서버의 IP 주소를 가리키는 DNS의 새로운 리소스 레코드를 만듭니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[호스트를 추가 &#40;는&#41; 페더레이션 서버에 대해 회사 DNS에 리소스 레코드](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|\(선택적\) 페더레이션 서버 팜에 페더레이션 서버 추가 됩니다, 것이 있으면 먼저 기존 토큰의 개인 키를 내보내려면\-서명 인증서 \(팜의첫번째페더레이션서버에\) 준비 인증서의 파일 형식을 갖도록 때 다른 페더레이션 서버 인증서를 가져와야 동일한 합니다.<br /><br />개인 키 내보내기 필요 없는 여러 컴퓨터에서 발급된 된 서버 인증 인증서를 다시 사용할 때 \(내보낼 필요 없이\) 때 받으려는 팜의 각 페더레이션 서버에 대 한 고유한 서버 인증 인증서 또는 합니다. **참고:** AD FS 관리 스냅인\-에서 서버 인증 인증서를 서비스 통신 인증서로 페더레이션 서버에 대 한 참조입니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[서버 인증 인증서의 개인 키 부분 내보내기](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|서버 인증 인증서를 가져온 후 \(또는 개인 키\) 인증 기관에서 \(CA\), 그런 다음 인증서 파일을 각 페더레이션 서버에 대 한 기본 웹 사이트에 가져와야 합니다. **참고:** AD FS 페더레이션 서버 구성 마법사를 사용 하기 전에 반드시 기본 웹 사이트에이 인증서를 설치 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[기본 웹 사이트로 서버 인증 인증서 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|\(선택적\) CA에서 서버 인증 인증서를 얻는 하는 대신, 인터넷 정보 서비스를 사용할 수 있습니다 \(IIS\) 페더레이션 서버에 대 한 샘플 인증서를 만듭니다. **주의:** 자체를 사용 하 여 프로덕션 환경에서 페더레이션 서버를 배포 하는 보안 모범 사례 아닙니다\-서버 인증 인증서를 서명 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 자동 만들기\-서버 인증서 서명](https://go.microsoft.com/fwlink/?LinkID=108271) 절차를 완료 하 고 [기본 웹 사이트로 서버 인증 인증서 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|계정 파트너 조직의 페더레이션 서버 팜 환경을 구성 됩니다, 경우 만들기 하 고 Active Directory Domain Services에서 전용된 서비스 계정을 구성 해야 합니다 \(AD DS\) 팜의 상주할 및 이 계정을 사용 하도록 팜의 각 페더레이션 서버를 구성 합니다. 이 절차를 수행 하 여 클라이언트에 Windows 통합 인증을 사용 하 여 팜에 페더레이션 서버를 인증 하기 위해 회사 네트워크로 지정 하면 있습니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[수동으로 페더레이션 서버 팜에 대 한 서비스 계정 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|역할을 할 페더레이션 서버 컴퓨터에서 페더레이션 서비스 역할 서비스를 설치 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서비스 역할 서비스 설치](Install-the-Federation-Service-Role-Service.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버 역할을 하도록 컴퓨터에 AD FS 소프트웨어를 구성 합니다.<br /><br />대기 모드를 설정 하려는 경우이 절차에 따라\-만 페더레이션 서버를 새 팜의 첫 번째 페더레이션 서버 만들기 또는 기존 페더레이션 서버 팜에 컴퓨터를 가입 합니다. **참고:** 페더레이션 웹 Single sign\-온 \(SSO\) 디자인, 계정 파트너 조직에서 하나 이상의 페더레이션 서버 및 리소스 파트너 조직에서 하나 이상의 페더레이션 서버를 사용 하도록 해야 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[독립 실행형 페더레이션 서버 만들기](Create-a-Stand-Alone-Federation-Server.md)<br /><br />![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)<br /><br />![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서버 팜에 페더레이션 서버 추가](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|\(선택적\) AD FS 관리 스냅인을 사용 하 여\-에 추가 하 고 디자인을 배포 하는 데 필요한 필요한 AD FS 인증서를 구성 합니다. 스냅인을 사용 하는 인증서를 추가 하거나 변경 하는 경우에 대 한 자세한 내용은\-을 참조 하십시오. [페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)합니다.|![페더레이션된 서버를 설정할](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[토큰 서명 인증서 추가](Add-a-Token-Signing-Certificate.md)<br /><br />![페더레이션된 서버를 설정할](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[토큰 암호 해독 인증서 추가](Add-a-Token-Decrypting-Certificate.md)<br /><br />![페더레이션된 서버를 설정할](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[서비스 통신 인증서 설정](Set-a-Service-Communications-Certificate.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|조직에서 첫 번째 페더레이션 서버를 AD FS 디자인에 맞도록 페더레이션 서비스를 구성 합니다.|![페더레이션된 서버를 설정할](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![페더레이션된 서버를 설정할](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 리소스 파트너 조직 구성](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![페더레이션된 서버 설정](media/icon_checkboxo.gif)|클라이언트 컴퓨터에서 페더레이션 서버가 작동 하는지 확인 합니다.|![페더레이션된 서버를 설정할](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[확인 하는 페더레이션 서버 작동](Verify-That-a-Federation-Server-Is-Operational.md)| 
