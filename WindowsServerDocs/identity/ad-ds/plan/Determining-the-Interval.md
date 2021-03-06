---
ms.assetid: 96a6749c-6c9f-4f2f-ad0a-51272d282ace
title: 간격 결정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 065b4ff707bdd8b82e33e06ad2b52c57a746045f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402622"
---
# <a name="determining-the-interval"></a>간격 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크 복제 간격 속성을 설정 하 여 일정에서 복제를 허용 하는 시간 동안 복제가 발생 하는 빈도를 지정 해야 합니다. 예를 들어 일정이 02:00 시간에서 04:00 시간 사이에 복제를 허용 하 고 복제 간격이 30 분으로 설정 된 경우 예약 된 시간 동안 복제가 최대 4 회까지 발생할 수 있습니다. 기본 복제 간격은 180 분 또는 3 시간입니다. 최소 간격은 15 분입니다.  
  
일정 창에서 복제가 발생 하는 빈도를 결정 하려면 다음 조건을 고려 합니다.  
  
-   간격이 적으면 대기 시간이 줄어들지만 WAN (광역 네트워크) 트래픽의 양이 증가 합니다.  
  
-   도메인 디렉터리 파티션을 최신 상태로 유지 하기 위해 짧은 대기 시간을 선호 합니다.  
  
저장소 및 전달 복제 전략을 사용 하면 디렉터리 업데이트를 모든 도메인 컨트롤러에 복제 하는 데 걸리는 시간을 결정 하기가 어렵습니다. 최대 대기 시간을 추정 하려면 다음 작업을 수행 합니다.  
  
-   다음 예제와 같이 네트워크에 있는 모든 사이트의 테이블을 만듭니다.  
  
    |사이트|Seattle|보스턴|Los Angeles|New York|워싱턴, D.C|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|||||  
    |보스턴||0.25||||  
    |Los Angeles|||0.25|||  
    |New York||||0.25||  
    |워싱턴, D.C|||||0.25|  
  
    사이트 내의 최악의 대기 시간은 15 분으로 예상 됩니다.  
  
-   복제 일정에서 두 허브 사이트를 연결 하는 모든 사이트 링크에서 가능한 최대 복제 대기 시간을 결정 합니다.  
  
    예를 들어 3 시간 마다 시애틀와 뉴욕 간에 복제가 발생 하는 경우 이러한 사이트 간의 복제에 대 한 최대 지연은 3 시간입니다. 뉴욕 및 시애틀 간의 복제 지연이 모든 허브 사이트에서 가장 긴 예약 된 지연 인 경우 모든 허브 사이의 최대 대기 시간은 3 시간입니다.  
  
-   각 허브 사이트에 대해 허브 사이트와 해당 위성 사이트 간 최대 대기 시간 테이블을 만듭니다.  
  
    예를 들어, D.C와 워싱턴 간에 복제가 발생 하는 경우,이는 4 시간 마다, 뉴욕 및 해당 위성 사이트 간의 가장 긴 복제 지연입니다. 뉴욕의 위성 사이트 간 최대 대기 시간은 4 시간입니다.  
  
-   이러한 최대 대기 시간을 결합 하 여 전체 네트워크에 대 한 최대 대기 시간을 결정 합니다.  
  
    예를 들어 시애틀 및 로스앤젤레스의 위성 사이트 간 최대 대기 시간이 하루 이면이 링크 집합의 최대 복제 대기 시간 (워싱턴, D.C-뉴욕-로스앤젤레스)은 31 시간, 즉 4 (워싱턴, D.C-뉴욕) + 3 (신규 시애틀) + 24 (시애틀-로스앤젤레스)와 같이 다음 표에 나와 있습니다.  
  
    |사이트|Seattle|보스턴|Los Angeles|New York|워싱턴, D.C|  
    |---------|-----------|----------|---------------|------------|--------------------|  
    |Seattle|0.25|4 + 3|24.00|3.00|4 + 3|  
    |보스턴||0.25|4 + 3 + 24|4.00|4.00|  
    |Los Angeles|||0.25|24 + 3|24 + 3 + 4|  
    |New York||||0.25|4.00|  
    |워싱턴, D.C|||||0.25|  
  


