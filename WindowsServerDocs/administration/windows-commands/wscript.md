---
title: wscript
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fbaf193-cdbd-414c-84c9-bb5720f84c29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: 771c1231ee5379ec797f535505839de8671e32a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821304"
---
# <a name="wscript"></a>wscript



Windows 스크립트 호스트에는 사용자는 다양 한 작업을 수행 하는 다양 한 개체 모델을 사용 하는 언어 스크립트를 실행할 수 있습니다 하는 환경을 제공 합니다.

## <a name="syntax"></a>구문

```
wscript [<scriptname>] [/b] [/d] [/e:<engine>] [{/h:cscript|/h:wscript}] [/i] [/job:<identifier>] [{/logo|/nologo}] [/s] [/t:<number>] [/x] [/?] [<ScriptArguments>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|scriptname|스크립트 파일의 경로 파일 이름을 지정합니다.|
|/b|경고, 스크립팅 오류 또는 입력된 프롬프트를 표시 하지 않는 일괄 처리 모드를 지정 합니다. 이것은의 반대 **/i**합니다.|
|/d|디버거를 시작 합니다.|
|/e|스크립트를 실행 하는 데 사용 되는 엔진을 지정 합니다. 이 사용자 지정 파일 이름 확장명을 사용 하는 스크립트를 실행할 수 있습니다. /E 매개 변수 없이 등록 된 파일 이름 확장명을 사용 하는 스크립트 에서만 실행할 수 있습니다. 예를 들어,이 명령을 실행 하려는 경우:<br>```cscript test.admin```<br>이 오류 메시지가 표시 됩니다. 입력된 오류: 파일 확장명에 대 한 스크립트 엔진이 ". 관리자"<br>비표준 파일 이름 확장명을 사용 하 여의 장점은 실수로 스크립트를 두 번 클릭 으로부터 보호 하는 것을 코드를 실행 실제로 보내지 않으려는 실행 됩니다. <br>.Admin 파일 이름 확장명 및 VBScript 간에 영구 연결을 만들지 않습니다. .Admin 파일 이름 확장명을 사용 하는 스크립트를 실행할 때마다 /e 매개 변수를 사용 해야 합니다.|
|/h:cscript|등록 **cscript.exe** 스크립트를 실행 하기 위한 기본 스크립트 호스트입니다.|
|/h:wscript|등록 **wscript.exe** 스크립트를 실행 하기 위한 기본 스크립트 호스트입니다. 이것이 기본 때 합니다 **/h** 옵션을 생략 하면 됩니다.|
|/i|경고, 스크립팅 오류 및 입력된 프롬프트를 표시 하는 대화형 모드를 지정 합니다.</br>이 고 기본값의 반대 **/b**합니다.|
|/job:\<identifier>|로 식별 되는 작업을 실행 *식별자* 에 **.wsf** 스크립트 파일입니다.|
|/logo|스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너 콘솔에 표시 되도록 지정 합니다.</br>이 고 기본값의 반대 **/nologo**합니다.|
|/nologo|스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너가 표시 되지 않도록 지정 합니다. 이것은의 반대 **/logo**합니다.|
|/s|현재 사용자에 대 한 현재 명령 프롬프트 옵션을 저장합니다.|
|/t:\<number>|스크립트를 초 단위로 실행할 수 있는 최대 시간을 지정 합니다. 최대 32, 767 초를 지정할 수 있습니다.</br>기본값은 시간 제한이 없습니다.|
|/x|스크립트 디버거를 시작 합니다.|
|ScriptArguments|스크립트에 전달 되는 인수를 지정 합니다. 각 스크립트 인수 앞에 슬래시 (/) 해야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   이 작업을 수행할 때는 관리 자격 증명이 필요하지 않습니다. 보안을 위해 관리 자격 증명이 없는 사용자로 이 작업을 수행하는 것이 좋습니다.
-   명령 프롬프트를 열려면 **시작** 화면에서 **cmd**를 입력한 다음 **명령 프롬프트**를 클릭합니다.
-   각 매개 변수는 선택 사항입니다. 그러나 스크립트를 지정 하지 않고 스크립트 인수를 지정할 수 없습니다. 스크립트 또는 스크립트 인수를 지정 하지 않으면 **wscript.exe** 표시는 **Windows 스크립트 호스트 설정** 전역 속성을 설정할 스크립팅 모든 사용할 수 있는 대화 상자는 스크립트를 **wscript.exe** 로컬 컴퓨터에서 실행 합니다.
-   **/t** 매개 변수는 타이머를 설정 하 여 스크립트의 과도 한 실행을 방지 합니다. 시간이 지정된 된 값을 초과할 경우 **wscript** 스크립트 엔진이 작동을 중단 하 고 프로세스를 종료 합니다.
-   Windows 스크립트 파일 일반적으로 다음 파일 이름 확장명 중 하나는: **.wsf**, **.vbs**, **.js**합니다.
-   연결 되지 않은 확장명을 가진 스크립트 파일을 두 번 클릭 하면는 **Open With** 대화 상자가 나타납니다. 선택 **wscript** 또는 **cscript**, 를 선택한 다음 **항상이 프로그램을 사용 하 여이 파일 형식을 열**합니다. 이 등록 **wscript.exe** 하거나 **cscript.exe** 이 파일 형식의 파일에 대 한 기본 스크립트 호스트입니다.
-   개별 스크립트에 대 한 속성을 설정할 수 있습니다. 참조 [Windows 스크립트 호스트 개요](https://technet.microsoft.com/library/cc738350(v=ws.10).aspx) 에 대 한 자세한 내용은 합니다.
-   Windows 스크립트 호스트를 사용 하 여 수 **.wsf** 스크립트 파일입니다. 각 **.wsf** 파일 여러 스크립팅 엔진을 사용할 수 있으며 여러 작업을 수행 합니다.

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
