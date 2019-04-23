---
title: 복제에 참여 하려면 장애 조치 클러스터의 서버에서에서 구성 하는 Hyper-v 복제본 브로커 있어야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d4966396af955f9c8bad34b5b2892115e93c3b85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887974"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>복제에 참여 하려면 장애 조치 클러스터의 서버에서에서 구성 하는 Hyper-v 복제본 브로커 있어야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*장애 조치 클러스터에서 Hyper-v 복제본 개별 서버 이름 대신 Hyper-v 복제본 브로커 이름 사용에 필요합니다.*  
  
## <a name="impact"></a>영향  
*가상 머신을 다른 장애 조치 클러스터 노드로 이동는 경우 복제를 계속할 수 없습니다.*  
  
## <a name="resolution"></a>해결 방법  
*장애 조치 클러스터 관리자를 사용 하 여 Hyper-v 복제본 브로커를 구성 합니다. Hyper-v 관리자에서 복제 구성을 Hyper-v 복제본 브로커 이름을 사용 하 여 서버 이름으로 확인 합니다.*  
  


