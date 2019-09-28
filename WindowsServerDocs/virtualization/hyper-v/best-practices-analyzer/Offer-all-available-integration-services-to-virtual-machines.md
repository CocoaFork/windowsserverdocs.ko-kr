---
title: 가상 컴퓨터에 모두 사용할 수 있는 통합 서비스를 제공 합니다.
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5ec2dc73cea8b8356d832bf9fdb960985df2df6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393595"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>가상 컴퓨터에 모두 사용할 수 있는 통합 서비스를 제공 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*하나 이상의 사용 가능한 integration services가 가상 머신에서 사용 하도록 설정 되어 있지 않습니다.*  
  
## <a name="impact"></a>영향  
  
*일부 기능은 다음과 같은 가상 컴퓨터에서 사용할 수 없습니다.*  
  
@no__t-가상 머신 이름의 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*이 의도적인 경우 추가 작업이 필요 하지 않습니다. 그렇지 않은 경우 이러한 가상 컴퓨터의 설정에 모든 통합 서비스를 제공 하는 것이 좋습니다.*  
  
가상 컴퓨터 설정을 통해 일부 통합 서비스의 가용성을 관리할 수 있습니다.   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>가상 컴퓨터에 통합 서비스의 가용성을 관리 하려면  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 구성 하려는 가상 컴퓨터를 선택 합니다.  
  
3.  **작업** 창의 가상 컴퓨터 이름에서 **설정**을 클릭합니다.  
  
4.  아래에서 **관리**, 클릭 **Integration Services**합니다.  
  
5.  Integration services의 목록에서 가상 컴퓨터에 제공 하려는 각 서비스에 대 한 확인란을 선택 합니다. 확인란을 사용할 수 없는 경우 해당 특정 통합 서비스는 가상 컴퓨터에서 실행 되는 게스트 운영 체제에서 지원 되지 않습니다.  
  


