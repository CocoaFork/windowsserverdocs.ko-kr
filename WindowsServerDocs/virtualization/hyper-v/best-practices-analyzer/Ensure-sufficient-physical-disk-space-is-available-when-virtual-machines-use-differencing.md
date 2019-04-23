---
title: 차이점 보관용 가상 하드 디스크를 사용 하는 가상 컴퓨터 때 충분 한 실제 디스크 공간을 사용할 수
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6d4d219402cdc321a75cc27d75ea7749eb6127e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855574"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>차이점 보관용 가상 하드 디스크를 사용 하는 가상 컴퓨터 때 충분 한 실제 디스크 공간을 사용할 수

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
*하나 이상의 가상 컴퓨터는 차이점 보관용 가상 하드 디스크를 사용 합니다.*  
  
## <a name="impact"></a>영향  
*차이점 보관용 가상 하드 디스크는 가상 하드 디스크에 대 한 쓰기 발생 하면 공간을 할당할 수 있도록 호스팅 볼륨의 사용 가능한 공간을 필요 합니다. 사용 가능한 공간이 부족 한 상태에서 물리적 저장소를 사용 하는 모든 가상 컴퓨터를 저하 될 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 하드 디스크 확장에 대 한 사용 가능한 공간이 충분 한지 확인 하려면 사용 가능한 디스크 공간을 모니터링 합니다. 차이점 보관용 가상 하드 디스크의 부모에 병합 하는 것이 좋습니다. Hyper-v 관리자에서 부모 가상 하드 디스크를 확인 하려면 차이점 보관용 디스크를 검사 합니다. 다른 차이점 보관용 디스크에서 공유 하는 부모 디스크를 차이점 보관용 디스크를 병합 하는 경우 해당 작업에는 다른 차이점 보관용 디스크와 사용할 수 없게 하는 부모 디스크 간의 관계를 손상 됩니다. 부모 가상 하드 디스크 공유 되지 않은 확인 한 후 부모 가상 하드 디스크를 차이점 보관용 디스크를 병합 하려면 디스크 편집 마법사를 사용할 수 있습니다.*  
  


