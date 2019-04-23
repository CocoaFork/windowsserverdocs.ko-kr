---
title: sxstrace
description: Side-by-side-문제를 진단 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 396d06bf079c0cfa8ba4864f71333eec39f7b255
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814104"
---
# <a name="sxstrace"></a>sxstrace

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

함께 하 여 문제를 진단합니다.    

## <a name="syntax"></a>구문  
```  
sxstrace [{[trace /logfile:<FileName> [/nostop]|[parse /logfile:<FileName> /outfile:<ParsedFile>  [/filter:<AppName>]}]  
```  

### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|추적|Sxs (side-by-side-)에 대 한 추적 활성화|  
|/logfile|원시 로그 파일을 지정합니다.|  
|\<FileName>|추적 로그가 저장 *FileName*합니다.|  
|/nostop|추적을 중지 하려면 안 함을 지정 합니다.|  
|구문 분석|원시 추적 파일을 변환합니다.|  
|outfile /|출력 파일 이름을 지정합니다.|  
|\<ParsedFile>|구문 분석 된 파일의 파일 이름을 지정합니다.|  
|/filter|출력을을 필터링 할 수 있습니다.|  
|\<AppName>|애플리케이션의 이름을 지정합니다.|  
|stoptrace|전에 중지 하지 않으면 추적을 중지 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="BKMK_Examples"></a>예제  
추적을 설정 하 고 추적 파일을 저장 **sxstrace.etl**:  
```  
sxstrace trace /logfile:sxstrace.etl  
```  
원시 추적 파일을 사람이 읽을 수 있는 형식으로 변환한 결과를 저장할 **sxstrace.txt**:  
```  
sxstrace parse /logfile:sxstrace.etl /outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  