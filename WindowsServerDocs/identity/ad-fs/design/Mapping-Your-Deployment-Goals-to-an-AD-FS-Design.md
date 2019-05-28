---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: AD FS 디자인에 배포 목표 매핑
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13d8ae8b8f3e4c8160f61284e5fb97e21b6a51b6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191253"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>AD FS 디자인에 배포 목표 매핑


기존 Active Directory Federation Services 검토를 완료 한 후 \(AD FS\) 배포 목표 확인 배포에 관련 된 목표, 특정 AD FS 디자인에 이러한 목표를 매핑할 수 있습니다. 자세한 내용은 AD FS 배포 목표 미리 정의 참조 [AD FS 배포 목표 식별](Identifying-Your-AD-FS-Deployment-Goals.md)합니다.  
  
다음 표를 사용 하 여 AD FS의 적절 한 조합에 매핑되는 AD FS 디자인 조직의 배포 목표를 결정 합니다. 이 테이블은이 가이드에 설명 된 대로 두 개의 기본 AD FS 디자인에만 참조 합니다. 그러나 조직의 요구를 충족 하도록 AD FS 배포 목표의 조합을 사용 하 여 하이브리드 또는 사용자 지정 AD FS 디자인을 만들 수 있습니다.  
  
|AD FS 배포 목표|[웹 SSO 디자인](Web-SSO-Design.md)|[페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Active Directory 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|아니요|예, 계정 파트너에서|  
|[Active Directory 사용자에게 다른 조직의 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|아니요|예, 계정 파트너에서 선택 사항|  
|[다른 조직의 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|예|예|  

## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

