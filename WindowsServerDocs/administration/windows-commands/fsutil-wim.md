---
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
title: Fsutil wim
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: fc79b70e8dedb9ecad5e8c6e89f51ece3279faa4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376663"
---
# <a name="fsutil-wim"></a>Fsutil wim
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

WIM (Windows 이미지) 지원 파일을 검색 하 고 관리 하는 함수를 제공 합니다.

## <a name="syntax"></a>구문

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|enumfiles|WIM 지원 파일을 열거 합니다.|
|\<drive name >|드라이브 이름을 지정 합니다.|
|\<data 원본 >|데이터 원본을 지정 합니다.|
|enumwims|지원 WIM 파일을 열거 합니다.|
|queryfile|파일이 WIM에 의해 지원 되는 경우 쿼리 하 고, 그럴 경우 WIM 파일에 대 한 세부 정보를 표시 합니다.|
|\< 파일 이름 >|파일 이름을 지정 합니다.|
|removewim|지원 파일에서 WIM을 제거 합니다.|




### <a name="examples"></a>예

C 드라이브의 파일을 열거 하려면 데이터 원본 0에서 다음을 입력 합니다.

```
fsutil wim enumfiles C: 0
```

드라이브 C:에 대 한 지원 WIM 파일을 열거 하려면 다음을 입력 합니다.

```
fsutil wim enumwims C:
```

파일이 WIM에 의해 지원 되는지 확인 하려면 다음을 입력 합니다.

```
fsutil wim C:\Windows\Notepad.exe
```

볼륨 C: 및 데이터 원본 2에 대 한 지원 파일에서 WIM을 제거 하려면 다음을 입력 합니다.

```
fsutil wim removewims C: 2
```

### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)