---
title: bitsadmin 피어 캐싱 및 setconfigurationflags
description: Windows 명령 항목에 대 한 **bitsadmin 피어 캐싱 및 setconfigurationflags** -컴퓨터 동료에 게 콘텐츠를 사용할 수 및 피어에서 콘텐츠를 다운로드 하는 경우를 결정 하는 구성 플래그를 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22408d4aab7f5ea374511bc16751d911a84644f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813334"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin 피어 캐싱 및 setconfigurationflags



컴퓨터 피어 컴퓨터에 콘텐츠를 사용할 수 및 피어에서 콘텐츠를 다운로드 하는 경우 결정 하는 구성 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|값|값이 이진 표현에서 비트에 대 한 다음 해석 가진 부호 없는 정수:</br>-피어 로부터 다운로드 작업의 데이터를 허용 합니다. 최하위 비트를 설정 합니다.</br>-작업의 데이터를 동료에 게 제공 허용: 오른쪽에서 두 번째 비트를 설정 합니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 피어 로부터 다운로드 작업의 데이터를 지정 *myJob*합니다.
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)