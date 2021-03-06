---
title: rd
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e672f6-5bc2-4c16-af25-18e7ed2dd555
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 029935bcd8773e41adefcd6ca916d75edcea3065
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371804"
---
# <a name="rd"></a>rd



디렉터리를 삭제합니다. 이 명령은 같습니다는 **rmdir** 명령입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
rd [<Drive>:]<Path> [/s [/q]]
rmdir [<Drive>:]<Path> [/s [/q]]
```

## <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                 설명                                                                  |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive >:] <Path> |                      삭제 하려는 디렉터리의 이름과 위치를 지정 합니다. *경로* 가 필요 합니다.                       |
|        /s         |                     (지정된 된 디렉터리 및 모든 파일을 비롯 한 모든 하위) 디렉터리 트리를 삭제 합니다.                      |
|        /q         | 자동 모드를 지정합니다. 디렉터리 트리를 삭제할 때 확인 표시 하지 않습니다. (유의 **/q** 경우에만 사용할 **/s** 지정 됩니다.) |
|        /?         |                                                     명령 프롬프트에 도움말을 표시합니다.                                                     |

## <a name="remarks"></a>설명

-   포함 하 여 파일을 포함 하는 디렉터리를 삭제할 수 없습니다 숨겨진 또는 시스템 파일입니다. 이렇게 하려고 하면 다음과 같은 메시지가 나타납니다.

    `The directory is not empty`

    모든 파일 (숨겨진 파일 및 시스템 파일 포함)을 나열 하려면 **dir/a** 명령을 사용 합니다. 다음 사용 하 여는 **attrib** 명령과 **-h** 숨겨진된 파일 특성을 제거 하려면 **-s** 시스템 파일 특성을 제거 하려면 또는 **-h-s** 모두 분리 숨김 및 시스템 파일 특성을 합니다. 숨겨진 후 및 파일 특성을 제거한, 파일을 삭제할 수 있습니다.
-   *경로의*시작 부분에 백슬래시 (\)을 삽입 하는 경우 *경로* 는 현재 디렉터리에 관계 없이 루트 디렉터리에서 시작 됩니다.
-   사용할 수 없습니다 **rd** 현재 디렉터리를 삭제 합니다. 현재 디렉터리를 삭제 하려고 하면 다음과 같은 오류 메시지가 나타납니다.

    `The process cannot access the file because it is being used by another process.`

    이 오류 메시지가 표시 되는 경우 다른 디렉터리 (현재 디렉터리의 하위 디렉터리 아님)로 변경한 다음 **rd** (필요한 경우 *경로* 지정)을 사용 해야 합니다.
-   **rd** 다른 매개 변수와 함께 명령을 복구 콘솔에서 사용할 수 있습니다.

## <a name="BKMK_examples"></a>예와

현재 작업 디렉터리를 삭제할 수 없습니다. 현재 디렉터리에 속하지 않는 디렉터리를 변경 해야 합니다. 예를 들어 부모 디렉터리를 변경 하려면 다음을 입력 합니다.
```
cd ..
```
이제 원하는 디렉터리를 안전 하 게 제거할 수 있습니다.

사용 된 **/s** 디렉터리 트리를 제거할 수 있습니다. 예를 들어 디렉터리를 제거 라는 테스트 (모든 하위 디렉터리 및 파일) 현재 디렉터리에서 유형:
```
rd /s test
```
자동 모드에서 앞의 예제를 실행 하려면 다음을 입력 합니다.
```
rd /s /q test
```

> [!CAUTION]
> 실행 하는 경우 **rd /s** 자동 모드에서 전체 디렉터리 트리가 확인 없이 삭제 됩니다. 중요 한 파일이 옮겨졌거나 사용 하기 전에 백업 확인은 **/q** 명령줄 옵션입니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)