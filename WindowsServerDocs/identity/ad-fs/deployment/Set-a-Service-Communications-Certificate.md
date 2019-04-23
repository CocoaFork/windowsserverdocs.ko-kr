---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: 서비스 통신 인증서 설정
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0d630372d82cf1519da82397a9c90d6a28903ed0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888474"
---
# <a name="set-a-service-communications-certificate"></a>서비스 통신 인증서 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 \(AD FS\) 서비스 통신 인증서를 사용 하 여 Secure Sockets Layer에 대 한 웹 서비스 트래픽의 보안을 유지 \(SSL\) 웹와의 통신 클라이언트 또는 페더레이션 서버 프록시를 사용 하 여 합니다. 페더레이션 서버는 인터넷 정보 서비스에서 SSL 인증서로 사용 하는 동일한 인증서를 이것이 \(IIS\)합니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 서비스 통신 인증서를 변경 하려면\-에서 합니다.  
  
> [!NOTE]  
> AD FS 관리 스냅인\-에서 서버 인증 인증서를 서비스 통신 인증서로 페더레이션 서버에 대 한 참조입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
### <a name="to-set-a-service-communications-certificate"></a>서비스 통신 인증서 설정  
  
1.  에 **시작** 화면에서 입력**AD FS 관리**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 두 번\-클릭 **Service**를 클릭 하 고 **인증서**합니다.  
  
3.  에 **동작** 창 클릭 합니다 **서비스 통신 인증서 설정** 링크.  
  
4.  에 **서비스 통신 인증서를 선택** 대화 상자에서 서비스 통신 인증서로 인증서 파일을 선택한 다음 클릭 하려는 인증서 파일을 이동 **엽니다**.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

