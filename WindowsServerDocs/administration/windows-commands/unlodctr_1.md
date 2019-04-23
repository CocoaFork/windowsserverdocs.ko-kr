---
title: unlodctr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1a662da10acc65b4ad2fd0d055cf9d46de603be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886654"
---
# <a name="unlodctr"></a>unlodctr

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템 레지스트리에서 성능 카운터 이름 및 서비스 또는 장치 드라이버에 대 한 설명 텍스트를 제거합니다.   

## <a name="syntax"></a>구문  
```  
Unlodctr <DriverName>   
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|\<DriverName>|제거는 성능 카운터 이름 설정 및 드라이버 또는 서비스에 대 한 텍스트 설명 <DriverName> Windows Server 2003 레지스트리에서 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>설명  
> [!WARNING]  
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.  

텍스트가 주위에 따옴표를 사용 하 여 사용자가 제공 하는 정보에 공백이 포함 되 면 (예를 들어 "<DriverName>").  

## <a name="BKMK_Examples"></a>예제  
현재 성능 레지스트리 설정을 제거한 SMTP Simple Mail Transfer Protocol () 서비스에 대 한 설명 텍스트를 카운터:  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
