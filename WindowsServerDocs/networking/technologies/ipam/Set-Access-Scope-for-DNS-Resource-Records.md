---
title: DNS 리소스 레코드에 대한 액세스 범위 설정
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c79e1f63b9bcb43520a57defca8228b76db68a31
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283866"
---
# <a name="set-access-scope-for-dns-resource-records"></a>DNS 리소스 레코드에 대한 액세스 범위 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔을 사용 하 여 DNS 리소스 레코드에 대 한 액세스 범위를 설정 하려면이 항목에서는 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>DNS 리소스 레코드에 대 한 액세스 범위를 설정 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 클릭 **DNS 영역**합니다.  아래쪽 탐색 창에서 확장 **정방향 조회** 찾아 리소스 레코드를 변경 하려는 액세스 범위가 포함 된 영역을 선택 합니다.  
  
3.  디스플레이 창에서 찾아 리소스 레코드를 변경 하려면 해당 액세스 범위를 선택 합니다.  
  
    ![리소스 레코드를 선택 합니다.](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  선택한 DNS 리소스 레코드를 마우스 오른쪽 단추로 누른 **액세스 범위 설정**합니다.  
  
    ![액세스 범위 설정](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  합니다 **액세스 범위 설정** 대화 상자가 열립니다. 배포에 필요한 경우 선택을 취소 하려면 클릭 **부모 로부터 액세스 범위 상속**합니다. **액세스 범위 선택**항목을 선택한 다음 클릭 **확인**합니다.  
  
    ![액세스 범위 선택](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 액세스 제어](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


