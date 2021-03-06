---
title: 전화
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d34a41dc-e6c7-4467-bf6a-15cec704833e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: 89097ec5d3711b3d8831f8c33b3778ed0752246f
ms.sourcegitcommit: ee8fa8e1293f29229b5ce1b0f3d4a07ba99568f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280194"
---
# <a name="call"></a>전화



상위 일괄 프로그램을 중지 하지 않고 다른 하나의 일괄 처리 프로그램을 호출 합니다. **호출** 명령 호출 대상으로 레이블을 받아들입니다.

> [!NOTE]
> **호출** 아무런 효과도 명령 프롬프트에서 스크립트 또는 배치 파일 외부에서 사용 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
call [Drive:][Path]<FileName> [<BatchParameters>] [:<Label> [<Arguments>]]
```

## <a name="parameters"></a>매개 변수

|           매개 변수           |                                                                         설명                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<드라이브 >:] [\<Path >]<FileName> | 호출 하려는 일괄 프로그램의 이름과 위치를 지정 합니다. *FileName* 매개 변수는 필수 되며 확장명이.bat 또는.cmd 있어야 합니다. |
|      BatchParameters \<>       |                                            일괄 처리 프로그램에 필요한 명령줄 정보를 지정 합니다.                                             |
|           :\<레이블 >           |                                            이동할 일괄 프로그램 제어를 원하는 레이블을 지정 합니다.                                             |
|         \<인수 >          |                     부터 배포 프로그램의 새 인스턴스를 전달 하도록 명령줄 정보를 지정 *: 레이블 합니다.*                     |
|              /?               |                                                             명령 프롬프트에 도움말을 표시합니다.                                                             |

## <a name="batch-parameters"></a>일괄 처리 매개 변수

일괄 처리 스크립트 인수 참조 ( **%0**, **%1**, ...)는 다음 표에 나열 됩니다.

일괄 처리 스크립트의 **%\*** 는 모든 인수를 참조 합니다 (예: **%1**, **%2**, **%3**...).

일괄 처리 매개 변수에 대 한 다음과 같은 선택적 구문을 대신 사용할 수 있습니다 ( **%n% n**):

|일괄 매개 변수|설명|
|---------------|-----------|
|% ~ 1|확장 **%1** 주변 따옴표를 제거 하 고 ("").|
|% ~ f1|확장 **%1** 정규화 된 경로에 있습니다.|
|% ~ d 1|확장 **%1** 드라이브 문자로 합니다.|
|% ~ p1|확장 **%1** 만 경로에 있습니다.|
|% ~ n1|확장 **%1** 만 파일 이름으로 저장 합니다.|
|% ~ x1|확장 **%1** 파일 이름 확장명으로 합니다.|
|% ~ s1|확장 **%1** 짧은 이름만 포함 하는 정규화 된 경로입니다.|
|% ~ a1|확장 **%1** 파일 특성에 있습니다.|
|% ~ t1|확장 **%1** 파일의 시간과 날짜를 합니다.|
|% ~ z1|확장 **%1** 파일의 크기입니다.|
|% ~ $PATH: 1|PATH 환경 변수에 나열 된 디렉터리를 검색 하 고 확장 **%1** 찾을 첫 번째 디렉터리의 정규화 된 이름에 있습니다. 환경 변수 이름이 정의 되지 않은 경우 파일은 검색에서 찾을 수 없습니다이 한정자는 빈 문자열로 확장 됩니다.|

다음 표에서 복합 결과 대 한 일괄 처리 매개 변수 한정자를 결합 하는 방법과 보여 줍니다.

|일괄 매개 변수 한정자|설명|
|-----------------------------|-----------|
|% ~ dp1|확장 **%1** 드라이브 문자와 경로를 합니다.|
|% ~ nx1|확장 **%1** 파일 이름과 확장명 전용입니다.|
|% ~ dp$ 경로: 1|에 대 한 PATH 환경 변수에 나열 되는 디렉터리 검색 **%1**, 을 드라이브 문자와 찾을 수 있는 첫 번째 디렉터리의 경로를 확장 하 여 합니다.|
|% ~ ftza1|확장 **%1** 유사한 출력을 표시 하는 **dir** 명령입니다.|

위의 예제에서 **%1** 경로 다른 유효한 값으로 대체 될 수 있습니다. <strong>%~</strong>  구문에 유효한 인수가 숫자 종료 됩니다. <strong>%~</strong> 한정자는 **%\*** 와 함께 사용할 수 없습니다.

## <a name="remarks"></a>주의

-   일괄 처리 매개 변수 사용

    일괄 처리 매개 변수는 명령줄 옵션, 파일 이름, 일괄 처리 매개 변수 **%0** - **%9**및 변수 (예: **% 전송%** )를 포함 하 여 일괄 프로그램에 전달할 수 있는 모든 정보를 포함할 수 있습니다.
-   *레이블* 매개 변수 사용

    *Label* 매개 변수와 함께 **call** 을 사용 하 여 새 일괄 처리 파일 컨텍스트를 만들고 지정 된 레이블 뒤에 있는 문에 제어를 전달 합니다. 배치 파일의 끝에 도달 하는 처음으로 (즉, 이동한 후 레이블에), 다음 문으로 제어가 반환는 **호출** 문입니다. 배치 파일의 끝에 도달 하는 두 번째 시간 배치 스크립트가 종료 됩니다.
-   파이프 및 리디렉션 기호 사용

    **호출**에 파이프 ( **|** ) 및 리디렉션 기호 ( **<** 또는 **>** )를 사용 하지 마십시오.
-   재귀 호출 만들기

    자신을 호출 하는 일괄 처리 프로그램을 만들 수 있습니다. 그러나 종료 조건을 제공 해야 합니다. 그렇지 않으면 부모 및 자식 일괄 프로그램 끊임없이 루프 수 있습니다.
-   명령 확장 사용

    명령 확장을 사용 하는 경우 호출의 대상으로 허용 *레이블을* **호출** 합니다. 올바른 구문은 다음과 같습니다.

    `call :<Label> <Arguments>`

## <a name="BKMK_examples"></a>예와

일괄 처리의 다른 프로그램에서 Checknew.bat 프로그램을 실행 하려면 부모 일괄 프로그램에서 다음 명령을 입력 합니다.
```
call checknew
```
두 개의 일괄 처리 매개 변수를 수락 하는 상위 일괄 프로그램 Checknew.bat에 이러한 매개 변수를 전달 하려는 경우 부모 일괄 프로그램에서 다음 명령을 입력 합니다.
```
call checknew %1 %2
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
