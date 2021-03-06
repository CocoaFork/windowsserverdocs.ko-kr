---
title: more
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/26/2019
ms.openlocfilehash: d505f99511d8702f11ac0c70edba3d62c8cf7996
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373911"
---
# <a name="more"></a>more



한 번에 한 화면씩 출력을 표시합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
<Command> | more [/c] [/p] [/s] [/t<N>] [+<N>]
more [[/c] [/p] [/s] [/t<N>] [+<N>]] < [<Drive>:][<Path>]<FileName>
more [/c] [/p] [/s] [/t<N>] [+<N>] [<Files>]
```

## <a name="parameters"></a>매개 변수

|           매개 변수            |                               설명                               |
|--------------------------------|-------------------------------------------------------------------------|
|           \<명령 >           |      출력을 표시 하려는 명령을 지정 합니다.      |
|               /c               |               페이지를 표시 하기 전에 화면을 지웁니다.               |
|               /p               |                      용지 공급 문자를 확장 합니다.                      |
|               /s               |          비어 있는 단일 선으로 여러 개의 빈 줄을 표시합니다.          |
|             /t\<N >             |         탭 하 여 지정 된 공백 수로 표시 *N*합니다.         |
|             +\<N >              |     지정한 줄에서 첫 번째 파일 시작을 표시 *N*합니다.     |
| [\<드라이브 >:] [\<Path >]\<파일 이름 > |          표시할 파일의 이름과 위치를 지정 합니다.          |
|            \<파일 >            | 표시할 파일의 목록을 지정 합니다. 파일 이름을 공백으로 구분 합니다. |
|               /?               |                  명령 프롬프트에 도움말을 표시합니다.                   |

## <a name="remarks"></a>설명

-   에 다음 하위 명령 들은 **더** 프롬프트 (`-- More --`). 

    | Key | 작업 |
    | --- | ------ |
    | 스페이스바 | 다음 페이지를 표시합니다. |
    | Enter 키 | 다음 줄을 표시합니다. |
    | f | 다음 파일이 표시 됩니다. |
    | q | 종료는 **자세한** 명령입니다. |
    | = | 줄 번호를 보여 줍니다. |
    | p \<N > | 다음 표시 *N* 선입니다. |
    | s \<N > |S kips는 다음 *N 개* 줄입니다. |
    | ? | 사용할 수 있는 명령이 표시는 **자세한** 프롬프트입니다.| 
    
-   리디렉션 문자 ( **<** )를 사용 하는 경우 파일 이름을 원본으로 지정 해야 합니다. 파이프 ( **\|** )를 사용 하는 경우 **dir**, **sort**및 **type**과 같은 명령을 사용할 수 있습니다.
-   **자세한** 다른 매개 변수와 함께 명령을 복구 콘솔에서 사용할 수 있습니다.

## <a name="BKMK_examples"></a>예와

첫 번째 화면 Clients.new 라는 파일에 대 한 정보를 보려면 다음 명령 중 하나를 입력 합니다.
```
more < clients.new
type clients.new | more
```
**자세한** 명령은 첫 번째 화면에서 Clients.new, 정보를 표시 하 고 다음 프롬프트를 표시 합니다.
```
-- More --
```
다음 정보는 다음 화면이 표시 하려면 스페이스바를 눌러 수 있습니다.

화면을 지우고 Clients.new 파일을 표시 하기 전에 빈 줄을 모두 제거를 다음 명령 중 하나를 입력 합니다.
```
more /c /s < clients.new
type clients.new | more /c /s
```
**자세한** 명령은 첫 번째 화면에서 Clients.new, 정보를 표시 하 고 다음 프롬프트를 표시 합니다.
```
-- More --
```

### <a name="using-more-subcommands"></a>더 많은 하위 명령을 사용 하 여

다음 예제에서 사용할 수는 **자세한** 프롬프트 (`-- More --`).
- 파일 한 줄을 한 번에 표시 하려면에서 ENTER 키를 눌러는 **자세한** 프롬프트입니다.
- 다음 화면을 표시 하려면 스페이스바를에 **자세한** 프롬프트입니다.
- 명령줄에 나열 된 다음 파일을 표시 하려면 다음을 입력 **f** 에 **자세한** 프롬프트입니다.
- 사용 가능한 명령에 표시 하려면 입력 **?** 에 **자세한** 프롬프트입니다.
- 취소 하려면 **자세한**, 형식 **q** 에 **자세한** 프롬프트입니다.
- 현재 줄 번호를 표시 하려면 입력 **=** 에 **자세한** 프롬프트입니다. 현재 줄 번호에 추가 되는 **더 많은** 다음과 같이 메시지를 표시 합니다.  
  ```
  -- More [Line: 24] --
  ```  
- 특정 줄 수를 표시 하려면 입력 **p** 에 **자세한** 프롬프트입니다. **더 많은** 다음과 같이 표시할 줄 수에 대 한 라는 메시지를 표시 합니다.  
  ```
  -- More -- Lines:
  ```  
  표시할 줄 번호를 입력 하 고 enter 키를 누릅니다. **더 많은** 지정 된 개수의 줄을 표시 합니다.
- 특정 개수의 줄을 건너뛰려면 입력 **s** 에 **자세한** 프롬프트입니다. **더 많은** 묻는 메시지가 표시 하지 않으려면 다음과 같이 줄 수 있습니다.  
  ```
  -- More -- Lines:
  ```  
  건너뛸, 줄 번호를 입력 하 고 enter 키를 누릅니다. **더 많은** 지정 된 개수의 줄을 건너뛰고 다음 화면을 표시 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
