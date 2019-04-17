---
title: "MBR(마스터 부트 레코드)을 GPT(GUID 파티션 테이블) 디스크로 변경"
description: "MBR(마스터 부트 레코드)을 GPT(GUID 파티션 테이블) 디스크로 변경하는 방법을 설명합니다."
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f28d151d3b1d6b19b9ca330c5ff8576a53acbfa5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-master-boot-record-mbr-disk-into-a-guid-partition-table-gpt-disk"></a>MBR(마스터 부트 레코드) 디스크를 GPT(GUID 파티션 테이블) 디스크로 변경

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

MBR(마스터 부트 레코드) 디스크는 표준 BIOS 파티션 테이블을 사용합니다. GPT(GUID 파티션 테이블) 디스크는 UEFI(Unified Extensible Firmware Interface)를 사용합니다. GPT 디스크의 한 가지 장점은 각 디스크에 4개 이상의 파티션을 보유할 수 있다는 점입니다. 2TB(테라바이트)보다 큰 디스크에 대해서는 GPT가 필요합니다.

디스크에 어떠한 파티션 또는 볼륨도 포함되어 있지 않는 한 디스크를 MBR에서 GPT 파티션 스타일로 변경할 수 있습니다.
이동식 미디어, 또는 클러스터 서비스에서 사용하는 공유 SCSI 또는 파이버 채널 버스에 연결된 클러스터 디스크에서 GPT 파티션 스타일을 사용할 수 없습니다.

> [!NOTE]
> 디스크를 변환하기 전에 디스크에서 실행 중인 모든 프로그램을 종료합니다.

## <a name="changing-an-mbr-disk-into-a-gpt-disk"></a>MBR 디스크를 GPT 디스크로 변경

-   [Windows 인터페이스 사용](#BKMK_WINUI)
-   [명령줄 사용](#BKMK_CMD)

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

<a id="BKMK_WINUI"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 MBR 디스크를 GPT 디스크로 변경

1.  GPT 디스크로 변환하고자 하는 기본 MBR 디스크의 모든 데이터를 백업 또는 이동합니다.

2.  디스크에 파티션 또는 볼륨이 포함된 경우 각각을 마우스 오른쪽 단추로 클릭한 다음 **파티션 삭제** 또는 **볼륨 삭제**를 클릭합니다.

3.  GPT 디스크로 변경하고자 하는 MBR 디스크를 마우스 오른쪽 단추로 클릭한 다음 **GPT 디스크로 변환**을 클릭합니다.

<a id="BKMK_CMD"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-a-command-line"></a>명령줄을 사용하여 MBR 디스크를 GPT 디스크로 변경

1.  GPT 디스크로 변환하고자 하는 기본 MBR 디스크의 모든 데이터를 백업 또는 이동합니다.

2.  **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택하여 관리자 권한 명령 프롬프트를 엽니다.

3. `diskpart`를 입력합니다. 디스크에 파티션이나 볼륨이 없는 경우 6단계까지 건너뜁니다.

4.  **DISKPART** 프롬프트에서 `list disk`를 입력합니다. 변환하고자 하는 디스크 번호를 메모합니다.

5.  **DISKPART** 프롬프트에서 `select disk <disknumber>`를 입력합니다.

6.  **DISKPART** 프롬프트에서 `clean`을 입력합니다.

> [!NOTE]
> **clean** 명령을 실행하면 디스크의 모든 파티션 또는 볼륨이 삭제됩니다.

7.  **DISKPART** 프롬프트에서 `convert gpt`를 입력합니다.

<br />

| 값  | 설명  |
| ----- | ----|
| <p>**list disk**</p> | <p>디스크의 목록과 크기, 사용 가능한 공간 크기, 기본 또는 동적 디스크 여부, 디스크의 MBR(마스터 부트 레코드) 또는 GPT(GUID 파티션 테이블) 파티션 스타일 사용 여부 등 정보를 표시합니다. 별표(*)가 표시된 디스크는 포커스가 설정됩니다.</p> |
| <p>**select disk** <em>disknumber</em></p> | <p>디스크 번호가 <em>disknumber</em>인 지정된 디스크를 선택하고 포커스를 설정합니다.</p> |
| <p>**clean**</p> | <p>포커스가 설정된 디스크에서 모든 파티션 또는 볼륨을 삭제합니다.</p>  |
| <p>**convert gpt**</p>| <p>MBR(마스터 부트 레코드) 파티션 스타일의 비어 있는 기본 디스크를 GPT(GUID 파티션 테이블) 파티션 스타일의 기본 디스크로 변환합니다.</p> |

## <a name="see-also"></a>참고 항목

-   [명령줄 구문 표기법](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


