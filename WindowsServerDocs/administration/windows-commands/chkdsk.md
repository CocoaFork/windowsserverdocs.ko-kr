---
title: chkdsk
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62912a3c-d2cc-4ef6-9679-43709a286035
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 26aad48db4a5f0a593dfcb29160031a0c9f3dc75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886864"
---
# <a name="chkdsk"></a>chkdsk



파일 시스템 및 논리적 및 물리적 오류에 대 한 볼륨의 파일 시스템 메타 데이터를 확인합니다. 매개 변수 없이 사용 하는 경우 **chkdsk** 볼륨의 상태에만 표시 하 고 오류를 수정 하지 않습니다. 사용 하는 경우는 **/f**, **/r**를 **/x**, 또는 **/b** 매개 변수를 수정 오류 볼륨.

> [!IMPORTANT]
> 로컬의 멤버 자격이 **관리자** 그룹 또는 그에 해당 하는 실행 하는 데 필요한 최소 **chkdsk**합니다. 관리자 권한으로 명령 프롬프트 창을 열려면 마우스 오른쪽 단추로 클릭 **명령 프롬프트** 시작 메뉴를 클릭 한 다음 **관리자 권한으로 실행**합니다.

> [!IMPORTANT]
> 중단 **chkdsk** 권장 되지 않습니다. 그러나 취소 하거나 중단 해도 **chkdsk** 그대로 안됩니다 볼륨 이전 보다 더 손상 **chkdsk** 를 실행 합니다. 다시 실행 **chkdsk** 확인 하 고 볼륨에 나머지 손상이 복구 합니다.

> [!IMPORTANT]
> **참고:** Chkdsk 로컬 디스크에 대해서만 사용할 수 있습니다. 이 명령은 네트워크를 통해 리디렉션된는 로컬 드라이브 문자를 사용 하 여 사용할 수 없습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

##<a name="syntax"></a>구문

```
chkdsk [<Volume>[[<Path>]<FileName>]] [/f] [/v] [/r] [/x] [/i] [/c] [/l[:<Size>]] [/b]  

```

##<a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<볼륨 >|(콜론) 드라이브 문자 지정 탑재 지점 또는 볼륨 이름입니다.|
|[\<Path>]<FileName>|사용 파일 할당 테이블 (FAT) 및 FAT32만 합니다. 위치와 파일 이름이 나 원하는 파일 집합 지정 **chkdsk** 검사할 합니다. 사용할 수는 **?** 및 **&#42;** 와일드 카드 문자를 여러 파일을 지정 합니다.|
|/f|디스크에서 오류를 해결합니다. 디스크를 잠가야 합니다. 경우 **chkdsk** 컴퓨터 다시 시작할 때마다 다음 드라이브를 확인 하려는 경우 요청 메시지 드라이브 표시 잠금 수 없습니다.|
|/v|디스크를 검사할 때 모든 디렉터리의 각 파일의 이름을 표시 합니다.|
|/r|불량 섹터를 찾아 읽을 수 있는 정보를 복구 합니다. 디스크를 잠가야 합니다. **/r** 의 기능을 포함 **/f**, 실제 디스크 오류 추가 분석 합니다.|
|/x|필요한 경우 볼륨을 먼저 분리 되도록 합니다. 드라이브에 열려 있는 모든 핸들이 무효화 됩니다. **/x** 의 기능을 포함 하는 또한 **/f**합니다.|
|/i|NTFS로 사용 합니다. 실행 하는 데 필요한 시간을 줄일 수 있도록 인덱스 항목 검사 **chkdsk**합니다.|
|/c|NTFS로 사용 합니다. 주기를 실행 하는 데 필요한 시간을 줄일 수는 폴더 구조 내에서 확인 하지 않습니다 **chkdsk**합니다.|
|/l[:\<Size>]|NTFS로 사용 합니다. 입력 한 크기를 로그 파일 크기를 변경 합니다. 크기 매개 변수를 생략 **/l** 현재 크기를 표시 합니다.|
|/b|NTFS에만 해당: 볼륨에 잘못 된 클러스터의 목록을 지우고 오류에 대 한 모든 할당 및 사용 가능한 클러스터를 다시 검사 합니다. **/ b** 의 기능을 포함 **/r**합니다. 새 하드 디스크 드라이브에 볼륨 이미징 후이 매개 변수를 사용 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

