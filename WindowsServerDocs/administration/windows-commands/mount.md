---
title: 탑재
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65083ce4b7d04129ff630a7f314c458d7ee378f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437241"
---
# <a name="mount"></a>탑재



사용할 수 있습니다 **탑재** 네트워크 파일 시스템 (NFS) 네트워크 공유를 탑재 합니다.

## <a name="syntax"></a>구문

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>설명

합니다 **탑재** 명령줄 유틸리티에서 식별 된 파일 시스템을 탑재 *ShareName* 식별 하는 NFS 서버에서 내보낸 *ComputerName* 연결 합니다 지정 된 드라이브 문자 *DeviceName* 경우에 별표 ( **&#42;** ) 첫 번째 사용 가능한 드라이버 문자로 사용 됩니다. 그런 다음 사용자는 로컬 컴퓨터의 드라이브 것 처럼 내보낸된 파일 시스템을 액세스할 수 있습니다. 인수 또는 옵션 없이 사용할 경우 **탑재** 탑재 된 모든 NFS 파일 시스템에 대 한 정보를 표시 합니다.

**탑재** 유틸리티는 NFS 용 클라이언트가 설치 되어 있는 경우에 사용할 수 있습니다.

다음 옵션 및 인수를 사용할 수는 **탑재** 유틸리티입니다.


|          용어          |                                                                                                                                                                                                                                                정의                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -o rsize=\<buffersize> |                                                                                                                                                                                            (킬로바이트) 읽기 버퍼의 크기를 설정합니다. 허용 가능한 값은 1, 2, 4, 8, 16 및 32입니다. 기본값은 32KB입니다.                                                                                                                                                                                            |
| -o wsize=\<buffersize> |                                                                                                                                                                                           (킬로바이트) 쓰기 버퍼의 크기를 설정합니다. 허용 가능한 값은 1, 2, 4, 8, 16 및 32입니다. 기본값은 32KB입니다.                                                                                                                                                                                            |
| -o timeout=\<seconds>  |                                                                                                                                                                       원격 프로시저 호출 (RPC)을 초 단위로 시간 제한 값을 설정합니다. 허용 가능한 값은 0.8, 0.9 및 1-60; 범위의 모든 정수 기본값은 0.8입니다.                                                                                                                                                                       |
|   -o retry=\<number>   |                                                                                                                                                                                             소프트 탑재에 대 한 재시도 횟수를 설정합니다. 허용 가능한 값은 1-10; 범위에 있는 정수 기본값은 1입니다.                                                                                                                                                                                             |
|     -o mtype={soft     |                                                                                                                                                                                                                                                  hard}                                                                                                                                                                                                                                                   |
|        -o anon         |                                                                                                                                                                                                                                       익명 사용자로 탑재 합니다.                                                                                                                                                                                                                                       |
|       -o nolock        |                                                                                                                                                                                                                                잠금을 사용 하지 않도록 설정 (기본값은 **활성화**).                                                                                                                                                                                                                                |
|    -o casesensitive    |                                                                                                                                                                                                                         강제로 서버 대/소문자 구분에 조회 파일입니다.                                                                                                                                                                                                                          |
| -o fileaccess=\<mode>  | NFS 공유에 만들어진 새 파일의 기본 사용 권한 모드를 지정 합니다. 지정 *모드* 형태로 세 자리 숫자로 *ogw*, 여기서 *o*, *g*, 및 *w* 는 각각 해당 파일의 소유자, 그룹 및 전 세계를 각각 부여 된 액세스를 나타내는 숫자입니다. 다음과 같은 의미를 사용 하 여 범위 0-7 숫자 여야 합니다.</br>-   0: 권한 없음</br>-1: x (실행 액세스)</br>-2: w (쓰기 액세스)</br>-3: wx</br>-4: r (읽기 액세스)</br>-5: rx</br>-6: rw</br>-7: rwx |
|    -o lang={euc-jp     |                                                                                                                                                                                                                                                  tw euc                                                                                                                                                                                                                                                  |
|     -u:\<UserName>     |                                                                                                                                                                             공유를 마운트 하는 데 사용할 사용자 이름을 지정 합니다. 경우 *username* 백슬래시 앞에 나오지 않는 ( **\\** ), UNIX 사용자 이름으로 처리 됩니다.                                                                                                                                                                             |
|     -p:\<Password>     |                                                                                                                                                                                          공유를 마운트 하는 데 사용할 암호입니다. 별표를 사용 하는 경우 ( **&#42;** ), 암호에 대 한 라는 메시지가 표시 됩니다.                                                                                                                                                                                          |

> [!NOTE]