---
title: gpt
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cba9839f98dfd5a72289838273a057dd0e09a7e5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438184"
---
# <a name="gpt"></a>gpt

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 GUID 파티션 테이블 (gpt) 디스크에 포커스가 있는 파티션에 gpt 특성을 할당합니다.  gpt 파티션 특성 파티션의 사용에 대 한 추가 정보를 제공합니다. 일부 특성은 GUID 파티션 형식에 따라 다릅니다.

> [!CAUTION]
> Gpt 특성을 변경 하면 기본 데이터 볼륨 드라이브 문자를 할당 하거나 파일 시스템 탑재에서 않으려면 실패 발생할 수 있습니다. 원래 장비 제조업체 (OEM) 또는 gpt 디스크와 숙련 된 IT 전문가가 아니라면 gpt 특성을 변경 하지 않아야 합니다.
> ## <a name="syntax"></a>구문
> ```
> gpt attributes=<n>
> ```
> ## <a name="parameters"></a>매개 변수
> 
> |   매개 변수    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
> |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | attributes=<n> | 포커스가 있는 파티션을에 적용할 특성에 대 한 값을 지정 합니다. Gpt 특성 필드에는 두 개의 하위 필드를 포함 하는 64 비트 필드가입니다. 하위 필드는 모든 파티션 Id에 공통적으로 적용 하는 동안 파티션 ID의 경우에만 더 높은 필드 해석 됩니다. 사용 가능한 값은 다음과 같습니다.<br /><br />-   **0x0000000000000001**. 파티션을 제대로 작동 하려면 컴퓨터에 필요 함을 지정 합니다.<br />-   **0x8000000000000000**. 파티션을 받지 드라이브 문자를 기본적으로 디스크 디스크는 컴퓨터에 처음으로 표시 하는 경우 또는 다른 컴퓨터로 이동 하는 경우 지정 합니다.<br />-   **0x4000000000000000**. 파티션의 볼륨을 숨깁니다. 즉, 파티션은 탑재 관리자에서 검색 되지 않습니다.<br />-   **0x2000000000000000**. 파티션을 다른 파티션이의 섀도 복사본 임을 지정 합니다.<br />-   **0x1000000000000000**. 파티션을 읽기 전용으로 지정 합니다. 이 특성을 쓰지 볼륨을 방지 합니다.<br /><b />이러한 특성에 대 한 자세한 내용은 있는 특성 섹션을 참조 하세요 [create_PARTITION_PARAMETERS 구조](https://go.microsoft.com/fwlink/?LinkId=203812) (<https://go.microsoft.com/fwlink/?LinkId=203812>). |
> 
> ## <a name="remarks"></a>설명
> - EFI 시스템 파티션에 운영 체제를 시작 하는 데 필요한 바이너리만 포함 되어 있습니다. 따라서 쉽게 OEM 바이너리 또는 이진 파일에 대 한 다른 파티션에 위치 하는 운영 체제입니다.
> - 이 작업을 수행 하려면 기본 gpt 파티션 선택 해야 합니다. 사용 된 **파티션을 선택** 기본 gpt 파티션 선택 및 포커스를 이동 하는 명령입니다.
>   ## <a name="BKMK_examples"></a>예제
>   gpt 디스크를 새 컴퓨터로 이동 하는 해당 컴퓨터에서 자동으로 포커스를 형식 인 파티션의 드라이브 문자를 할당 하지 못하게 하려는 경우:
>   ```
>   gpt attributes=0x8000000000000000
>   ```
