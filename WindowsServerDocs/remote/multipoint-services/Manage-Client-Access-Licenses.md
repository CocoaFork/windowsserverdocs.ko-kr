---
title: 클라이언트 액세스 라이선스 관리
description: MultiPoint 서비스에서 Cal을 사용 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 4d809ab1bf2a18dff537bf63620623d576c0b25d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949879"
---
# <a name="manage-client-access-licenses"></a>클라이언트 액세스 라이선스 관리
MultiPoint Service를 스테이션으로 사용 되는 실행 중인 컴퓨터를 포함 하 여 MultiPoint 서비스 시스템에 연결 하는 모든 스테이션에 유효한 사용자 원격 데스크톱 있어야 *클라이언트 액세스 라이선스 (CAL)* 합니다.

실제 스테이션 대신 스테이션 가상 데스크톱을 사용 하는 경우 각 스테이션 가상 데스크톱에 대해 CAL을 설치 해야 합니다.  
  
1.  MultiPoint 서비스 컴퓨터 또는 서버에 연결 된 각 스테이션에 대해 클라이언트 라이선스를 구매 합니다. Cal 구매에 대 한 자세한 내용은 원격 데스크톱 라이선싱 설명서를 참조 하세요. 

2.  **시작** 화면이 열리면서 **다중 포인트 관리자**합니다.  
  
3.  **홈** 탭을 클릭 한 다음 **클라이언트 액세스 라이선스 추가**를 클릭 합니다.  이렇게 하면 CAL 라이선스에 대 한 관리 도구가 열립니다.

## <a name="set-the-licensing-mode-manually"></a>수동으로 라이선스 모드 설정
제대로 구성 되지 않은 경우 MultiPoint 서비스 설정에 유예 기간이 만료 되었다는 알림이 표시 됩니다. 라이선스 모드를 설정 하려면 다음 단계를 수행 합니다.

1. **로컬 그룹 정책 편집기** (gpedit.msc)를 시작 합니다.

2. 왼쪽 창에서 **로컬 컴퓨터 정책-> 컴퓨터 구성-> 관리 템플릿 > Windows 구성 요소->** 원격 데스크톱 서비스-> 원격 데스크톱 세션 호스트 라이선스로 이동 합니다.

3. 오른쪽 창에서 **지정 된 원격 데스크톱 라이선스 서버 사용** 을 마우스 오른쪽 단추로 클릭 하 고 **편집**을 선택 합니다.
   - 그룹 정책 편집기 대화 상자에서 **사용** 을 선택 합니다.
   - **사용할 라이선스 서버** 필드에 로컬 컴퓨터 이름을 입력 합니다.
   - **확인**을 선택합니다.
  
4. 오른쪽 창에서 **원격 데스크톱 라이선싱 모드 설정** 을 마우스 오른쪽 단추로 클릭 하 고 **편집** 을 선택 합니다.
   - 그룹 정책 편집기 대화 상자에서 **사용** 을 선택 합니다.
   - 장치/사용자 당 **라이선스 모드** 를 설정 합니다.
   - **확인**을 선택합니다. 

  
## <a name="see-also"></a>참고 항목  
[MultiPoint 관리자를 사용하여 시스템 작업 관리](Manage-System-Tasks-Using-MultiPoint-Manager.md)
