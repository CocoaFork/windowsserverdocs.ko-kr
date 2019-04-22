---
title: auditpol 제거
description: Windows 명령 항목에 대 한 **auditpol 제거** -지정된 된 계정 또는 모든 계정에 대 한 사용자 단위 감사 정책을 제거 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be42ec55-235c-44f7-9abd-ed1cf3f5b1f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 566827e93d9f8c9dc0d00f4f704513369fbb44ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818304"
---
# <a name="auditpol-remove"></a>auditpol 제거

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 계정 또는 모든 계정에 대 한 사용자 단위 감사 정책을 제거합니다.

## <a name="syntax"></a>구문
```
auditpol /remove [/user[:<username>|<{SID}>]]
[/allusers]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/user|보안 식별자 (SID)를 지정 또는 사용자 단위 감사 정책에 사용자에 대 한 사용자 이름이 삭제 됩니다.|
|/allusers|모든 사용자에 대 한 사용자 단위 감사 정책을 제거합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
사용자별 정책에 대 한 제거 작업에 대 한 보안 설명자에 설정 된 해당 개체에 대 한 쓰기 또는 전체 제어 권한이 있어야 합니다. 처리 하는 개체로 제거 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한을 제거 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.
## <a name="BKMK_examples"></a>예제
사용자 단위 감사 정책을 사용자 mikedan에 대 한 이름으로를 제거 하려면 다음을 입력 합니다.
```
auditpol /remove /user:mikedan
```
사용자 mikedan sid에 대 한 사용자 단위 감사 정책을 제거 하려면 다음을 입력 합니다.
```
auditpol /remove /user:{S-1-5-21-397123471-12346959}
```
모든 사용자에 대 한 사용자 단위 감사 정책을 제거 하려면 다음을 입력 합니다.
```
auditpol /remove /allusers
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
