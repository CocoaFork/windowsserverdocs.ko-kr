---
title: bdehdcfg
description: '**Bdehdcfg** 에 대 한 Windows 명령 항목-BitLocker 드라이브 암호화 하는 데 필요한 파티션이 있는 하드 드라이브를 준비 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: acfe2582905402f7be149148520784be6ad47453
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382186"
---
# <a name="bdehdcfg"></a>bdehdcfg



BitLocker 드라이브 암호화에 필요한 파티션이 있는 하드 드라이브를 준비합니다. BitLocker 설치 프로그램은 필요에 따라 드라이브를 준비 하 고 다시 분할할 수 있는 기능을 포함 하므로 대부분의 Windows 7 설치는이 도구를 사용할 필요가 없습니다.

> [!WARNING]
> 알려진된와 충돌 하는 **BitLocker로 보호 되지 않는 고정된 드라이브에 대 한 쓰기 액세스 거부** 그룹 정책 설정에 있는 **컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\BitLocker Drive 고정 데이터 드라이브**합니다.</br>>이 정책 설정을 사용 하는 경우 컴퓨터에서 Bdehdcfg가 실행 되는 경우 다음과 같은 문제가 발생할 수 있습니다.</br>>-드라이브를 축소 하 고 시스템 드라이브를 만들면 드라이브 크기가 성공적으로 줄어들고 원시 파티션이 생성 됩니다. 그러나 원시 파티션에 포맷 되지 않습니다. 다음과 같은 오류 메시지가 표시 됩니다. "새 활성 드라이브를 포맷할 수 없습니다. 해야 수동으로 bitlocker가 드라이브를 준비 합니다. "</br>>-할당 되지 않은 공간을 사용 하 여 시스템 드라이브를 만드는 경우 원시 파티션이 생성 됩니다. 그러나 원시 파티션에 포맷 되지 않습니다. 다음과 같은 오류 메시지가 표시 됩니다. "새 활성 드라이브를 포맷할 수 없습니다. 해야 수동으로 bitlocker가 드라이브를 준비 합니다. "</br>>-기존 드라이브를 시스템 드라이브로 병합 하려고 하면이 도구는 시스템 드라이브를 만들기 위해 필요한 부팅 파일을 대상 드라이브에 복사 하지 못합니다. 다음과 같은 오류 메시지가 표시 됩니다. "BitLocker 설치 프로그램에서 부팅 파일을 복사 하지 못했습니다. 해야 수동으로 bitlocker가 드라이브를 준비 합니다. "</br>>이 정책 설정이 적용 되는 경우 드라이브가 보호 되므로 하드 드라이브를 다시 분할 수 없습니다. 이전 버전의 Windows에서 조직에서 컴퓨터를 업그레이드 하는 경우 해당 컴퓨터는 단일 파티션으로 구성 된 컴퓨터에 정책 설정을 적용 하기 전에 필요한 BitLocker 시스템 파티션을 만들어야 합니다.

이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Bdehdcfg: driveinfo](bdehdcfg-driveinfo.md)|지정 된 드라이브에서 드라이브 문자, 총 크기, 최대 여유 공간, 및 파티션의 파티션 특성을 표시 합니다. 유효한 파티션으로 나열 됩니다. 4 개의 주 또는 확장 된 파티션이 이미 존재 하는 경우에 할당 되지 않은 공간 나열 되지 않습니다.|
|[Bdehdcfg: 대상](bdehdcfg-target.md)|시스템 드라이브로 사용할 드라이브를의 부분을 정의 하 고 부분을 활성화 합니다.|
|[Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md)|시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다.|
|[Bdehdcfg: 크기](bdehdcfg-size.md)|새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 결정 합니다.|
|[Bdehdcfg: quiet](bdehdcfg-quiet.md)|모든 작업과 명령줄 인터페이스에서 오류를 표시 하지 않습니다 고 Bdehdcfg 모든 예에 "예" 대 한 답변을 사용 하 는/후속 동안 발생할 수 있는 프롬프트 없이 드라이브 준비 합니다.|
|[Bdehdcfg: 다시 시작](bdehdcfg-restart.md)|드라이브를 준비 하는 완료 된 후 다시 시작 하는 컴퓨터에 지시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_Examples"></a>예와

다음 예제에서는 500MB의 시스템 파티션을 만들려면 기본 드라이브에 사용 되는 Bdehdcfg를 보여 줍니다. 드라이브 문자 없이 지정 되어 있으므로 새 시스템 파티션에 드라이브 문자를 갖지 않습니다.
```
bdehdcfg -target default -size 500
```
다음 예제에서는 드라이브에 할당 되지 않은 공간이 부족 합니다. 300MB의 기본 크기의 시스템 파티션을 p (:)을 만들려면 기본 드라이브에 사용 되는 Bdehdcfg을 보여 줍니다. 이 도구는 더 이상 모든 입력에 대 한 사용자를 묻지 않습니다도 모든 오류를 표시 됩니다. 시스템 드라이브를 만든 후 컴퓨터 자동으로 다시 시작 됩니다.
```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)