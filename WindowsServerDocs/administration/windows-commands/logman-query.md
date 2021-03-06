---
title: logman 쿼리
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1116a0f0-5415-4369-a045-12f79f8f66de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6acf6cf5240dd59357f4c788577190699a354744
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374423"
---
# <a name="logman-query"></a>logman 쿼리

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터 수집기 또는 데이터 수집기 집합 속성을 쿼리 합니다.  

## <a name="syntax"></a>구문  
```  
logman query [providers|"Data Collector Set name"] [options]  
```  
## <a name="parameters"></a>매개 변수  

|     매개 변수      |                                 설명                                  |
|--------------------|------------------------------------------------------------------------------|
|         /?         |                       도움말 상황에 맞는 표시 합니다.                       |
| -s <computer name> |            지정된 된 원격 컴퓨터에서 명령을 수행 합니다.             |
|  -config <value>   |           명령 옵션을 포함 하는 설정 파일을 지정 합니다.            |
|    [-n] <name>     |                          대상 개체의 이름입니다.                          |
|        -ets        | 이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다. |

## <a name="BKMK_examples"></a>예와  
다음 명령은 대상 시스템에 구성 된 모든 데이터 수집기 집합을 나열 합니다.  
```  
logman query  
```  
다음 명령은 perf_log 데이터 수집기 집합에 포함 된 데이터 수집기를 나열 합니다.  
```  
logman query "perf_log"  
```  
다음 명령은 대상 시스템에 데이터 수집기의 모든 사용 가능한 공급자를 나열 합니다.  
```  
logman query providers  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
