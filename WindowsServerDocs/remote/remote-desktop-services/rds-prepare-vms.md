---
title: 원격 데스크톱용 가상 컴퓨터 준비
description: 원격 데스크톱 구성 요소를 위한 VM 준비
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 07/21/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fc39dff-61ca-4eba-81ab-52289081bead
author: lizap
manager: dongill
ms.openlocfilehash: 6a1f0bfef21351894d3b9c2cfd8d044491834f6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387254"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>원격 데스크톱용 가상 컴퓨터 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

물리적 서버 또는 가상 머신에서 원격 데스크톱 서비스 구성 요소를 설치할 수 있습니다. 

첫 번째 단계는 [Azure에서 Windows Server 가상 머신을 만드는](/azure/virtual-machines/windows/quick-create-portal) 것입니다. RD 세션 호스트용 VM, 연결 브로커용 VM 및 RD 웹 및 RD 게이트웨이용 VM 3개를 생성합니다. RDS 배포의 가용성을 보장하려면 가용성 세트(VM 생성 프로세스에서 **고가용성** 아래)를 만들고 해당 가용성 세트에서 여러 VM을 그룹화합니다.
 
VM을 만든 후 다음 단계를 사용하여 RDS에 대해 준비합니다.

1.  RDC(원격 데스크톱 연결) 클라이언트를 사용하여 가상 머신에 연결합니다.  
    1.  Azure Portal에서 리소스 그룹 보기를 연 다음, 배포에 대해 사용할 리소스 그룹을 클릭합니다.  
    2.  새 RDSH 가상 머신(예: Contoso-Sh1)을 선택합니다.  
    3.  클릭 **연결 > 열고** 를 원격 데스크톱 클라이언트를 엽니다.  
    4.  클라이언트에서 클릭 **연결**, 를 클릭 하 고 **다른 사용자 계정을 사용 하 여**합니다. 로컬 관리자 계정의 사용자 이름 및 암호를 입력합니다.  
    5.  클릭 **예** 때 인증서에 대 한 경고 메시지를 받습니다.  
2.  원격 관리를 사용하도록 설정합니다.  
    1.  서버 관리자에서 **로컬 서버 > 원격 관리 현재 설정(해제)** 을 클릭합니다.  
    2.  **원격 관리를 사용하도록 설정**을 선택합니다.  
    3.  **확인**을 클릭합니다.  
3.  옵션: 업데이트를 자동으로 다운로드 및 설치하지 않도록 일시적으로 Windows 업데이트를 설정할 수 있습니다. 이렇게 하면 RDSH 서버를 배포하는 동안 변경 사항과 시스템 재시작을 방지할 수 있습니다.  
    1.  서버 관리자에서 **로컬 서버 > Windows 업데이트 현재 설정**을 클릭합니다.  
    2.  **고급 옵션 > 업그레이드 연기**를 선택합니다.   
4.  서버를 도메인에 추가합니다.  
    1.  서버 관리자에서 **로컬 서버 > 작업 그룹 현재 설정**을 클릭합니다.  
    2.  **변경 > 도메인**을 클릭한 다음, 도메인 이름을 입력합니다(예: Contoso.com).  
    3.  도메인 관리자 자격 증명을 입력합니다.  
    4.  가상 컴퓨터를 다시 시작합니다.  
5.  RD 웹 및 GW 가상 머신에 대해 1-4단계를 반복합니다.  
6.  RD 연결 브로커 가상 머신에 대해 1-4단계를 반복합니다.  
7.  RD 연결 브로커 가상 머신에서 연결된 디스크를 초기화하고 포맷합니다.  
    1.  RD 연결 브로커 가상 머신에 연결합니다(위 1단계).  
    2.  서버 관리자에서 **도구 > 컴퓨터 관리**를 클릭합니다.  
    3.  **디스크 관리**를 클릭합니다.  
    4.  연결된 디스크를 선택한 다음, **MBR(마스터 부트 레코드)** 을 클릭한 다음, **확인**을 클릭합니다.  
    5.  새 디스크(**할당되지 않음**으로 표시됨)를 마우스 오른쪽 단추로 클릭하고 **새 단순 볼륨**을 클릭합니다.  
    6.  **새 단순 볼륨** 마법사에서 기본값을 수락하지만 **볼륨 레이블**(예: 공유)에 해당하는 이름을 제공합니다.  
8.  RD 연결 브로커 가상 머신에서 사용자 프로필 디스크 및 인증서에 대한 파일 공유를 만듭니다.   
    1.  파일 탐색기를 열고 **이 PC**를 클릭한 후, 파일 공유에 대해 추가한 디스크를 엽니다.  
    2.  **홈** 및 **새 폴더**를 클릭합니다.  
    3.  사용자 디스크 폴더에 사용할 이름을 입력합니다(예: **UserDisks**).  
    4.  새 폴더를 마우스 오른쪽 단추로 클릭하고 **속성 > 고급 공유**를 클릭합니다.  
    5.  **이 폴더 공유**를 선택하고 **사용 권한**을 클릭합니다.  
    6.  선택 **Everyone**, 를 클릭 하 고 **제거**합니다. 이제 클릭 **추가**, 입력 **Domain Admins**, 를 클릭 하 고 **확인**합니다.  
    7.  선택 **모든 권한을 허용**, 를 클릭 하 고 **확인 > 확인 > 닫기**합니다.  
    8.  c-g단계를 반복하여 인증서에 대한 공유 폴더를 만듭니다.   


