---
title: 복제 트래픽에 대 한 압축 것이 좋습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 802f11355bec8903e7f6ab81bf337d38e64513f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833514"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>복제 트래픽에 대 한 압축 것이 좋습니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*복제본 서버에 주 서버에서 네트워크를 통해 전송 되는 복제 트래픽을 압축 아닙니다.*  
  
## <a name="impact"></a>영향  
*복제 트래픽에 필요한 것 보다 더 많은 대역폭을 사용 합니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자에서 가상 컴퓨터의 설정에 네트워크를 통해 전송 되는 데이터를 압축 하려면 Hyper-v 복제본을 구성 합니다. 또한 압축을 수행 하려면 Hyper-v 외부 도구를 사용할 수 있습니다.*  
  


