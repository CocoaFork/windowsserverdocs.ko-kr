---
title: auditpol 지우기
description: Windows 명령 항목- **auditpol 지우기** -모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하 고, 모든 하위 범주에 대 한 시스템 감사 정책을 다시 설정 (해제) 하며 모든 감사 옵션을 사용 안 함으로 설정 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4fd2cce2b860ee41725b698dcd36ca38b2c4c6a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382422"
---
# <a name="auditpol-clear"></a>auditpol 지우기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하 고 모든 하위 범주에 대 한 시스템 감사 정책을 다시 설정 (해제) 하며 모든 감사 옵션을 사용 안 함으로 설정 합니다.

## <a name="syntax"></a>구문
```
auditpol /clear [/y]
```
## <a name="parameters"></a>매개 변수

| 매개 변수 |                                   설명                                    |
|-----------|----------------------------------------------------------------------------------|
|    /y     | 모든 감사 정책 설정을 지워야 하는 경우를 확인 하는 메시지를 표시 하지 않습니다. |
|    /?     |                       명령 프롬프트에 도움말을 표시합니다.                       |

## <a name="remarks"></a>설명
사용자 정책 및 시스템 정책에 대 한 일반 작업의 경우 보안 설명자에 설정 된 해당 개체에 대 한 쓰기 또는 모든 권한이 있어야 합니다. 처리 하는 개체로 지우기 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한을 지우기 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.
## <a name="BKMK_examples"></a>예와
모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하려면 모든 (해제) 시스템 감사 정책 하위 범주를 다시 설정 하 고 모든 감사 정책 설정을 확인 메시지 형식에서 사용 안 함으로 설정 합니다.
```
auditpol /clear
```
모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하려면 모든 하위 범주에 대 한 시스템 감사 정책 설정을 다시 설정 하 고 모든 감사 정책 설정 유형 확인 메시지 없이 사용 안 함으로 설정:
```
auditpol /clear /y
```
> [!NOTE]
> 앞의 예제는이 작업을 수행 하는 스크립트를 사용 하는 경우에 유용 합니다.
> #### <a name="additional-references"></a>추가 참조
> [명령줄 구문 키](command-line-syntax-key.md)
