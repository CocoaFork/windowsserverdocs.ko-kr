---
title: 프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 가상 하드 디스크를 차이점 보관용 VHD 포맷을 사용 하지 마십시오
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: da908d00a6b5c48a61dad89e8c7b08cf80b4314c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819184"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 가상 하드 디스크를 차이점 보관용 VHD 포맷을 사용 하지 마십시오

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*하나 이상의 가상 컴퓨터 VHD 형식 차이점 보관용 가상 하드 디스크를 사용 합니다.*  
  
## <a name="impact"></a>**Impact**  
*VHD 형식 차이점 보관용 가상 하드 디스크 전원 오류가 발생 하는 경우 일관성 문제가 발생할 수 있습니다. 실제 디스크 전원 오류가 발생 하면 수정 되는.vhd 파일에는 섹터에 대 한 불완전 하거나 잘못 된 업데이트를 수행 하는 경우 일관성 문제가 발생할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*가상 컴퓨터를 종료 하 고 체인에 VHD 형식 차이점 보관용 가상 하드 디스크를 VHDX 형식으로 변환 하거나 고정 가상 하드 디스크 체인을 병합 합니다. (VHDX 형식은 전원 오류로 인 한 손상을에서 디스크를 보호 하는 데 안정성 메커니즘에 있습니다.) 그러나 이전 버전 Windows의 어느 시점에 연결 될 가능성이 높은 경우에 가상 하드 디스크 변환 하지 않습니다. Windows는 Windows Server 2012 VHDX 형식을 지원 하지 않는 이전의 해제 합니다.*  
  


