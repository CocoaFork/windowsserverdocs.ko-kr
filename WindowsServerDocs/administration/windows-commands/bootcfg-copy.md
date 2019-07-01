---
title: bootcfg copy
description: Windows 명령 항목에 대 한 **bootcfg 복사** -명령줄 옵션을 추가할 수 있는 기존 부팅 항목의 복사본을 만듭니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b76ecfe953d1a462e311fdaaeba35e8f962165c4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434865"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령줄 옵션을 추가할 수 있는 있는 기존 부팅 항목의 복사본을 만듭니다.

## <a name="syntax"></a>구문
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                                             설명                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                          |
| /u <Domain>\\<User>  | 지정한 사용자의 계정 권한으로 명령을 실행 <User>나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
|    /p <Password>     |                                                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                        |
|   /d <Description>   |                                                                    새 운영 체제 항목에 대 한 설명을 지정합니다.                                                                    |
| /id <OSEntryLineNum> |         복사 하려면 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.         |
|          /?          |                                                                                명령 프롬프트에 도움말을 표시합니다.                                                                                 |

## <a name="BKMK_examples"></a>예제
다음 예에서는 사용 하는 방법을 보여 줍니다 합니다 **bootcfg /copy** 부팅 항목 1을 복사 하 고 입력 명령을 "\ABC Server\\" 설명으로:
```
bootcfg /copy /d "\ABC Server\" /id 1
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)