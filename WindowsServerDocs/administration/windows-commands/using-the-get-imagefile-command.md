---
title: Get 이미지 파일 명령을 사용 하 여
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c8136585e04caca02ab16c7b4ca11a825cf400d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392138"
---
# <a name="using-the-get-imagefile-command"></a>Get 이미지 파일 명령을 사용 하 여



Windows 이미지 (.wim) 파일에 포함 된 이미지에 대 한 정보를 검색 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/Sos: \<WIM file path >|.Wim 파일의 전체 경로 파일 이름을 지정합니다.|
|[/ 자세한]|각 이미지에서 모든 이미지 메타 데이터를 반환합니다. 이 옵션을 사용 하지 않는 경우 기본 동작은 반환할 이미지 이름, 설명 및 파일 이름입니다.|

## <a name="BKMK_examples"></a>예와

이미지에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-ImageFile /ImageFile:"C:\temp\install.wim"
```
자세한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:"\\Server\Share\My Folder \install.wim" /Detailed
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)