##<a name="remarks"></a>설명

-   건너뛸 볼륨 확인

    합니다 **/i** 또는 **/c** 스위치를 실행 하는 데 필요한 시간을 줄여 **chkdsk** 특정 볼륨 건너뛰어 확인 합니다.
-   다시 시작할 때 잠긴된 드라이브를 검사합니다.

    원하는 경우 **chkdsk** 디스크 오류를 해결 하려면 드라이브에 열려 있는 파일을 사용할 수 없습니다. 파일이 열려 있으면 다음 오류 메시지가 나타납니다.  
    ```
    Chkdsk cannot run because the volume is in use by another process. Would you like to schedule this volume to be checked the next time the system restarts? (Y/N)  
    
    ```  
    컴퓨터를 다시 시작 하면 다음에 드라이브에 있는지 확인 하려는 경우 **chkdsk** 드라이브를 확인 하 고 컴퓨터를 다시 시작 하는 경우 오류를 자동으로 수정 합니다. 드라이브 파티션 부팅 파티션인 경우 **chkdsk** 드라이브를 검사 한 후 컴퓨터를 자동으로 다시 시작 합니다.

    사용할 수도 있습니다는 **chkntfs /c** 명령 다음에 검사할 볼륨 컴퓨터를 다시 시작 합니다. 사용 된 **fsutil 커밋되지 않은 데이터 집합** 는 Windows가 실행 되도록 볼륨을 설정 하는 명령 (나타내는 손상)의 더티 비트 **chkdsk** 컴퓨터 다시 시작 되 면 합니다.
-   디스크 오류를 보고합니다.

    사용 해야 **chkdsk** 디스크 오류를 검사 FAT 또는 NTFS 파일 시스템에 가끔 있습니다. **Chkdsk** 디스크 공간과 디스크 사용을 검사 하 고 각 파일 시스템에 특정 한 상태 보고서를 제공 합니다. 상태 보고서에는 파일 시스템에서 발견 된 오류가 표시 됩니다. 실행 하는 경우 **chkdsk** 없이 **/f** 매개 변수는 활성 파티션에 보고할 수 있습니다 드라이브를 잠글 수 없기 때문에 잘못 된 오류입니다.
-   논리 디스크 오류 수정

    **Chkdsk** 지정 하는 경우에 논리 디스크 오류를 수정 합니다 **/f** 매개 변수입니다. **Chkdsk** 오류를 수정 하 여 드라이브를 잠글 수 있어야 합니다.

    FAT 파일 시스템에 대 한 복구는 일반적으로 디스크의 파일 할당 테이블을 변경 하 고 데이터의 손실을 나올 **chkdsk** 다음과 유사 하 게 확인 메시지가 표시 될 수 있습니다.  
    ```
    10 lost allocation units found in 3 chains.  
    Convert lost chains to files?  
    
    ```  
    키를 누르면 **Y**, Windows 각 손실 된 체인 루트 디렉터리에 있는 파일로 저장 형식 파일의에서 이름으로\<nnnn >.chk 합니다. 때 **chkdsk** 완료 되 면 모든 필요한 데이터를 포함 하는 경우이 파일을 확인할 수 있습니다. 키를 누르면 **N**, Windows는 디스크 오류를 수정 하지만 손실 된 할당 단위의 내용을 저장 하지 않습니다.

    사용 하지 않는 경우는 **/f** 매개 변수 **chkdsk** 는 파일을 수정 해야 하지만 오류를 수정 하지 않는 메시지를 표시 합니다.

    사용 하는 경우 **chkdsk /f** 매우 큰 디스크 또는 디스크 파일 (예를 들어 수백만 개의 파일), 매우 큰 숫자로 **chkdsk /f** 는 완료 하는 데 시간이 오래 걸릴 수 있습니다.
