---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: "부록 E-Active Directory에 관리자 그룹 엔터프라이즈 보안"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 714bc0ab3fe15d09f4ccabb3f35d9b4519e5459c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>부록 e: Active Directory에 관리자 그룹 엔터프라이즈 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>부록 e: Active Directory에 관리자 그룹 엔터프라이즈 보안  
숲 루트 도메인에 보관 됩니다 되는 엔터프라이즈 관리자 (EA) 그룹 루트 도메인 관리자 계정 제외 하 고와 일상적으로 사용자가 보안 된에 설명 된 대로 제공 들어 [Active Directory에 부록 d: 보안 기본 제공 관리자 계정](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

기본적으로 각 도메인 숲에서 관리자가 그룹의 회원 엔터프라이즈의 관리자는 합니다. 숲 장애 복구 시나리오에서 발생 하는 경우 EA 권한이 필요할 수도 있으므로 EA 그룹 각 도메인에 있는 관리자가 그룹에서 제거 되지는 됩니다. 숲 속의 엔터프라이즈 관리자 그룹 보안 단계별 지침에 따라 있는에 설명 된 대로 합니다.  

엔터프라이즈 관리자 그룹 숲에서:  

1.  Ou 포함 된 각 도메인에 워크스테이션과 회원 서버에 연결 된 gpo, Enterprise 관리자 그룹에서 다음 사용자 권한에 추가 해야 **컴퓨터 구성 보안 로컬 Settings\User 권한 할당**:  

    -   네트워크에서이 컴퓨터에 대 한 액세스 거부  

    -   로그온 일괄 작업으로 거부  

    -   로그온 서비스 거부  

    -   로컬 로그온 거부  

    -   원격 데스크톱 서비스를 통해 로그온 거부  

2.  속성 또는 Enterprise 관리자 그룹의 회원 수정 되는 경우 알림을 보내도록 감사를 구성 합니다.  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>엔터프라이즈 관리자 그룹의 모든 구성원이 제거에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  

2.  하지 루트 도메인 콘솔 트리에서 숲을 관리 하는 경우 마우스 오른쪽 단추로 클릭 <Domain>을 차례로 클릭 하 고 **도메인 변경** (여기서 <Domain> 현재 관리 하는 도메인 이름입니다).  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  에 **도메인 변경** 대화 상자를 클릭 **찾아보기**루트 도메인 숲을 선택 하 고 클릭 **확인**합니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  EA 그룹의 모든 구성원이 제거:  

    1.  두 번 클릭는 **엔터프라이즈 관리자** 그룹화 하 고 클릭 한 다음는 **회원** 탭 합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  그룹의 회원을 클릭 **제거**, 클릭 **예**를 클릭 하 고 **확인**합니다.  

5.  EA 그룹의 모든 구성원이 제거 될 때까지 2 단계를 반복 합니다.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>보안 Active Directory에 Enterprise 관리자에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 확장 <Forest>\Domains\\<Domain>, 선택한 다음 **그룹 정책 개체** (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    > [!NOTE]  
    > 여러 도메인 포함 된 숲 속의 엔터프라이즈 관리자 그룹 보호 필요한 각 도메인에 있는 GPO 유사한 만들어야 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**를 클릭 하 고 **새로**합니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  에 **새 GPO** 대화 상자, 입력 <GPO Name>, 클릭 하 고 **확인** (여기서 <GPO Name> 이 GPO 이름입니다).  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 <GPO Name>를 클릭 하 고 **편집**합니다.  

6.  로 이동 **컴퓨터 구성 보안 로컬 정책**를 클릭 하 고 **사용자 권한 할당**합니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  엔터프라이즈 관리자 그룹의 회원 다음을 수행 하 여 네트워크를 통해 워크스테이션과 회원 서버에 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **엔터프라이즈 관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  엔터프라이즈 관리자 그룹의 회원 다음을 수행 하 여 일괄 작업으로 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

        > [!NOTE]  
        > 여러 도메인 포함 된 숲 속의 클릭 **위치** 루트 도메인 숲을 선택 합니다.  

    3.  입력 **엔터프라이즈 관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. EA 그룹의 회원 다음을 수행 하 여 서비스 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **서비스로 로그 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 차례로 클릭 하 고 **찾아보기**합니다.  

        > [!NOTE]  
        > 여러 도메인 포함 된 숲 속의 클릭 **위치** 루트 도메인 숲을 선택 합니다.  

    3.  입력 **엔터프라이즈 관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 엔터프라이즈 관리자 그룹의 회원 로컬로 로그온 워크스테이션과 회원 서버에는 다음을 수행 하 여 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **로컬 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 차례로 클릭 하 고 **찾아보기**합니다.  

        > [!NOTE]  
        > 여러 도메인 포함 된 숲 속의 클릭 **위치** 루트 도메인 숲을 선택 합니다.  

    3.  입력 **엔터프라이즈 관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

11. 엔터프라이즈 관리자 그룹의 회원 다음을 수행 하 여 원격 데스크톱 서비스를 통해 워크스테이션과 회원 서버에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로그온 원격 데스크톱 서비스를 통해 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 차례로 클릭 하 고 **찾아보기**합니다.  

        > [!NOTE]  
        > 여러 도메인 포함 된 숲 속의 클릭 **위치** 루트 도메인 숲을 선택 합니다.  

    3.  입력 **엔터프라이즈 관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

12. 종료 하려면 **그룹 정책 편집기 관리**, 클릭 **파일**를 클릭 하 고 **종료**합니다.  

13. **그룹 정책 관리**, 다음을 수행 하 여 GPO 구성원 서버 및 Ou 워크스테이션을 연결 합니다.  

    1.  로 이동는 <Forest>\Domains\\<Domain> (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    2.  OU GPO에 적용 되 고 클릭를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  방금 만든 GPO 선택 하 고 클릭 **확인**합니다.  

        ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  모든 일부 조직 구성 단위 워크스테이션 포함 된에 대 한 링크를 만듭니다.  

    5.  모든 일부 조직 구성 단위 구성원 서버를 포함 하는 링크를 만듭니다.  

    6.  여러 도메인 포함 된 숲 속의 엔터프라이즈 관리자 그룹 보호 필요한 각 도메인에 있는 GPO 유사한 만들어야 합니다.  

> [!IMPORTANT]  
> 점프 서버 관리 도메인 컨트롤러 및 Active Directory를 사용 하는 경우 점프 서버가이 Gpo 연결 되지 않은에 있는지 확인 합니다.  

### <a name="verification-steps"></a>확인 단계  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"액세스 거부가이 컴퓨터에는 네트워크에서" GPO 설정 확인  
모든 구성원이 서버 또는 (예: "점프 서버)" GPO 변경 영향을 받지 않는 워크스테이션 구성원 서버 또는 워크스테이션 GPO 변경 사항을 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 지도를 시도 GPO 설정을 확인 하 고 **NET 사용** 다음 단계를 수행 하 여 명령:  

1.  로컬 EA 그룹 구성원 계정을 사용 하 여 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 한 다음 **관리자 권한으로 실행** 관리자 권한 명령 프롬프트를 엽니다.  

4.  를 상승 승인 하 라는 메시지가 나타나면 클릭 **예**합니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  에 **명령 프롬프트** 창, 입력 **사용 net \\\<Server Name>\c$**, 여기서 <Server Name> 구성원 서버 또는 워크스테이션 네트워크를 통해 액세스를 시도 하는 이름입니다.  

6.  다음 스크린샷 표시 되 고 오류 메시지가 표시 됩니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정 확인  

모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

##### <a name="create-a-batch-file"></a>배치 파일을 만들어  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 입력 **디렉터리 c:**합니다.  

4.  클릭 **파일**를 클릭 하 고 **다른 이름으로 저장**합니다.  

5.  에 **파일** 상자 이름, 형식 ** <Filename>.bat** (여기서 <Filename> 새 배치 파일 이름).  

##### <a name="schedule-a-task"></a>작업을 예약  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 컴퓨터에서 실행 중인 Windows 8에서는 **검색** 상자에 입력 **작업을 예약**를 클릭 하 고 **작업을 예약**합니다.  

3.  클릭 **알림**를 클릭 하 고 **작업 만들기**합니다.  

4.  **작업 만들기** 대화 상자에서 입력 ** <Task Name> ** (여기서 <Task Name> 새 작업의 이름) 합니다.  

5.  클릭는 **작업** 탭 및 클릭 **새로**합니다.  

6.  에 **알림** 필드를 **프로그램 시작**합니다.  

7.  아래에서 **프로그램/스크립트**, 클릭 **찾아보기**을 찾아에서 만든 배치 파일 선택는 **배치 파일을 만들어** 섹션을 클릭 **열기**합니다.  

8.  클릭 **확인**합니다.  

9. 클릭 하 고 **일반** 탭 합니다.  

10. 에 **보안 옵션** 필드를 클릭 **사용자 또는 그룹 변경**합니다.  

11. EAs 그룹 구성원 계정의 이름을 입력 합니다 **이름 확인**를 클릭 하 고 **확인**합니다.  

12. 선택 **사용자의 로그온 실행** 선택한 **암호를 저장 하지 않는**합니다. 작업 로컬 컴퓨터 리소스에 액세스할 수 있는 기간은 됩니다.  

13. 클릭 **확인**합니다.  

14. 작업을 실행 하 요청 하는 사용자 계정 자격 대화 상자가 표시 됩니다.  

15. 자격 증명을 입력 한 후 클릭 **확인**합니다.  

16. 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"로그온 거부 as a service" GPO 설정 확인  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  아래에서 **로 로그온**선택 **이 계정**합니다.  

7.  클릭 **찾아보기**의 EAs 그룹 구성원 계정의 이름을 입력 합니다 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  아래에서 **암호:** 및 **암호 확인**선택한 계정의 암호를 입력 하 고 클릭 **확인**합니다.  

9. 클릭 **확인** 세 번 합니다.  

10. 마우스 오른쪽 단추로 클릭는 **인쇄 스풀러** 서비스 선택한 **다시 시작**합니다.  

11. 서비스를 다시 시작 하면 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>되돌리기 프린터 스풀러 서비스에 대 한 변경  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  아래에서 **로 로그온**는 **로컬 시스템** 계정, 클릭 한 **확인**합니다.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>"로그온 거부 로컬로" GPO 설정 확인  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 EA 그룹 구성원 계정을 사용 하 여 로그온 하려고 합니다. 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>"로그온 거부 원격 데스크톱 서비스를 통해" GPO 설정 확인  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **원격 데스크톱 연결**을 차례로 클릭 하 고 **원격 데스크톱 연결**합니다.  

3.  에 **컴퓨터** 필드를 클릭 한 다음 하 고, 연결 하려는 컴퓨터의 이름을 입력 **연결**합니다. (입력할 수도 있습니다 컴퓨터 이름 대신 IP 주소 합니다.)  

4.  메시지가 표시 되 면 EA 그룹의 회원은 계정의 자격 증명을 제공 합니다.  

5.  다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![관리자 그룹 엔터프라이즈 보안](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
