---
title: auditpol get
description: Windows 명령 항목에 대 한 **auditpol get** -시스템 정책, 사용자별 정책, 감사 옵션 및 감사 보안 설명자 개체를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe13de4e-836c-4207-b47c-64b6272d6c41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03ba59b19af42ab2d3fdd1dd52d976d381779640
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435138"
---
# <a name="auditpol-get"></a>auditpol get

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템 정책, 사용자별 정책, 감사 옵션 및 감사 보안 설명자 개체를 검색 합니다.

## <a name="syntax"></a>구문
```
auditpol /get 
[/user[:<username>|<{sid}>]]
[/category:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/subcategory:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/option:<option name>]
[/sd]
[/r]
```
## <a name="parameters"></a>매개 변수

|  매개 변수   |                                                                                                                                         설명                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /user     | 사용자 단위 감사 정책을 쿼리할 때 사용자에 대 한 보안 주체를 표시 합니다. /Category 또는 /subcategory 매개 변수를 지정 합니다. 사용자는 SID (보안 식별자) 또는 이름으로 지정할 수 있습니다. 사용자 계정을 지정 하지 않으면, 시스템 감사 정책 쿼리 됩니다. |
|  /category   |                                                          전역 고유 식별자 (GUID) 또는 이름으로 지정 된 하나 이상의 감사 범주입니다. 별표 (\*) 모든 감사 범주를 쿼리할 수를 나타내는 데 사용할 수 있습니다.                                                          |
| /subcategory |                                                                                                                  하나 이상의 감사 하위 범주 GUID 또는 이름을 지정 합니다.                                                                                                                  |
|     /sd      |                                                                                                        감사 정책에 대 한 액세스 권한을 위임 하는 데 사용 되는 보안 설명자를 검색 합니다.                                                                                                        |
|   /option    |                                                                              CrashOnAuditFail, 트래버스, AuditBaseObjects, 또는 AuditBasedirectories 옵션에 대 한 기존 정책을 검색합니다.                                                                               |
|      /r      |                                                                                                              보고서 형식으로 쉼표로 구분 된 값 (CSV) 출력을 표시합니다.                                                                                                              |
|      /?      |                                                                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                                                                             |

## <a name="remarks"></a>설명
모든 범주 및 하위 GUID 또는 따옴표로 묶인 이름으로 지정할 수 있습니다. 사용자는 SID 또는 이름으로 지정할 수 있습니다.
사용자별 정책 및 시스템 정책에 대 한 모든 get 연산에 대 한 보안 설명자에 설정 된 해당 개체에 대 한 권한이 읽기 있어야 합니다. 처리 하는 개체로 get 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한은 가져오기 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.
## <a name="BKMK_examples"></a>예제
### <a name="examples-for-the-per-user-audit-policy"></a>사용자 단위 감사 정책에 대 한 예제
추적 세부 게스트 계정에 대 한 사용자 단위 감사 정책을 검색 하 고 시스템에 대 한 출력을 표시 하 고 개체 액세스 범주를 입력 합니다.
```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:"System","detailed Tracking","Object Access"
```
> [!NOTE]
> 이 명령은 두 가지 경우에 유용합니다. 의심 스러운 활동에 대 한 특정 사용자 계정을 모니터링 하는 경우 추가 감사를 사용 하도록 포함 정책을 사용 하 여 특정 범주에서 결과 검색 하려면 /get 명령을 사용할 수 있습니다. 또는 계정에 대 한 감사 설정을 불필요 한 이벤트 하지만 다양 한 로깅 하는 경우 제외 정책 사용 하 여 해당 계정에 대 한 불필요 한 이벤트를 필터링 하려면 /get 명령을 사용할 수 있습니다. 목록이 모든 범주에 대 한 auditpol /list /category 명령을 사용 합니다.
> 사용자 단위 감사 정책 범주 및 게스트 계정에 대 한 시스템 범주 아래의 해당 하위 범주에 대 한 포괄 및 전용 설정을 보고, 특정 하위 범주에 대 한 검색 하려면 다음을 입력 합니다.
> ```
> auditpol /get /user:guest /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> 보고서 형식으로 출력을 표시 하 고를 컴퓨터 이름, 정책 대상, 하위 범주, 하위 범주 GUID, 설정 포함 및 제외 설정 포함 하려면 다음을 입력 합니다.
> ```
> auditpol /get /user:guest /category:detailed Tracking" /r
> ```
> ### <a name="examples-for-the-system-audit-policy"></a>시스템 감사 정책에 대 한 예제
> 시스템에 대 한 정책 검색 하려면 범주 및 하위 범주를 범주와 하위 정책 설정을 시스템 감사 정책에 대 한 보고서를 입력 합니다.
> ```
> auditpol /get /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> 자세한 추적 범주 및 하위 보고서 형식에서에 대 한 정책 검색 및 컴퓨터 이름, 정책 대상, 하위 범주, 하위 범주 GUID, 설정 포함 및 제외 설정 형식 포함:
> ```
> auditpol /get /category:"detailed Tracking" /r
> ```
> 범주와 함께 두 범주에 대 한 정책을 검색할 지정 된 모든 하위 범주의 모든 감사 정책 설정을 보고 하는 Guid로 두 가지 범주, 유형:
> ```
> auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> ### <a name="examples-for-auditing-options"></a>감사 옵션에 대 한 예제
> 사용 하도록 설정 또는 해제, AuditBaseObjects 옵션 중 하나는 상태를 검색 하려면 다음을 입력 합니다.
> ```
> auditpol /get /option:AuditBaseObjects
> ```
> [!NOTE]
> 사용 가능한 옵션은 AuditBaseObjects, AuditBaseOperations, 및 트래버스 됩니다.
> 사용 상태를 검색 하려면 사용 안 함, 또는 2-crashonauditfail 옵션 2 입력 합니다.
> ```
> auditpol /get /option:CrashOnAuditFail /r
> ```
> #### <a name="additional-references"></a>추가 참조
> [명령줄 구문 키](command-line-syntax-key.md)