-   실제 디스크 오류 찾기

    사용 된 **/r** 디스크 섹터의 영향을 매개 변수를 파일 시스템에 실제 디스크 오류를 찾고에서 데이터를 복구 하려고 합니다.
-   사용 하 여 **chkdsk** 열려 있는 파일 사용

    지정 하는 경우는 **/f** 매개 변수 **chkdsk** 디스크에 열린 파일이 있는 경우 오류 메시지를 표시 합니다. 지정 하지 않으면 경우는 **/f** 매개 변수 및 존재 하는 열린 파일 **chkdsk** 디스크에서 손실 된 할당 단위를 보고할 수 있습니다. 열려 있는 경우 발생할 수 있는 파일이 아직 파일 할당 테이블에 기록 되지 않습니다. 경우 **chkdsk** 손실 되었다고 보고 많은 할당 단위는 디스크를 수리 해야 합니다.
-   사용 하 여 **chkdsk** 공유 된 폴더의 섀도 복사본과 함께

    공유 폴더 원본 볼륨의 섀도 복사본을 잠글 수 없으며 섀도 복사본 하는 동안 공유 폴더에 대 한 실행 **chkdsk** 소스에 대해 볼륨 수 잘못 된 오류가 보고 버리거나 **chkdsk** 예기치 않게 종료 합니다. 하지만 실행 하 여 오류에 대 한 섀도 복사본을 확인 수 **chkdsk** (매개 변수 제외) 읽기 전용 모드에서 폴더 공유 저장소 볼륨의 섀도 복사본을 확인 합니다.
-   종료 코드 이해

    다음 표에서 종료 코드를 **chkdsk** 이 완료 된 후 보고 합니다.  
    |종료 코드|설명|
    |---------|-----------|
    |0|없음 오류가 발견 되었습니다.|
    |1|오류 발견 하 고 해결 되었습니다.|
    |2|(예: 가비지 수집) 디스크 정리를 수행 또는 정리를 수행 하지 않았습니다 **/f** 지정 되지 않았습니다.|
    |3|디스크를 확인할 수 없습니다 오류를 해결할 수 또는 오류 때문에 수정 되지 않았습니다 **/f** 지정 되지 않았습니다.|
-   **chkdsk** 다른 매개 변수와 함께 명령을 복구 콘솔에서 사용할 수 있습니다.
-   을 자주 다시 시작 하는 서버에서 사용 하려면 수는 **chkntfs** 또는 **fsutil 더티 쿼리** chkdsk를 실행 하기 전에 이미 있는지 확인할 볼륨의 더티 비트 명령을 설정 합니다.

## <a name="BKMK_examples"></a>예제

D 드라이브에 디스크를 확인 하 고 windows에서 오류를 해결 하려면 다음을 입력 합니다.
```
chkdsk d: /f  

```
오류를 발견 하면 **chkdsk** 일시 중지 하 고 메시지를 표시 합니다. **Chkdsk** 디스크의 상태를 나열 하는 보고서를 표시 하 여 완료 합니다. 될 때까지 지정된 된 드라이브의 모든 파일을 열 수 없습니다 **chkdsk** 완료 합니다.

연속 되지 않은 블록에 대 한 현재 디렉터리에 FAT 디스크에 있는 모든 파일을 확인 하려면 다음을 입력 합니다.
```
chkdsk *.*  

```
**Chkdsk** 상태 보고서를 표시 한 후 연속 되지 않은 블록이 파일 사양을 일치 하는 파일을 나열 합니다.
#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)