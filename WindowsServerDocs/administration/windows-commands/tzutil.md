---
title: tzutil
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 347254bd5a00a8bfb4a80f20d518f1e0e8b593bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392307"
---
# <a name="tzutil"></a>tzutil

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 표준 시간대 유틸리티를 표시 합니다. 
## <a name="syntax"></a>구문
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/?|명령 프롬프트에 도움말을 표시합니다.|
|/g|현재 표준 시간대 ID를 표시 합니다.|
|/s \<timeZoneID > [_dstoff]|지정 된 표준 시간대 ID를 사용 하 여 현재 표준 시간대를 설정 합니다. **_Dstoff** 접미사는 표준 시간대에 대 한 일광 절약 시간 조정을 사용 하지 않도록 설정 합니다 (해당 하는 경우).|
|/l|모든 유효한 표준 시간대 Id 및 표시 이름을 나열 합니다. 출력은 다음과 같습니다.<br /><br />-   \<표시 이름 ><br />-   \<표준 시간대 ID >|

## <a name="remarks"></a>설명
종료 코드 **0** 은 명령이 성공적으로 완료 되었음을 나타냅니다.

## <a name="BKMK_Examples"></a>예와
현재 표준 시간대 ID를 표시 하려면 다음을 입력 합니다.
```
tzutil /g
```
현재 표준 시간대를 태평양 표준시로 설정 하려면 다음을 입력 합니다.
```
tzutil /s Pacific Standard time
```
현재 표준 시간대를 태평양 표준 시간으로 설정 하 고 일광 절약 시간 조정을 사용 하지 않도록 설정 하려면 다음을 입력 합니다.
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)

