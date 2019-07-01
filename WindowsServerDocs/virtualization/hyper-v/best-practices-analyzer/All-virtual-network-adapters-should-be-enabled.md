---
title: 모든 가상 네트워크 어댑터를 사용 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0a769c3203f6c6946f01cd91b66fbec38af83bbd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837134"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>모든 가상 네트워크 어댑터를 사용 해야

>적용 대상: Windows Server 2016


  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*실제 네트워크 어댑터와 연결 된 하나 이상의 가상 네트워크 어댑터는 관리 운영 체제에서 비활성화 되었습니다.*  
  
## <a name="impact"></a>영향  
  
*이 서버의 구성이 최적의 아닙니다.*  
  
관리 운영 체제는 사용 되지 않는 가상 네트워크 어댑터와 연결 하기 때문에이 컴퓨터에 실제 네트워크 어댑터 중 하나를 사용 하는 실제 (외부) 네트워크에 연결할 수 없습니다.  
  
## <a name="resolution"></a>해결 방법  
  
*네트워크 및 인터넷 설정을 사용 하 여 가상 네트워크 어댑터를 사용 하도록 설정 합니다. 또는 가상 스위치 관리자를 사용 하 여 관리 운영 체제와 공유 되지 않습니다 있도록 외부 가상 스위치를 다시 구성 합니다.*  
  

