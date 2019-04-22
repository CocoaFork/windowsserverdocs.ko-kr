---
title: 집합 id
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5793d7ad-827e-4285-b2c6-ae60eeb0e886
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f95490850acd263fb0b34007ac64a84c9a374865
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822054"
---
# <a name="set-id"></a>집합 id

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ID를 설정 하는 Diskpart 명령이 포커스가 있는 파티션에 대 한 파티션 형식 필드를 변경합니다.  
  
> [!IMPORTANT]  
> 이 명령을 사용 하기 위한 original equipment manufacturer \(Oem\) 만 합니다. 이 매개 변수를 사용 하는 파티션 형식 필드를 변경 하면 컴퓨터가 실패 하거나 부팅 수 없는 경우가 발생할 수 있습니다. 를 하는 OEM 하거나 gpt 디스크를 사용 하 여 발생 하지 않으면이 매개 변수를 사용 하 여 gpt 디스크의 파티션 형식 필드를 변경 하지 않아야 합니다. 대신 항상을 [efi 파티션을 만들](create-partition-efi.md) EFI 시스템 파티션에 만드는 명령을 합니다 [파티션 msr 만드는](create-partition-msr.md) Microsoft 예약 파티션을 만드는 명령 및 [만들기 기본 파티션](create-partition-primary.md) gpt 디스크에 주 파티션을 만들 ID 매개 변수 없이 명령을 합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
set id={ <byte> | <GUID> } [override] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|<byte>|마스터 부트 레코드에 대 한 \(MBR\) 디스크, 파티션에 대 한 16 진수 형식으로 type 필드에 대 한 새 값을 지정 합니다. 모든 파티션 형식 바이트 LDM 파티션을 지정 하는 형식 0x42 제외 하 고이 매개 변수를 지정할 수 있습니다. 16 진수 파티션 유형을 지정 하는 경우 선행 0x를 생략 하면 note 합니다.|  
|<GUID>|GUID 파티션 테이블에 대 한 \(gpt\) 디스크, 파티션에 대 한 유형 필드에 대 한 새 GUID 값을 지정 합니다. 인식 된 Guid는 다음과 같습니다.<br /><br />-EFI 시스템 파티션을: c12a7328\-f81f\-11 d 2\-ba4b\-00a0c93ec93b<br />-기본 데이터 파티션을: ebd0a0a2\-b9e5\-4433\-87 c 0\-68b6b72699c7<br /><br />이 매개 변수는 다음을 제외한 모든 파티션 유형 GUID를 지정할 수 있습니다.<br /><br />-Microsoft Reserved 파티션: e3c9e316\-0b5c\-4db8\-817 d\-f92df00215ae<br />-LDM 메타 데이터 파티션에 동적 디스크: 5808c8aa\-7e8f\-42e0\-85 d 2\-e1e90434cfb3<br />동적 디스크에 데이터 파티션을 LDM: af9b60a0\-1431\-4f62\-bc68\-3311714a69ad<br />-메타 데이터 파티션을 클러스터: db97dba9\-0840\-4bae\-97f0\-ffb9a327c7e1|  
|재정|파일 시스템에 볼륨을 파티션 유형을 변경 하기 전에 분리 되도록 합니다. 실행 하는 경우는 **집합 id** 명령, DiskPart 잠금 및 파일 시스템에서 볼륨을 분리 하려고 합니다. 경우 **재정의** 지정 되지 않은 파일 시스템 잠금에 대 한 호출에 실패 하 고 \(예를 들어 열린 핸들 이므로\), 작업이 실패 합니다. 때 **재정의** 지정, 파일 시스템 잠금에 대 한 호출에 실패 하는 볼륨에 모든 열린 핸들이 무효화 됩니다 하는 경우에 DiskPart 분리를 수행 합니다.<br /><br />이 명령은 Windows 7 및 Windows Server 2008 r 2에만 있습니다.|  
|noerr|스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   DiskPart은 앞에서 언급 한 제한 사항 이외의 지정 하는 값의 유효성을 확인 하지 않습니다 \(를 16 진수 형식 또는 GUID 바이트 인지를 확인 하는 제외 하 고\)합니다.  
  
-   이 명령은 Microsoft 예약 파티션 또는 동적 디스크에서 작동 하지 않습니다.  
  
## <a name="BKMK_examples"></a>예제  
0x07에 유형 필드를 설정 하 고 분리 하 고 파일 시스템을 하려면 다음을 입력 합니다.  
  
```  
set id=0x07 override  
```  
  
기본 데이터 파티션이 되도록 유형 필드를 설정 하려면 다음을 입력 합니다.  
  
```  
set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

