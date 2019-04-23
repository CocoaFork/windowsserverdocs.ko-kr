---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: 페더레이션 서버 프록시 작동 여부 확인
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4900d8621b94a514a07bba55b2f7f3df5dd36353
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814624"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>페더레이션 서버 프록시 작동 여부 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 절차를 사용 하 여 페더레이션 서버 프록시 Active Directory Federation Services에서 페더레이션 서비스와 통신할 수 있는지 확인 하려면 \(AD FS\)합니다. 실행 한 후이 절차를 실행 합니다 **AD FS 페더레이션 서버 프록시 구성 마법사** 페더레이션 서버 프록시 역할에서 실행 하도록 컴퓨터를 구성 하려면. 이 마법사를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [컴퓨터 페더레이션 서버 프록시 역할에 대 한 구성](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)합니다.  
  
> [!IMPORTANT]  
> 이 테스트에 성공하면 이벤트 뷰어에 페더레이션 서버 프록시 컴퓨터에 대한 특정 이벤트가 생성됩니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>페더레이션 서버 프록시 작동 중인지 확인 하려면  
  
1.  관리자 권한으로 페더레이션 서버 프록시에 로그온 합니다.  
  
2.  에 **시작** 화면에서 입력**이벤트 뷰어**, 한 다음 ENTER를 누릅니다.  
  
3.  세부 정보 창에서 두 번\-클릭 **Applications and Services Logs**, 이중\-클릭 **AD FS 이벤트**를 클릭 하 고 **관리자**합니다.  
  
4.  **이벤트 ID** 열에서 이벤트 ID 198을 확인합니다.  
  
    페더레이션 서버 프록시가 제대로 구성 되어 이벤트 ID 198을 사용 하 여 이벤트 뷰어 응용 프로그램 로그에 새 이벤트가 표시 됩니다. 이 이벤트는 페더레이션 서버 프록시 서비스가 성공적으로 시작 되었으며 현재 온라인 확인 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
