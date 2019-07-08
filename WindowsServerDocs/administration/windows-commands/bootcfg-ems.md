---
title: bootcfg ems
description: Windows 명령 항목에 대 한 **bootcfg ems** -추가 하거나 원격 컴퓨터에 응급 관리 서비스 콘솔의 리디렉션에 대 한 설정을 변경할 수 있습니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57abdc50-c64a-45f1-8470-3f8c3a51f743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d971fab552b321d54899b418eac4f54c4665ccb7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434742"
---
# <a name="bootcfg-ems"></a>bootcfg ems

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자를 추가 하 여 원격 컴퓨터에 응급 관리 서비스 콘솔의 리디렉션에 대 한 설정을 변경할 수 있습니다. 응급 관리 서비스를 사용 하 여 추가 "리디렉션 = Port #" 줄의 Boot.ini 파일 및 지정 된 운영 체제 항목 줄을입니다 옵션 [부팅 로더] 섹션에 있습니다. 응급 관리 서비스 기능은 서버에만 사용 됩니다.

## <a name="syntax"></a>구문
```
bootcfg /ems {ON | OFF | edit} [/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>매개 변수

|                            매개 변수                             |                                                                                                                                                                                                                                                                                                                                                              설명                                                                                                                                                                                                                                                                                                                                                              |
|------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    {ON &#124; OFF&#124; 편집}                    | 응급 관리 서비스 리디렉션에 대 한 값을 지정합니다.<br /><br />**ON** -지정 된 원격 출력 활성화 <OSEntryLineNum>합니다. 지정 된을입니다 옵션을 추가 <OSEntryLineNum> 및 리디렉션이 = com<X> [부팅 로더] 섹션을 설정 합니다. Com 값<X> 에 의해 설정 됩니다는 **/포트** 매개 변수입니다.<br /><br />**OFF** -원격 컴퓨터에 대 한 출력을 사용 하지 않도록 설정 합니다. 지정 된 위치에서입니다 옵션을 제거 <OSEntryLineNum> 리디렉션 = com<X> [부팅 로더] 섹션에서 설정 합니다.<br /><br />**편집할** -리디렉션 변경 하 여 포트 설정을 사용 하면 com =<X> [부팅 로더] 섹션에서 설정 합니다. Com 값<X> 에 지정 된 값으로 다시 설정 되는 **/포트** 매개 변수입니다. |
|                          /s <computer>                           |                                                                                                                                                                                                                                                                                                          이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                                                                                                                                                                                                                                           |
|                       /u <Domain>\\<User>                        |                                                                                                                                                                                                                                                                 지정한 사용자의 계정 권한으로 명령을 실행 <User> 나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                                                                                                                                                                                                                                                                  |
|                          /p <Password>                           |                                                                                                                                                                                                                                                                                                                         에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                                                                                                                                                                                                                                         |
| / {COM1 &#124; 포트 COM2 &#124; COM3 &#124; COM4 &#124; BIOSSET}  |                                                                                                                                                                                                                              리디렉션에 사용할 COM 포트를 지정 합니다. **BIOSSET** 리디렉션에 사용할 포트를 확인 하 고 BIOS 설정을 가져오려는 응급 관리 서비스에 지시 합니다. 사용 하지 않는 **/포트** 출력을 원격으로 관리 하는 경우 매개 변수는 사용할 수 없습니다.                                                                                                                                                                                                                              |
| /baud {9600 &#124; 19200 &#124; 38400&#124; 57600 &#124; 115200} |                                                                                                                                                                                                                                                                                               리디렉션에 사용할 전송 속도 지정 합니다. 사용 하지 않는 **/baud** 출력을 원격으로 관리 하는 경우 매개 변수는 사용할 수 없습니다.                                                                                                                                                                                                                                                                                               |
|                       /id <OSEntryLineNum>                       |                                                                                                                                                                                              응급 관리 서비스 옵션 Boot.ini 파일의 [운영 체제] 섹션에 추가 된 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. 응급 관리 서비스 값으로 설정 된 경우이 매개 변수는 필수 **ON** 또는 **OFF**합니다.                                                                                                                                                                                              |
|                                /?                                |                                                                                                                                                                                                                                                                                                                                                 명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                                                                                  |

## <a name="BKMK_examples"></a>예제
다음 예제에서는 사용 하는 방법을 보여는 **bootcfg /ems** 명령:
```
bootcfg /ems on /port com1 /baud 19200 /id 2 
bootcfg /ems on /port biosset /id 3 
bootcfg /s srvmain /ems off /id 2 
bootcfg /ems edit /port com2 /baud 115200 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
