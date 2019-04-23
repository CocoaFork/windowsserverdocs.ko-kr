---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: 부록 E-Active Directory의 Enterprise Admins 그룹 보안
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 976eb8c7159c8349b72bee05a5248b5cc116d96b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856724"
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>부록 B: Active Directory의 Enterprise Admins 그룹 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>부록 B: Active Directory의 Enterprise Admins 그룹 보안  
에 설명 된 대로 보안이 제공 포리스트 루트 도메인에서 예외일의 Enterprise Admins (EA) 그룹에서 루트 도메인의 관리자 계정의 예외일 수 있음 일상적으로 사용자를 포함 해야 [부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

Enterprise Admins는 기본적으로 포리스트의 각 도메인의 관리자 그룹의 구성원입니다. 포리스트 재해 복구 시나리오에서 발생할 경우 EA 권한이 필요할 수도 있으므로 EA 그룹 각 도메인의 관리자 그룹에서 제거 되지 해야 합니다. 포리스트의 Enterprise Admins 그룹의 보안을 유지 해야 이어지는 단계별 지침에 설명 된 대로 합니다.  

포리스트의 Enterprise Admins 그룹:  

1.  구성원 서버 및 워크스테이션 각 도메인에 포함 된 Ou에 연결 된 Gpo, Enterprise Admins 그룹에 다음 사용자 권한을 추가 해야 합니다 **컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ Policies\ 사용자 권한 할당**:  

    -   네트워크에서 이 컴퓨터 액세스 거부  

    -   일괄 작업으로 로그온 거부  

    -   서비스로 로그온 거부  

    -   로컬 로그온 거부  

    -   원격 데스크톱 서비스를 통한 로그온 거부  

2.  감사는 Enterprise Admins 그룹의 구성원 또는 속성을 수정한 경우 경고를 보내도록 구성 합니다.  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Enterprise Admins 그룹에서 모든 구성원을 제거 하기 위한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory Users and Computers**합니다.  

2.  콘솔 트리에서 포리스트 루트 도메인을 관리 하는 경우 마우스 오른쪽 단추로 클릭 <Domain>를 클릭 하 고 **도메인 변경** (여기서 <Domain> 현재 관리 하는 도메인의 이름입니다).  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  에 **도메인 변경** 대화 상자, 클릭 **찾아보기**포리스트의 루트 도메인을 선택 하 고 클릭 **확인**합니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  EA 그룹에서 모든 구성원을 제거 합니다.  

    1.  두 번 클릭 합니다 **Enterprise Admins** 그룹을 클릭 한 다음는 **멤버** 탭 합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  그룹의 멤버를 선택, 클릭 **제거할**, 클릭 **예**, 클릭 **확인**합니다.  

5.  EA 그룹의 모든 구성원을 제거할 때까지 2 단계를 반복 합니다.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Active Directory에서 엔터프라이즈 관리자를 보호 하기 위한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 <Forest>\Domains\\<Domain>를 차례로 **그룹 정책 개체** (여기서 <Forest> 포리스트의 이름 및 <Domain> 하려는 도메인의 이름 그룹 정책 설정).  

    > [!NOTE]  
    > 여러 도메인이 포함 된 포리스트에 있는 비슷한 GPO Enterprise Admins 그룹 보호는 필요한 각 도메인에 만들어야 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**, 클릭 **새로 만들기**합니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  에 **새 GPO** 대화 상자에서 <GPO Name>, 클릭 **확인** (여기서 <GPO Name> 이 GPO의 이름입니다).  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 <GPO Name>, 클릭 **편집**합니다.  

6.  이동할 **컴퓨터 구성 \ 정책 \ 로컬 정책**, 클릭 **사용자 권한 할당**합니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  다음을 수행 하 여 네트워크를 통해 멤버 서버 및 워크스테이션에에서 Enterprise Admins 그룹의 멤버를 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Enterprise Admins**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  Enterprise Admins 그룹의 멤버는 다음을 수행 하 여 일괄 작업으로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

        > [!NOTE]  
        > 포리스트에 여러 도메인이 포함 된, 클릭 **위치** 포리스트의 루트 도메인을 선택 합니다.  

    3.  형식 **Enterprise Admins**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 다음을 수행 하 여 서비스로 로그온 EA 그룹의 구성원을 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **서비스로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 을 클릭 한 다음 **찾아보기**합니다.  

        > [!NOTE]  
        > 포리스트에 여러 도메인이 포함 된, 클릭 **위치** 포리스트의 루트 도메인을 선택 합니다.  

    3.  형식 **Enterprise Admins**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 로컬로 로그온 구성원 서버 및 워크스테이션에 다음을 수행 하 여에서 Enterprise Admins 그룹의 멤버를 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로컬 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 을 클릭 한 다음 **찾아보기**합니다.  

        > [!NOTE]  
        > 포리스트에 여러 도메인이 포함 된, 클릭 **위치** 포리스트의 루트 도메인을 선택 합니다.  

    3.  형식 **Enterprise Admins**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

11. Enterprise Admins 그룹의 멤버는 다음을 수행 하 여 구성원 서버 및 워크스테이션을 통해 원격 데스크톱 서비스를 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **원격 데스크톱 서비스를 통한 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 을 클릭 한 다음 **찾아보기**합니다.  

        > [!NOTE]  
        > 포리스트에 여러 도메인이 포함 된, 클릭 **위치** 포리스트의 루트 도메인을 선택 합니다.  

    3.  형식 **Enterprise Admins**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

12. 끝내려면 **그룹 정책 관리 편집기**, 클릭 **파일**, 클릭 **종료**합니다.  

13. **그룹 정책 관리**, 다음을 수행 하 여 Ou 워크스테이션 및 구성원 서버에 GPO을 연결 합니다.  

    1.  로 이동 합니다 <Forest>\Domains\\ <Domain> (여기서 <Forest> 포리스트의 이름 및 <Domain> 그룹 정책 설정 하려는 도메인의 이름입니다).  

    2.  GPO에 적용 됩니다을 클릭 하는 OU를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  방금 만든 GPO를 선택 하 고 클릭 **확인**합니다.  

        ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

    6.  여러 도메인이 포함 된 포리스트에 있는 비슷한 GPO Enterprise Admins 그룹 보호는 필요한 각 도메인에 만들어야 합니다.  

> [!IMPORTANT]  
> 점프 서버 도메인 컨트롤러와 Active Directory 관리를 사용 하는 경우이 Gpo 연결 되지 않은 OU에 점프 서버가 있는지는 확인 합니다.  

### <a name="verification-steps"></a>확인 단계  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>액세스 거부 "이이 컴퓨터에 네트워크에서" GPO 설정을 확인 합니다.  
구성원 서버 또는 워크스테이션 (예: "점프 서버") GPO 변경 내용의 영향을 받지 않는 구성원 서버 또는 워크스테이션 GPO 변경이 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 매핑할 시도 GPO 설정을 확인 하는 **NET USE** 다음 단계를 수행 하 여 명령:  

1.  EA 그룹의 구성원 인 계정을 사용 하 여 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행** 열려면 관리자 권한 명령 프롬프트입니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  에 **명령 프롬프트** 창, 형식 **사용 하 여 net \\ \\ \<서버 이름\>\c$** 여기서 \<서버 이름을\> 는 구성원 서버 또는 네트워크를 통해 액세스를 시도 중인 워크스테이션의 이름입니다.  

6.  다음 스크린 샷에 표시 되는 오류 메시지를 표시 합니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정을 확인 합니다.  

구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

##### <a name="create-a-batch-file"></a>배치 파일을 만듭니다  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 형식 **dir c:** 합니다.  

4.  클릭 **파일**, 클릭 **다른 이름으로 저장**합니다.  

5.  에 **파일** 이름 상자에서  **<Filename>.bat** (여기서 <Filename> 새 일괄 처리 파일의 이름입니다).  

##### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 컴퓨터에서 Windows 8을 실행에 **검색** 상자에 입력 **작업 예약**, 클릭 **작업을 예약**합니다.  

3.  클릭 **동작**, 클릭 **작업 만들기**합니다.  

4.  에 **작업 만들기** 대화 상자에서 **<Task Name>** (여기서 <Task Name> 새 작업의 이름입니다).  

5.  클릭 합니다 **동작** 탭을 클릭 **새로 만들기**합니다.  

6.  에 **동작** 필드를 선택한 **프로그램을 시작할**합니다.  

7.  아래 **프로그램/스크립트**, 클릭 **찾아보기**에서 찾아에서 생성 된 일괄 처리 파일을 선택 합니다 **배치 파일을 만듭니다** 섹션을 클릭 **엽니다**.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. 에 **보안 옵션** 필드, 클릭 **사용자 또는 그룹 변경**합니다.  

11. EAs 그룹의 구성원 인 계정의 이름을 입력, 클릭 **이름 확인**, 클릭 **확인**합니다.  

12. 선택 **사용자의 로그온 여부 실행** 선택한 **암호를 저장 하지 않는**합니다. 작업만 로컬 컴퓨터 리소스에 액세스할을 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 요청 사용자 계정 작업을 실행 하려면 자격 증명 대화 상자가 표시 됩니다.  

15. 자격 증명을 입력 한 후 클릭 **확인**합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO 설정을 "로그온 거부 as a service"를 확인 합니다.  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  아래 **로 로그온**를 선택 **이 계정은**합니다.  

7.  클릭 **찾아보기**EAs 그룹의 구성원 인 계정의 이름을 입력, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  아래 **암호:** 하 고 **암호 확인**선택한 계정의 암호를 입력 하 고 클릭 **확인**합니다.  

9. 클릭 **확인** 3 회 더 합니다.  

10. 마우스 오른쪽 단추로 클릭 합니다 **인쇄 스풀러** 선택한 서비스 **다시 시작**합니다.  

11. 서비스를 다시 시작할 때 다음과 유사한 대화 상자가 표시 됩니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스에 대 한 변경 내용 되돌리기  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  아래 **로 로그온**를 선택 합니다 **로컬 시스템** 를 고려 하 고 클릭 **확인**.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>GPO 설정을 "로컬 로그온 거부"를 확인 합니다.  

1.  구성원 서버 또는 워크스테이션 GPO 변경의 영향, EA 그룹의 구성원 인 계정을 사용 하 여 로컬로 로그온 하려고 합니다. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>GPO 설정 "에서 원격 데스크톱 서비스를 통한 로그온을 거부"를 확인 합니다.  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **원격 데스크톱 연결**를 클릭 하 고 **원격 데스크톱 연결**합니다.  

3.  에 **컴퓨터** 필드에 연결 하 고 클릭 하려는 컴퓨터의 이름을 입력 합니다 **Connect**합니다. (입력할 수도 있습니다 컴퓨터 이름 대신 IP 주소입니다.)  

4.  메시지가 표시 되 면 EA 그룹의 구성원 인 계정의 자격 증명을 제공 합니다.  

5.  다음과 유사한 대화 상자가 표시 됩니다.  

    ![엔터프라이즈 관리자 그룹을 보호](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
