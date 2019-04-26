---
title: 서버 저장소 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef7ddcdd-3a74-40ca-9487-c3a6fc5155a5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6de485f6fd46464ba707bc0871f60ac2fec5a1db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859984"
---
# <a name="configure-server-storage"></a>서버 저장소 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="sample-hard-disk-configurations"></a>샘플 하드 디스크 구성  
 다음 표는 샘플 하드 디스크 구성을 제안합니다. 예상치는 일반적 사용과 기능을 기준으로 하지만 최적 성능에 영향을 미치는 문제는 다루지 않습니다. 고객의 기본 설정과 요구 사항에 따라 이러한 구성에 지원되는 모든 유형의 하드 디스크(예: SATA 또는 SCSI)를 사용할 수 있습니다.  
  
> [!IMPORTANT]
>   C: 볼륨으로 Windows Server Essentials를 설치 해야 하 고 볼륨 크기가 60GB 이상 이어야 합니다. 운영 체제 디스크를 두 개의 파티션으로 나누고 C:(시스템 파티션)에는 비즈니스 데이터를 저장하지 않는 것이 좋습니다.  
  
|서버 수준|디스크 구성|  
|------------------|------------------------|  
|입력|-두 개의 실제 디스크<br /><br /> -다음을 포함 하는 RAID 1 미러링 세트로 구성:<br /><br /> C: 볼륨? 60GB<br /><br /> -D: 볼륨? 1,000 GB|  
|보통|-실제 디스크 3 개<br /><br /> -다음을 포함 하는 RAID 5 세트로 구성:<br /><br /> C: 볼륨? 60GB<br /><br /> -D: 볼륨? 1500GB|  
|높음|-총 5 개 이상의 실제 디스크<br /><br /> -C: 볼륨을 포함 하는 RAID 1 미러링 집합 두 개의 디스크? 100GB<br /><br /> -다음을 포함 하는 RAID 5 집합에서 모든 남은 디스크:<br /><br /> -D: 볼륨? 1500GB<br /><br /> -E: 볼륨? 1500GB|  
  
 이러한 권장 사항은 설치된 운영 체제의 크기, 서버에서 사용하는 데이터 저장소의 평균 크기 및 서버 사용 수명 동안 예상되는 데이터 저장소의 증가를 고려한 것입니다. 볼륨은 단일 실제 디스크에 있는 여러 파티션이거나 별도의 실제 디스크에 둘 수 있습니다. 서버에 고객을 위해 중요 한 데이터를 저장 하므로 여러 실제 디스크를 사용 하 고 하드웨어 RAID 또는 저장소 공간을 사용 하 여 고객의 데이터를 보호 하는 데 도움이 되는 것이 좋습니다.  
  
## <a name="configuring-your-server-backup"></a>서버 백업 구성  
 서버에 있는 내부 하드 디스크 이외에 고객은 외부 USB 하드 디스크를 백업에 사용할 수 있습니다. 이상적인 경우 고객은 서버의 모든 데이터를 백업할 만한 충분한 공간을 가진 최소 두 개 이상의 외부 하드 디스크를 사용합니다. 외부 하드 디스크를 사용하는 경우 고객은 매일 밤 하나의 디스크를 오프사이트로 이동하여 데이터를 추가적으로 보호할 수 있습니다.  
  
## <a name="partition-configuration"></a>파티션 구성  
 서버의 초기 구성 동안 공유 폴더 및 클라이언트 컴퓨터 백업 폴더를 포함하는 일련의 기본 서버 폴더가 디스크 0의 가장 큰 데이터 파티션에 만들어집니다.  
  
## <a name="see-also"></a>관련 항목  

 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK 시작 하기](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포용 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

