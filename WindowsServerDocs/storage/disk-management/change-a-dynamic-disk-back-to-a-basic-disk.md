---
title: 동적 디스크를 기본 디스크로 다시 변경
description: 동적 디스크를 기본 디스크로 다시 변환하는 방법을 설명합니다.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 249db6d2779e696ef93fecfd11718dbcce8654be
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812471"
---
# <a name="change-a-dynamic-disk-back-to-a-basic-disk"></a>동적 디스크를 기본 디스크로 다시 변경

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 동적 디스크의 모든 항목을 삭제한 다음, 기본 디스크로 변환하는 방법을 설명합니다. Windows에서는 동적 디스크 사용이 중단되었으며 더 이상 권장하지 않습니다. 대신, 디스크를 더 큰 볼륨으로 함께 풀링할 때 기본 디스크를 사용하거나 최신 [스토리지 공간](https://support.microsoft.com/help/12438/windows-10-storage-spaces) 기술을 사용하는 것이 좋습니다. Windows가 부팅되는 볼륨을 미러링하려는 경우 다수의 마더보드에 포함된 것과 같은 하드웨어 RAID 컨트롤러를 사용할 수 있습니다.

> [!WARNING]
> 동적 디스크를 기본 디스크로 변환하려면 디스크의 모든 볼륨을 삭제하여 디스크의 모든 데이터를 영구적으로 삭제해야 합니다. 진행하기 전에 보관하려는 모든 데이터를 백업해야 합니다.

## <a name="changing-a-dynamic-disk-back-to-a-basic-disk"></a>동적 디스크를 기본 디스크로 다시 변경

-   [Windows 인터페이스 사용](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface)
-   [명령줄 사용](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line)

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 동적 디스크를 기본 디스크로 변경

1.  동적에서 기본으로 변환하려는 디스크의 모든 볼륨을 백업합니다.

2.  디스크 관리에서 기본 디스크로 변환하려는 동적 디스크에서 각 볼륨을 마우스 오른쪽 단추로 클릭한 다음, 디스크의 각 볼륨에 대하여 **볼륨 삭제**를 클릭합니다.

3.  디스크의 모든 볼륨이 삭제되었을 경우 디스크를 마우스 오른쪽 단추로 클릭한 다음, **기본 디스크로 변환**을 클릭합니다.

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line"></a>명령줄을 사용하여 동적 디스크를 기본 디스크로 변경

1.  동적에서 기본으로 변환하려는 디스크의 모든 볼륨을 백업합니다.

2.  명령 프롬프트를 열고 `diskpart`를 입력합니다.

3.  **DISKPART** 프롬프트에서 `list disk`을(를) 입력합니다. 기본 디스크로 변환하려는 디스크 번호를 기록해 둡니다.

4.  **DISKPART** 프롬프트에서 `select disk <disknumber>`을(를) 입력합니다.

5.  **DISKPART** 프롬프트에서 `detail disk <disknumber>`을(를) 입력합니다.

6.  **DISKPART** 프롬프트에서 디스크의 각 볼륨에 대하여 `select volume= <volumenumber>`을(를) 입력한 다음, `delete volume`을(를) 입력합니다.

7.  **DISKPART** 프롬프트에서 `select disk <disknumber>`을(를) 입력하여 기본 디스크로 변환하려는 디스크의 디스크 번호를 지정합니다.

8.  **DISKPART** 프롬프트에서 `convert basic`을(를) 입력합니다.


| 값  | 설명 |
| --- | --- |
| **list disk**                         | 디스크의 목록과 크기, 사용 가능한 공간 크기, 기본 또는 동적 디스크 여부, 디스크의 MBR(마스터 부트 레코드) 또는 GPT(GUID 파티션 테이블) 파티션 스타일 사용 여부 등 정보를 표시합니다. 별표(*)가 표시된 디스크는 포커스가 설정됩니다. |
| **select disk** <em>disknumber</em>   | 디스크 번호가 <em>disknumber</em>인 지정된 디스크를 선택하고 포커스를 설정합니다.  |
| **detail disk** <em>disknumber</em>   | 해당 디스크에 선택된 된 디스크와 볼륨의 속성을 표시합니다.  |
| **select volume** <em>disknumber</em> | 볼륨 번호가 <em>disknumber</em>인 지정된 볼륨을 선택하고 포커스를 설정합니다. 지정된 볼륨이 없는 경우 **select** 명령이 포커스가 설정된 현재 볼륨 목록을 표시합니다. 번호, 드라이브 문자 또는 탑재 지점 경로로 볼륨을 지정할 수 있습니다. 기본 디스크에서 볼륨을 선택하면 해당 파티션에도 포커스를 설정합니다. |
| **delete volume**                     | 선택한 볼륨을 삭제 합니다. 시스템 볼륨, 부팅 볼륨 또는 활성 페이징 파일이나 크래시 덤프(메모리 덤프)가 포함된 볼륨을 삭제할 수 없습니다. |
| **convert basic** | 빈 동적 디스크를 기본 디스크로 변환합니다.  |

## <a name="additional-considerations"></a>추가 고려 사항

-   디스크를 기본 디스크로 변경하기 전에 디스크에 어떤 볼륨이나 데이터가 있어서는 안 됩니다. 데이터를 보관하려는 경우 디스크를 기본 디스크로 변환하기 전에 데이터를 백업하거나 다른 볼륨으로 이동합니다.
-   동적 디스크를 기본 디스크로 변경하고 나면 디스크에 파티션 및 논리 드라이브만 만들 수 있습니다.

## <a name="see-also"></a>참고 항목

-   [명령줄 구문 표기법](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)