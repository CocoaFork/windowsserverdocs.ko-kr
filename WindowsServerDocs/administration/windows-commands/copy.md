---
title: copy
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9624d4a1-349a-4693-ad00-1d1d4e59e9ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d593fbdbffd2a5ee4e4dfb4a817ad4708162160a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853774"
---
# <a name="copy"></a>copy



다른 한 위치에서 하나 이상의 파일을 복사합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
copy [/d] [/v] [/n] [/y | /-y] [/z] [/a | /b] <Source> [/a | /b] [+<Source> [/a | /b] [+ ...]] [<Destination> [/a | /b]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/d|대상 위치에 암호 해독 된 파일로 저장할 수를 복사 하 고 암호화 된 파일 수 있습니다.|
|/v|새 파일이 쓰여지는지 확인 합니다.|
|/n|8 자 보다 긴 이름 또는 파일 이름 확장명 3 자 보다 긴 파일을 복사 하는 경우 사용 가능한 경우 짧은 파일 이름을 사용 합니다.|
|/y|기존 대상 파일을 덮어쓸 것인지를 확인 하는 메시지를 표시 하지 않습니다.|
|/ y|기존 대상 파일을 덮어쓸 것인지 확인 하 라는 메시지가 표시 됩니다.|
|/z|다시 시작 가능 모드에서 네트워크에 연결 된 파일을 복사 합니다.|
|/ a|ASCII 텍스트 파일을 나타냅니다.|
|/b|이진 파일을 나타냅니다.|
|\<Source>|필수. 파일 또는 파일 집합이 복사 하려는 위치를 지정 합니다. *소스* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다.|
|\<대상 >|필수 사항입니다. 파일 또는 파일 집합이 복사 하려는 위치를 지정 합니다. *대상* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   파일의 끝을 나타내는 파일의 끝 문자 (CTRL + Z)를 사용 하는 ASCII 텍스트 파일을 복사할 수 있습니다.
-   사용 하 여 **/a**

    때 **/a** 이전 또는 이후 목록을 명령줄에서 파일을 적용할 때까지 나열 된 모든 파일 **복사** 발견 **/b**합니다. 이 경우 **/b** 이전 파일에 적용 **/b**합니다.

    효과 **/a** 명령줄 문자열의 해당 위치에 따라 달라 집니다. 때 **/a** 따릅니다 *소스*, **복사** 취급 하는 파일이 ASCII 파일을 첫 번째 파일의 끝 문자 (CTRL + Z) 앞에 있는 데이터를 복사 합니다.

    때 **/a** 따릅니다 *대상*, **복사** 파일의 마지막 문자로 파일의 끝 문자 (CTRL + Z)를 추가 합니다.
-   사용 하 여 **/b**

    **/b** 는 명령 인터프리터가 디렉터리의 파일 크기에 의해 지정 된 바이트 수를 읽을 수 있습니다. **/b** 에 대 한 기본값은 **복사**, 하지 않는 한, **복사** 파일을 결합 합니다.

    때 **/b** 이전 또는 이후 목록을 명령줄에서 파일을 적용할 때까지 나열 된 모든 파일 **복사** 발견 **/a**합니다. 이 경우 **/a** 이전 파일에 적용 **/a**합니다.

    효과 **/b** 명령줄 문자열의 해당 위치에 따라 달라 집니다. 때 **/b** 따릅니다 *소스*, **복사** 모든 파일의 끝 문자 (CTRL + Z)를 포함 하 여 전체 파일을 복사 합니다.

    때 **/b** 따릅니다 *대상*, **복사** 파일의 끝 문자 (CTRL + Z)를 추가 하지 않습니다.
-   사용 하 여 **/v**

    경우 오류 메시지가 나타나면 쓰기 작업을 확인할 수 없습니다. 기록 오류가 거의 발생 하지 않지만 **복사**, 를 사용할 수 있습니다 **/v** 중요 한 데이터가 제대로 기록 되었는지 확인 합니다. **/v** 명령줄 옵션 또한 느려집니다는 **복사** 디스크에 기록 된 각 섹터를 확인 해야 하므로 명령입니다.
-   사용 하 여 **/y** 및 **/y**

    경우 **/y** 미리 설정 되어 /z를 재정의할 수 있습니다이 설정을 사용 하 여 **/y** 명령줄에서. 기본적으로는 메시지가 대체 하면이 설정 하지 않으면는 **복사** 배치 스크립트에서 명령을 실행 합니다.
-   파일 추가

    파일을 추가 하려면, 단일 파일을 지정 *대상*, 여러 파일에 대 한 하지만 *소스* (와일드 카드 문자를 사용 하 여 또는 *File1*+*File2*+*File3* 형식).
-   사용 하 여 **/z**

    연결이 손실 (예를 들어, 오프 라인으로 전환 하는 서버 연결을 끊는 경우), 복사 단계 **/z 복사** 연결이 다시 설정 되 면 다시 시작 됩니다. **/z** 도 각 파일에 대해 완료 하는 복사 작업의 백분율을 표시 합니다.
-   장치에서 복사

    하나 이상의 항목에 대 한 장치 이름을 대체할 수 있습니다 *소스* 또는 *대상*합니다.
-   사용 하 여 하거나 생략 하더라도 **/b** 장치에 복사 하는 경우

    때 *대상* 는 장치 (예를 들어, Com1 또는 Lpt1) **/b** 이진 모드에서 장치에 데이터를 복사 합니다. 이진 모드에서 **/b 복사** 데이터로 장치 모든 문자 (CTRL + C, CTRL + S, CTRL + Z, 및 ENTER 등의 특수 문자 포함)에 복사 합니다. 그러나 생략 하면 **/b**, ASCII 모드로 장치에 데이터를 복사 합니다. 특수 문자는 ASCII 모드로 파일 복사 프로세스 동안 결합 하 여 발생할 수 있습니다.
-   기본 대상 파일을 사용 하 여

    대상 파일을 지정 하지 않으면 복사본을 동일한 이름의 수정한 날짜를 만들어지고 시간 원본 파일을 수정 합니다. 새 복사본은 현재 드라이브에서 현재 디렉터리에 저장 됩니다. 소스 파일은 현재 드라이브 및 현재 디렉터리에 다른 드라이브 또는 대상 파일의 디렉터리를 지정 하지 않으면 경우는 **복사** 명령은 중지 하 고 다음 오류 메시지가 표시 됩니다.

    `File cannot be copied onto itself`

    `0 File(s) copied`
-   파일 결합

    둘 이상의 파일을 지정 하는 경우 *소스*, **복사** 결합 하 여 모든 단일 파일에 지정 된 파일 이름을 사용 하 여 *대상*합니다. **복사** 결합 된 파일을 사용 하지 않는 경우 ASCII 파일로 간주는 **/b** 옵션입니다.
-   길이가 0 인 파일을 복사합니다.

    **복사** 0 바이트 파일을 복사 하지 않습니다. 사용 하 여 **xcopy** 이러한 파일을 복사 합니다.
-   파일의 날짜와 시간을 변경합니다.

    파일을 수정 하지 않고 파일에 날짜와 현재 시간을 변경 하려는 경우에 다음 구문을 사용 합니다.  
    ```
    copy /b <Source> +,,
    ```  
    쉼표는 생략 나타냅니다는 *대상* 매개 변수입니다.
-   하위 디렉터리에 파일을 복사합니다.

    사용 하 여 모든 디렉터리의 파일 및 하위 디렉터리를 복사 하려면는 **xcopy** 명령입니다.
-   **복사** 다른 매개 변수와 함께 명령을 복구 콘솔에서 사용할 수 있습니다.

## <a name="BKMK_examples"></a>예제

현재 드라이브에 다음을로 라는 파일을 복사 하 고 복사 된 파일의 끝에는 파일의 끝 문자 (CTRL + Z) 인지 확인 하려면 다음을 입력 합니다.
```
copy memo.doc letter.doc /a
```
C 드라이브에 있는 라는 기존 디렉터리로 현재 드라이브와 디렉터리의 Robin.typ 라는 파일을 복사 하려면 다음을 입력 합니다.
```
copy robin.typ c:\birds
```
C 드라이브에서 디스크에 루트 디렉터리에 있는 라는 파일에 Robin.typ 파일 복사는 새 디렉터리가 없는 경우

Mar89.rpt, Apr89.rpt, 및 결합 May89.rpt, 현재 디렉터리에 있는 보고서 (현재 디렉터리)에 라는 파일에 배치 되며, 다음을 입력 합니다.
```
copy mar89.rpt + apr89.rpt + may89.rpt Report
```
파일을 결합 하는 경우 **복사** 대상 파일의 현재 날짜와 시간을 표시 합니다. 생략 하면 *대상*, 파일 결합 되 고 목록에서 첫 번째 파일의 이름으로 저장 합니다. 예를 들어 보고서의 모든 파일을 한 Report 라는 파일이 이미 존재 하는 경우 결합 하려면 다음을 입력 합니다.
```
copy report + mar89.rpt + apr89.rpt + may89.rpt
```
현재 디렉터리에 명명 된 단일 파일 Combined.doc에 the.txt 파일 이름 확장명을 가진 모든 파일을 결합 하려면 다음을 입력 합니다.
```
copy *.txt Combined.doc 
```
포함, 와일드 카드 문자를 사용 하 여 파일 하나에 여러 개의 이진 파일을 결합 하려는 경우 **/b**합니다. 이렇게 하면 Windows에서를 CTRL + Z를 파일의 끝 문자로 취급지 않습니다. 예를 들어 입력 합니다.
```
copy /b *.exe Combined.exe
```

> [!CAUTION]
> 이진 파일을 결합 하는 경우 결과 파일 내부 형식으로 인해 사용할 수 있습니다.

다음 예에서 **복사** 각 파일을 해당.ref 인 파일 확장명이.txt 인 결합 합니다. 결과 동일한 파일 이름은 같지만 확장명이.doc 파일. **복사** File1.ref와 File1.txt File1.doc, 폼에 결합 한 다음 **복사** File2.txt File2.ref File2.doc, 폼에 함께 결합 합니다. 예를 들어 입력 합니다.
```
copy *.txt + *.ref *.doc
```
모든 파일 확장명이.txt 인 결합 한 다음 모든 파일 확장명이.ref 인 Combined.doc 라는 하나의 파일로,를 입력 합니다.
```
copy *.txt + *.ref Combined.doc
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)