---
title: choice
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c65a9119-410b-4dcf-9fa7-4e07d2a7238b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e710b3813525647053365ebf4c764181fc38b3f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379365"
---
# <a name="choice"></a>choice



일괄 처리 프로그램에서 단일 문자 선택 목록에서 항목을 하나 선택 하 라는 메시지 하 고 선택 된 항목의 인덱스를 반환 합니다. 매개 변수 없이 사용 하는 경우 **선택한** 기본 선택 항목을 표시 **Y** 및 **N**합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
choice [/c [<Choice1><Choice2><…>]] [/n] [/cs] [/t <Timeout> /d <Choice>] [/m <"Text">]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/c \<Choice1 > <Choice2> < ... >|만들려는 선택 목록을 지정 합니다. 유효한 선택 항목 a-z, A-Z, 0-9 및 확장된 ASCII 문자 (128-254)를 포함 합니다. 기본 목록은 "YN"으로 표시 되는 `[Y,N]?`합니다.|
|/n|중에서 선택할 수는 여전히 사용할 수 있지만 선택 목록이 숨깁니다 메시지 텍스트 (지정 된 경우 **/m**) 계속 표시 됩니다.|
|/cs|선택 항목은 대/소문자 구분을 지정 합니다. 기본적으로 선택 항목은 대/소문자 구분 하지 않습니다.|
|/t \<Timeout >|사용 하 여 지정 된 기본 선택 하기 전에 일시 중지 시간 (초)의 수를 지정 **/d**합니다. 사용할 수 있는 값은 **0** 에 **9999**합니다. 경우 **/t** 로 설정 된 **0**, **선택** 기본 선택 항목을 반환 하기 전에 일시 중지 되지 않습니다.|
|/d \<Choice >|기본 선택으로 지정 된 초 수를 대기한 후 사용 하 여 지정 **/t**합니다. 기본적으로 선택 하 여 지정 된 선택 항목 목록에 있어야 합니다. **/c**합니다.|
|/m < "text" >|선택 항목의 목록 앞에 표시할 메시지를 지정 합니다. 경우 **/m** 를 지정 하지 않으면만 선택 프롬프트가 표시 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   ERRORLEVEL 환경 변수는 사용자가 선택 목록에서 선택 하는 키의 인덱스에 설정 됩니다. 목록에서 첫 번째 선택 값이 1, 두 번째는 2, 등에 대 한 값을 반환합니다. 사용자가 적절 한 선택 되지 않은 키를 누르면 **선택한** 경고 경고음 보이기도 합니다. 경우 **선택한** 오류 조건이 검색 255 ERRORLEVEL 값을 반환 합니다. 사용자가 CTRL + BREAK 또는 CTRL + C를 누르면 **선택한** ERRORLEVEL 값 0을 반환 합니다.

> [!NOTE]
> 일괄 프로그램에서 ERRORLEVEL 값을 사용 하는 경우 내림차순으로 나열 합니다.

## <a name="BKMK_examples"></a>예와

선택 항목을 제공 Y, N, 및 C, 배치 파일에서 다음 줄을 입력 합니다.
```
choice /c ync
```
다음 메시지가 표시 되는 배치 파일을 실행 하는 경우는 **선택** 명령:
```
[Y,N,C]?
```
Y, N 및 C, 선택 항목을 숨기지만 텍스트를 표시 하려면 "예, 아니요 또는 계속"을 배치 파일에서 다음 줄을 입력 합니다.
```
choice /c ync /n /m "Yes, No, or Continue?"
```
다음 메시지가 표시 되는 배치 파일을 실행 하는 경우는 **선택** 명령:
```
Yes, No, or Continue?
```

> [!NOTE]
> 사용 하는 경우는 **/n** 매개 변수를 하지만 사용 하지 않습니다 **/m**, 사용자가 아닌 메시지 표시 **선택** 입력을 기다리고 있습니다.

텍스트와 앞의 예제에 사용 되는 옵션을 표시 하려면 배치 파일에서 다음 명령줄을 입력 합니다.
```
choice /c ync /m "Yes, No, or Continue"
```
다음 메시지가 표시 되는 배치 파일을 실행 하는 경우는 **선택** 명령:
```
Yes, No, or Continue [Y,N,C]?
```
5 초 시간 제한 설정 지정 **N** 값을 기본값으로 배치 파일에서 다음 줄을 입력 합니다.
```
choice /c ync /t 5 /d n
```
다음 메시지가 표시 되는 배치 파일을 실행 하는 경우는 **선택** 명령:
```
[Y,N,C]?
```

> [!NOTE]
> 이 예제에서는 사용자 5 초 이내에 키를 누르지 않습니다 **선택** 선택 **N** 기본적으로 2의 오류 값을 반환 합니다. 그렇지 않으면 **선택** 해당 사용자의 선택 하는 값을 반환 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)