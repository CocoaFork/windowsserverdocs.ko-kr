---
title: bootcfg timeout
description: '**Bootcfg timeout** 에 대 한 Windows 명령 항목-운영 체제의 시간 제한 값을 변경 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94bc2de43dd179117c7a44747961213d12741a09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379872"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

운영 체제의 시간 제한 값을 변경 합니다.

## <a name="syntax"></a>구문
```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```
## <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                                                                                                                                  설명                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /timeout <timeOutValue> | [부팅 로더] 섹션에서 시간 제한 값을 지정합니다. <timeOutValue> 사용자는 NTLDR 기본값을 로드 하기 전에 운영 체제를 부팅 로더 화면에서 선택 해야 하는 시간 (초)입니다. 유효 범위 <timeOutValue> 는 0-999입니다. 값이 0 이면 NTLDR 즉시 시작 기본 운영 체제 부트 로더 화면을 표시 하지 않고 있습니다. |
|      /s <computer>      |                                                                                                                               이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                                                               |
|    /u < 도메인 > \ 사용자     |                                                                                       지정 된 사용자의 계정 권한으로 명령을 실행 <User> 또는 도메인 \ < 사용자 >. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                                                                                        |
|      /p <Password>      |                                                                                                                                            지정 된 <Password> 에 지정 된 사용자 계정의 **/u** 매개 변수입니다.                                                                                                                                             |
|           /?            |                                                                                                                                                                      명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                      |

## <a name="BKMK_examples"></a>예와
다음 예제에서는 사용 하는 방법을 보여는 **bootcfg /timeout** 명령:
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
