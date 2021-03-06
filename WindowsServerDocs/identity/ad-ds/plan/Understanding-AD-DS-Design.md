---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: AD DS 디자인 이해
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f46cad23e13edcef57bf00113e601069c02cfd4f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402461"
---
# <a name="understanding-ad-ds-design"></a>AD DS 디자인 이해

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에서는 Windows Server에서 Active Directory Domain Services (AD DS)를 사용 하 여 확장 가능 하 고 안전 하며 관리 하기 쉬운 인프라를 만들 때 사용자 및 리소스 관리를 간소화할 수 있습니다. AD DS를 사용 하 여 지점, Microsoft Exchange Server 및 다중 포리스트 환경을 비롯 한 네트워크 인프라를 관리할 수 있습니다.  
  
AD DS 배포 프로젝트에는 디자인 단계, 배포 단계 및 작업 단계의 세 단계가 포함 됩니다. 디자인 단계에서 디자인 팀은 디렉터리 서비스를 사용 하는 조직의 각 부서에 대 한 요구 사항을 가장 잘 충족 하는 AD DS 논리적 구조에 대 한 디자인을 만듭니다. 설계가 승인 되 면 배포 팀은 랩 환경에서 디자인을 테스트 한 다음 프로덕션 환경에서 디자인을 구현 합니다. 테스트는 배포 팀에서 수행 하 고 잠재적으로 디자인 단계에 영향을 줄 수 있으므로 디자인 및 배포를 모두 겹치는 중간 작업입니다. 배포가 완료 되 면 운영 팀은 디렉터리 서비스를 유지 관리 하는 일을 담당 합니다.  
  
이 가이드에서 설명 하는 Windows Server AD DS 설계 및 배포 전략은 고객 환경에서 광범위 한 랩 및 파일럿 프로그램 테스트와 성공적인 구현을 기반으로 하지만 AD DS 디자인을 사용자 지정 해야 할 수도 있습니다. 구체적이 고 복잡 한 환경에 적합 한 배포
  
- 지점 환경에 AD DS를 배포 하는 방법에 대 한 자세한 내용은 [RODC (읽기 전용 도메인 컨트롤러) 지점 계획 가이드](https://go.microsoft.com/fwlink/?LinkId=100207)를 참조 하세요.  
- Exchange 환경에 AD DS를 배포 하는 방법에 대 한 자세한 내용은 [exchange 2007-계획 Active Directory](https://go.microsoft.com/fwlink/?LinkId=88904)문서를 참조 하세요.  
- 다중 포리스트 환경에 AD DS를 배포 하는 방법에 대 한 자세한 내용은 [windows 2000 및 Windows Server 2003의 여러 포리스트 고려 사항](https://go.microsoft.com/fwlink/?LinkId=88905)문서를 참조 하세요.  
