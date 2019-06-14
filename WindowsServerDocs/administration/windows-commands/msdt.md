---
title: msdt
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba411cf73026afe9990e5c32824e3dc277507891
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437235"
---
# <a name="msdt"></a>msdt



명령줄에서 또는 자동화 된 스크립트의 일부로 문제 해결 팩을 호출 하 고 사용자 입력 없이 추가 옵션을 활성화 합니다.

## <a name="syntax"></a>구문

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>매개 변수

다음 표에서 매개 변수 및 msdt.exe에서 지 원하는 옵션을 포함 합니다.


|      매개 변수      |                                                                                            설명                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id \<패키지 이름 > |        실행 하는 진단 패키지를 지정 합니다. 사용 가능한 패키지 목록을 문제 해결 팩 ID를 "문제 해결 팩 사용 가능을 참조 하세요? 이 항목 뒷부분의 섹션입니다.         |
|  /path \<directory  |                                                                                           .diagpkg 파일                                                                                            |
|   /dci \<passkey>   |                                        Msdt 암호 필드를 미리 채우면 됩니다. 이 매개 변수 지원 공급자가 암호를 제공 하는 경우에 사용 됩니다.                                         |
|  /dt \<directory>   | 지정된 된 디렉터리에서 문제 해결 기록이 표시 됩니다. 사용자에 저장 된 진단 결과 **%LOCALAPPDATA%\Diagnostics** 하거나 **%LOCALAPPDATA%\ElevatedDiagnostics** 디렉터리입니다. |
| /af \<answer file>  |                                               하나 이상의 진단 상호 작용에 대 한 응답을 포함 하는 XML 형식으로 응답 파일을 지정 합니다.                                               |

