---
ms.assetid: e6fa9069-ec9c-4615-b266-957194b49e11
title: AD RMS Windows Server 2016으로 업그레이드
description: ''
author: msmbaldwin
ms.author: esaggese
ms.date: 05/30/2019
ms.topic: article
ms.openlocfilehash: f5d621a0ba06f5b1beb97ccdbffb8376b5503168
ms.sourcegitcommit: 927adf32faa6052234ad08f21125906362e593dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033345"
---
# <a name="upgrading-ad-rms-to-windows-server-2016"></a>AD RMS Windows Server 2016으로 업그레이드

## <a name="introduction"></a>소개

Active Directory Rights Management Services (AD RMS)는 중요 한 문서와 메일을 보호 하는 Microsoft 서비스입니다. 방화벽 및 Acl과 같은 다른 기존 보호 메서드와 달리 AD RMS 암호화 및 보호는 파일로 이동 하는 위치 또는 전송 하는 방법에 관계 없이 지속 됩니다. 

이 문서에서는 SQL Server 2012를 사용 하 여 Windows Server 2012 R2에서 Windows Server 2016 및 SQL Server 2016으로 마이그레이션에 대 한 지침을 제공 합니다. 지원 되는 이전 버전의 AD RMS에서 마이그레이션하려면 동일한 프로세스를 사용할 수 있습니다.
Active Directory Rights Management Services 더 이상 활발 하 게 개발 하 고 최신 기능에 대 한 고객은 마이그레이션을 고려해 야 [Azure Information Protection](https://azure.microsoft.com/services/information-protection/), 등을 제공 하는 더 완전 한 장치 및 응용 프로그램 지원 기능의 포괄적인 집합입니다. 

콘텐츠를 다시 보호 하지 않고 AD RMS에서 Azure Information Protection으로 마이그레이션에 대 한 내용은 [Azure Information Protection 마이그레이션 설명서](https://docs.microsoft.com/azure/information-protection/migrate-from-ad-rms-to-azure-rms)합니다.

## <a name="about-the-environment-used-in-this-guide"></a>이 가이드에 사용 되는 환경에 대 한

AD FS는 AD RMS 설치 과정의 선택적 구성 요소입니다. 이 가이드에서는 ADFS 사용 가정 합니다. ADFS는 사용자가 AD RMS를 지 원하는 환경에서 사용 되지 않은, 경우에 ADFS를 참조 하는 모든 단계를 건너뛸 수 있습니다.

이 가이드에서는 병렬 설치를 수행 하 고 백업을 통해 데이터베이스를 이동 하 여 SQL Server는 SQL Server 2016으로 업그레이드 됩니다. 또는 AD RMS 및 ADFS 데이터베이스 서버 위치에서 SQL Server 2016으로 업그레이드할 수 있을 경우 후 이동할 수 있습니다이 문서의 다음 섹션으로이 섹션의 단계를 수행 하지 않고도 작업입니다.  

## <a name="installation"></a>설치

### <a name="configuring-sql-server-2016"></a>SQL Server 2016 구성

다음 섹션에서는 세부 정보 구현 작업을 직접 구성과 관련 된 SQL Server 2016 합니다. 이 가이드는 이러한 작업을 완료 하려면 서버 관리자 및 SQL Server Management Studio를 사용 하 여 중점을 둡니다.

SQL Server 2016 설치에서 이러한 단계를 완료 해야 합니다. 조직의 표준 사례 및 정책에 따라 적합 한 하드웨어에서 SQL Server 2016을 설치 합니다. 

#### <a name="preparing-the-sql-server"></a>SQL Server 준비

다음 섹션에는 Windows Server 2016을 사용 하도록 AD RMS 플랫폼에서 다른 서비스를 업그레이드 하기 전에 SQL Server 2016으로 업그레이드할 수 있도록 SQL Server를 준비 하는 방법을 자세히 설명 합니다.

##### <a name="adding-cname-for-sql-server-2016-to-dns"></a>SQL Server 2016에 대 한 DNS CNAME 추가

CNAME는 Windows Server 2016 설치 발생 적절 한 데이터를 새 SQL Server 2016을 가리키는 수는 이후 확인 하는 데 사용 됩니다. **참고: ADFS와 AD RMS 서비스에 대 한 CNAME을 이미 사용 하는 경우 다음 단계 이동할 수 있습니다.**


**SQL Server 2016에 대 한 dns CNAME를 추가 하려면**

1.  도메인 관리자 자격 증명을 사용 하 여 Windows Server 2012 R2 도메인 컨트롤러에 로그온 합니다.

2.  서버 관리자를 엽니다.

3.  클릭 **도구가** 선택한 **DNS** DNS 관리자를 엽니다.

4.  왼쪽된 탐색 창에서 DC를 확장 하 고 엽니다 **정방향 조회 영역**합니다.

5.  적절 한 도메인 리소스를 열려면 보기 오른쪽 창에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 별칭 (CNAME)** CNAME을 만들기 시작 합니다.

6.  별칭 이름을 입력에 다른와 구분 하기 위해 논리적 이름이 있을 수 (탐색 SQLADRMS 또는 SQLADFS)

7.  이름을 입력 한 후 새 SQL Server 2016 서버 될 대상 호스트에 대 한 FQDN을 제공 합니다. (예: SQL2016.contoso.com)

8.  모든 정보를 입력 한 후 클릭 **확인**합니다.

##### <a name="backup-the-ad-rms-and-adfs-databases"></a>AD RMS 및 ADFS 데이터베이스를 백업 합니다.

AD RMS 및 ADFS 데이터베이스 서버 사용 허가자 인증서, 권한 정책 템플릿, ADFS 구성 데이터 및 로깅 정보 공개 키와 같은 AD RMS에 필요한 중요 한 정보를 저장 합니다. 이러한 데이터베이스 없이 클라이언트는 다른 문제가 간에 보호 된 콘텐츠를 사용 하는 라이선스를 발급할 수 없습니다.

데이터베이스의 AD RMS 구성 데이터베이스에서 가장 중요 한 비율은 SLC에 저장 하는 대로 권한 정책 템플릿을, 사용자의 키 및 구성 정보입니다. 따라서 모든 AD RMS 및 ADFS 데이터베이스를 백업 하려면 주의 해야, 있지만 구성 데이터베이스를 정기적으로 백업할 계획 해야 합니다.

로깅 데이터베이스 인증서 및 사용 하 여 라이선스에 대 한 AD RMS 클러스터에 대 한 사용자 요청에 대 한 정보를 저장합니다. 이 데이터베이스의 백업 전략에 따라 이러한 종류의 정보를 유지 하는 것에 대 한 회사 정책을 기반으로 해야 합니다.

디렉터리 서비스 데이터베이스를 AD RMS 기능에 중요 하지 않은 고 최신 데이터를 손실 된 경우 데이터베이스는 AD RMS 서버에서 인증서에 대 한 요청을 수신 하므로 정보를 사용 하 여 다시 채울 라이선스를 사용 합니다. 이 데이터베이스를 정기적으로 백업 해야 하지만 AD RMS를 배포한 후에 원래 구성 된 이상 데이터베이스의 복사본을 수행 해야 합니다.

**Microsoft SQL Server를 사용 하 여 AD RMS 및/또는 ADFS 데이터베이스를 백업 하려면**

1.  SQL 2012와 Windows Server 2012 R2 AD RMS 데이터베이스 서버에 로그온 합니다.

2.  클릭 **시작**, 클릭 **프로그램도**, 클릭 **Microsoft SQL Server**, 클릭 **SQL Server Management Studio**합니다.

3.  에 **서버에 연결** 창에서 AD RMS 데이터베이스를 호스팅하는 서버는 확인 합니다 **서버 이름** 상자 하 고 클릭 **연결**합니다.

4.  **데이터베이스**를 확장합니다. 적절 한 데이터베이스를 마우스 오른쪽 단추로 클릭 (**DRM** 및 **Adfs**)를 가리키도록 **작업**를 선택한 **백업**합니다.

5.  나머지 데이터베이스에 대 한 4 단계를 반복 합니다.

6.  네트워크 또는 마이그레이션하는 동안 이후 단계에 대 한 필요 하므로 대로 저장소 장치를 사용 하 여 다른 컴퓨터에서 데이터베이스를 백업에 액세스할 수 있는지 확인 합니다.

이제 데이터베이스 복사본을 안전한 위치에 저장할 수 있습니다. 데이터베이스를 자주 백업 해야 합니다.

##### <a name="adding-domain-admin-sql-ad-rms-andor-adfs-service-account-to-sql-server-2016"></a>도메인 관리자를 추가, SQL, AD RMS 및/또는 ADFS 서비스 계정을 SQL Server 2016

다음 단계를 SQL Server 2016 Windows Server 2012 R2 환경에서 데이터를 마이그레이션하는 데 유용한 다양 한 서비스 계정을 추가 하는 방법을 소개 합니다. 이렇게 하면 콘텐츠에 액세스 하 고 데이터를 처리 하려고 할 때 적절 한 권한이 제공 됩니다.

**SQL Server에 도메인 관리자, SQL, AD RMS 및 ADFS 서비스 계정을 추가 하려면**

1.  로컬 관리자 계정으로 SQL Server 2016을 사용 하 여 서버에 로그온 합니다.

2.  클릭 **시작**, 클릭 **프로그램도**, 클릭 **Microsoft SQL Server**, 클릭 **SQL Server Management Studio**합니다.

3.  에 **서버에 연결** 창에서 AD RMS 데이터베이스를 호스팅하는 서버는 확인 된 **서버 이름** 상자 인증에 대 한 드롭다운 메뉴를 클릭 하 고 선택 **SQL Server 인증**합니다.

4.  에 **로그인** 필드의 이름을 입력 합니다 (예: 로컬 관리자 계정 localadmin) 적절 한 암호를 제공 하 고 클릭 **Connect**합니다.

5.  확장 **Security** 마우스 오른쪽 단추로 클릭 한 다음 **로그인** 선택한 **새 로그인** 나타나는 상황에 맞는 메뉴에서.

6.  창이 나타나면 도메인 관리자 계정에 입력 되 면 합니다 **로그인 이름** 필드 (예: Contoso\\ContosoAdmin)

7.  왼쪽된 탐색 창에서 선택 **서버 역할**입니다.

8.  다음에 대 한 확인란 **sysadmin** 서버 역할 및 클릭 **확인**합니다.

9.  다시 시작 **SQL Server Management**합니다.

10. 에 **서버에 연결** 창에서 AD RMS 데이터베이스를 호스팅하는 서버는 확인 된 **서버 이름** 상자 인증에 대 한 드롭다운 메뉴를 클릭 하 고 선택 **Windows 인증** 누릅니다 **Connect**합니다.

##### <a name="restoring-the-ad-rms-and-adfs-databases-to-sql-server-2016"></a>SQL Server 2016에 AD RMS 및 ADFS 데이터베이스 복원

다음 단계를 새 2016 인스턴스를 이전 SQL Server 인스턴스에서 데이터를 복원 하는 방법을 소개 합니다. 새 SQL 이전 AD RMS 및 ADFS 데이터베이스에서 관련 구성 데이터를 사용할 수 있습니다.

**새 SQL server 이전 SQL Server에서 데이터를 복원 하려면**

1.  SQL Server 2016을 사용 하 여 적절 한 계정 사용 하 여 서버에 로그온 합니다.

2.  왼쪽된 탐색 창에서 마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **Restore Database** 복원 프로세스를 시작 합니다.

3.  아래 **소스** 선택 **장치** 이전 단계에서 저장 된 데이터베이스 파일 위치를 찾아야 합니다.

4.  파일 선택 했으면, 클릭 **확인**합니다.

5.  확인 추가 된 모든 데이터베이스 파일을 클릭 하 여 프로세스를 완료 **확인**합니다.

### <a name="configuring-windows-server-2016-active-directory-federation-services-ad-fs"></a>Windows Server 2016 Active Directory Federation Services (AD FS)를 구성합니다.

응용 프로그램으로 AD RMS로 single sign-on (SSO) 액세스 권한을 제공 하려면 AD FS 배포 되었습니다. 것도 구성 되었고 사용 하 여 AD RMS 모바일 장치 확장 (MDE), Mac 및 최종 사용자에 대 한 모바일 장치 지원을 가능 합니다.

다음 섹션에서는 AD FS 배포에서 수행 해야 하는 운영 작업에 지침을 제공 합니다.

#### <a name="adding-a-2016-ad-fs-server-to-the-farm"></a>2016 AD FS 서버를 팜에 추가

AD RMS 배포를 지원 하도록 추가 AD FS 서버를 배포할 수 있습니다. AD RMS 서버 또는 추가 응용 프로그램에 대 한 트래픽이 증가할된 경우이 작업을 수행 하도록 선택할 수 있습니다 또는 AD FS에 대 한 현재 사용 중인 서버 중 하나를 사용 중지 해야 합니다.

**2016 AD FS 서버를 팜에 추가 하려면**

1.  Azure AD Connect 서버에서 두 번 클릭 합니다 **Azure AD Connect** 아이콘을 Azure AD Connect 마법사를 시작 합니다.

2.  시작 페이지에서 클릭 **구성**합니다.

3.  추가 작업 페이지에서 클릭 **추가 페더레이션 서버 배포** 을 클릭 한 다음 **다음**합니다.

4.  Azure AD 페이지로 연결에서의 사용자 이름 및 전역 관리 권한이 있는 계정의 암호를 입력 한 다음 클릭 **다음**합니다.

5.  도메인 관리자 자격 증명 페이지에서 사용자 이름 및 도메인 관리자 권한이 있는 계정의 암호를 입력 하 고 클릭 **다음**합니다.

6.  클릭 **찾아보기** 및 선택 인증서 파일을 사용 하는 경우 Azure AD Connect를 사용 하 여 AD FS 팜을 구성 합니다.

7.  클릭 **암호 입력** 인증서 암호 대화 상자를 엽니다.

8.  암호 필드에 인증서의 암호를 입력 한 다음 클릭 **확인**합니다.

9.  **다음**을 클릭합니다.

10. AD FS 서버 페이지에서 이름 또는 새 AD FS 서버의 IP 주소를 입력 하 고 클릭 **추가**합니다.

11. 준비 구성 페이지를 클릭 **설치**합니다.

12. 설치 완료 페이지에서 클릭 **종료**합니다.

#### <a name="raising-the-adfs-farm-behavior-level"></a>ADFS 팜 동작 수준 올리기

와 같은 현재 환경 수준을 초과 하는 ADFs 서버를 배포할 때 Windows Server 2012 r 2에서 ADFS를 유지 한 다음는 ADFS Windows Server 2016, 팜 동작 수준 증가 해야를 추가 합니다. 이 최신 정보와 함수 환경이 사용 중인지 확인 해야 합니다.

**ADFS 팜 동작 수준 올리기**

1.  Windows Server 2016 ADFS로 이동 합니다.

2.  관리자 PowerShell 세션을 엽니다.

3.  다음 명령을 입력 합니다.  **\$cred = Get-credential**

4.  자격 증명을 묻는 창이 표시 됩니다 도메인 관리자 자격 증명을 입력 합니다.

5.  이 명령을 입력 합니다. **Invoke-AdfsFarmBehaviorLevelRaise -Credential \$cred**

6.  메시지가 표시 됩니다, **이 작업을 계속 하 시겠습니까?** 입력 한 다음 **는** 프롬프트를 허용 하려면.

7.  명령이 완료 되 면 팜 동작 수준 설치를 업데이트 하 고 준비 됩니다.

#### <a name="enabling-mobile-device-extension-logging"></a>모바일 장치 확장 로깅을 사용 하도록 설정

모바일 장치 확장 최종 사용자 장치에서 수신 하는 요청을 기록할 수 있습니다. 기본적으로 비활성화 되어 있으며만 문제 해결 시나리오에서 로깅을 사용 하도록 설정 하는 것이 좋습니다. 모바일 장치 및 최종 사용 라이선스를 획득 또는 부트스트랩 데스크톱 컴퓨터에서 모든 요청에는 AD RMS 로깅 데이터베이스 또는 Azure storage 계정에 기록 됩니다. MDE 로깅 AD RMS에서 사용 하 여 SQL Server에 두 개의 추가 테이블을 만들겠습니다: 클라이언트 로그 테이블과 클라이언트 성능 로그를 디버그 합니다.

**모바일 장치 확장 로깅을 사용 하도록 설정**

1.  AD RMS 서버에서 관리자 권한으로 Windows PowerShell을 엽니다.

2.  다음 명령 및 키를 눌러 입력 **Enter**: **Import-module AdRmsAdmin**

3.  다음 명령 및 키를 눌러 입력 **Enter**: **New-PSDrive -Name AdrmsCluster -PsProvider AdRmsAdmin -Root https://localhost**

4.  다음 명령 및 키를 눌러 입력 **Enter**: **Set-itemproperty-Path AdrmsCluster:\\ -IsLoggingEnabled 이름-값 \$true**

MDE 로깅 문제 해결을 사용 하는 경우에 문제를 해결 한 후 사용 하지 않도록 설정 하는 것이 좋습니다.

**모바일 장치 확장 로깅을 사용 하지 않으려면**

1.  AD RMS 서버에서 관리자 권한으로 Windows PowerShell을 엽니다.

2.  다음 명령 및 키를 눌러 입력 **Enter**: **Import-module AdRmsAdmin**

3.  다음 명령 및 키를 눌러 입력 **Enter**: **New-PSDrive -Name AdrmsCluster -PsProvider AdRmsAdmin -Root https://localhost**

4.  다음 명령 및 키를 눌러 입력 **Enter**: **Set-itemproperty-Path AdrmsCluster:\\ -IsLoggingEnabled 이름-값 \$false**

### <a name="upgrading-ad-rms-to-windows-server-2016"></a>AD RMS Windows Server 2016으로 업그레이드

다음 섹션에서는 현재 Windows Server 2012 R2 클러스터로 Windows Server 2016 기반 AD RMS 서버를 추가 하는 방법에 지침을 제공 합니다. 서버 클러스터에 추가 되 고 리소스 확보 하기 위해 이전 AD RMS 서버 중단 될 수 있도록 정보를 복제 됩니다.

AD RMS 클러스터에 추가 된 Windows Server 2016 기반 AD RMS 서버 하나를 추가 하면 이전 버전의 Windows 기반으로 하는 모든 노드 비활성화 됩니다. 이 작업이 완료 되 면 해당 서버 (예: 종료, 용도 변경 또는 AD RMS 클러스터에 가입 하도록 Windows Server 2016을 사용 하 여 다시 설치)를 프로 비전 해제할 수 있습니다. 

AD RMS 배포의 부하를 지원 하기 위해 클러스터에 추가 하는 AD RMS 서버를 배포할 수 있습니다. AD RMS 서버에 대 한 트래픽이 증가할된 경우이 작업을 수행할 수도 있습니다.

이 가이드는 부하 분산 사용 중단 된 서버를 제외 하 고 클러스터에 추가 하는 것을 포함 하려면 사용자 환경에서 사용할 수 있습니다 하는 메커니즘을 변경 하는 데 필요한 단계를 다루지 않습니다. 

#### <a name="adding-a-2016-ad-rms-server"></a>2016 AD RMS 서버를 추가합니다.

AD RMS 클러스터를 사용 중인 경우 하드웨어 보안 모듈을 중앙에서 관리 되는 키 대신 해당 서버 사용 허가자 인증서에 대 한 AD RMS를 설치 하기 전에 서버에서 소프트웨어 및 기타 HSM 아티팩트 (예: 키 및 구성 파일)를 설치 해야 합니다. 또한 서버에 물리적으로 또는 관련 네트워크 구성을 통해 HSM을 연결 해야 합니다. 다음이 단계에 대 한 HSM 지침에 따릅니다. 

**2016 AD RMS 서버를 추가 하려면**

1.  원하는 Windows Server 2016 배포에서 AD RMS 역할을 설치 합니다.

2.  설치가 완료 되 면 링크를 선택 **추가 구성 수행**합니다.

3.  선택 **기존 AD RMS 클러스터에 참여할** 누릅니다 **다음**합니다.

4.  에 **구성 데이터베이스 선택** 페이지에서 지정한 2016 SQL server (FQDN)에 대 한 DNS에서 CNAME을 입력 합니다.

5.  클릭 **목록을** 두 번째 줄에 선택 합니다 **DefaultInstance** 드롭다운 목록에서.

6.  아래 **구성 데이터베이스 이름은**, 드롭 다운 메뉴를 선택 하 고 표시 되는 DRM 구성을 선택 합니다. 그리고 **다음**을 클릭합니다.

7.  에 **데이터베이스 정보** 페이지에서 제공 된 필드에 클러스터 키 암호를 입력 합니다. 그런 다음 클릭 **다음**합니다.

8.  마법사의 다음 페이지에서 AD RMS 서비스 계정 지정에 대 한 암호를 제공 하 고 클릭 **다음** 확인 한 후입니다.

9.  한 번 합니다 **클러스터 웹 사이트** 단순히 적절 한 웹 사이트를 선택 했는지는 확인 페이지가 표시 되 고 클릭 **다음**합니다.

10. 에 **서버 인증 인증서 선택** 페이지에서 가져온된 SSL 인증서를 선택 하 고 클릭 **다음**합니다.

11. **설치**를 클릭하여 설치를 시작합니다.

12. 구성이 완료 된 후에 AD RMS를 관리 하려면 다시 로그인 해야 합니다.

13. 다시 로그온 시 엽니다 **서버 관리자** 선택 **도구** 차례로 **Active Directory Rights Management**합니다. 관리 창 표시 하 고 클러스터에 클러스터의 추가 서버를 지정 해야 합니다.

14. 원래 AD RMS 클러스터에서 AD RMS 모바일 장치 확장 설치 된 경우 업데이트 된 클러스터 노드에서 MDE에도 설치 해야 합니다. MDE AD RMS 클러스터에 추가할 MDE 문서의 지침을 따릅니다. 이 시점에서 모든 기존 노드를 용도 변경 또는 Windows Server 2016으로 업그레이드를 다시 위에서 설명한 동일한 프로세스를 사용 하 여 AD RMS 클러스터에 조인 합니다. 

### <a name="configuring-windows-server-2016-web-application-proxy-wap"></a>Windows Server 2016 웹 응용 프로그램 프록시 (WAP) 구성

다음 섹션에서는 웹 응용 프로그램 프록시 배포에 수행 해야 하는 운영 작업에 지침을 제공 합니다. 이것이 없어도 다음 경우에 게시 하는 AD RMS 인터넷 다른 메커니즘을 통해 단계는 선택 사항입니다. 

#### <a name="adding-a-windows-server-2016-wap-server"></a>Windows Server 2016 WAP 서버 추가

AD RMS 배포를 지원 하도록 추가 웹 응용 프로그램 프록시 서버를 배포할 수 있습니다. AD RMS 서버에 대 한 트래픽이 증가할된 또는 웹 응용 프로그램 프록시에 대 한 현재 사용 중인 서버 중 하나를 사용 중지 해야 하는 경우이 작업을 수행할 수 있습니다.

**2016 웹 응용 프로그램 프록시 서버를 추가 하려면**

1.  웹 응용 프로그램 프록시로 설치 하려는 서버에서 서버 관리자 콘솔로 이동 하 고 **역할 및 기능 추가**합니다.

2.  에 **역할 및 추가 기능 마법사**, 클릭 **다음** 하 여 서버 역할 선택 화면에 도달할 때까지 합니다.

3.  서버 역할 선택 화면에서 선택 **원격 액세스**를 클릭 하 고 **다음** 까지 서버 역할 선택 화면으로 돌아가게 됩니다.

4.  서버 역할 선택 화면에서 선택 **웹 응용 프로그램 프록시**, 클릭 **기능 추가**를 클릭 하 고 **다음**합니다.

5.  설치 선택 확인 화면에서 클릭 **설치**합니다.

6.  설치가 완료 되 면 클릭 **닫기**합니다.

7.  이제 서버를 구성 하는 시간입니다. 이렇게 하려면 웹 응용 프로그램 프록시 서버에서 원격 액세스 관리 콘솔을 엽니다. 엽니다는 **시작** 메뉴, 형식 **RAMgmtUI.exe**, 다음 응용 프로그램을 선택 합니다.

8.  탐색 창에서 클릭 **웹 응용 프로그램 프록시**합니다.

9.  원격 액세스 관리 콘솔에서 클릭 **웹 응용 프로그램 프록시 구성 마법사 실행**합니다. 마법사에서를 클릭 한 번 **다음**합니다.

10. 페더레이션 서버 화면 (구절 AD FS 서버의 정규화 된 도메인 이름 입력 adfs.contoso.com) 선택한 다음 AD FS 서버에서 관리자에 대 한 자격 증명을 입력 합니다.

11. AD FS Proxy 인증서 화면에서 현재 웹 응용 프로그램 프록시 서버에 설치 된 인증서 목록에서 AD FS 프록시에 대 한 웹 응용 프로그램 프록시에서 사용할 인증서를 선택한 다음 클릭 **다음**합니다.

12. 확인 화면에서 설정을 검토 한 다음 클릭 **구성**합니다.

13. 구성이 완료 되 면 클릭 **닫기**합니다.

#### <a name="dns-configuration-for-2016-wap-server"></a>2016에 대 한 DNS 구성을 WAP 서버

Windows Server 2016 웹 응용 프로그램 프록시 서버에 설정 되어, 후에 일부 DNS 변경 되도록 해야 합니다. 2016 WAP 서버에 ADFS를 가리키도록 GoDaddy와 같은 서비스 및 AD RMS 서비스를 사용 해야 합니다.

**DNS WAP 서버를 가리키도록**

1.  (예: 공급자의 웹 사이트로 이동 GoDaddy)입니다.

2.  도메인 관리 및 DNS 관리로 이동 합니다.

3.  ADFS 및 AD RMS 서비스를 찾을 수 있으며 바꿀 합니다 **가리킵니다** 2016 WAP 서버의 공용 IP 주소를 사용 하 여 부분 및 **저장**합니다.

4.  변경 내용을 전파 하는 데 시간이 걸릴 수 있습니다 하지만 그럴이 설치 프로그램 완료 됩니다.

#### <a name="enabling-debugging-logs"></a>디버깅 로그를 사용 하도록 설정

자세한 로깅 정보는 웹 응용 프로그램 프록시 서버에서 사용할 수 있습니다. 이벤트 뷰어를 사용 하 여 고급 디버깅 로깅을 구성할 수 있습니다. 또한 추가 설정은 분석 뷰어에 유용 하 게 하는 로그의 크기에 대 한 선택할 수 있습니다.

**웹 응용 프로그램 프록시에 대 한 디버깅 로그를 사용 하도록 설정**

1.  엽니다는 **이벤트 뷰어** Web Application Proxy에서 콘솔.

2.  확장 된 **Microsoft** 노드.

3.  확장 된 **Windows** 노드.

4.  엽니다는 **웹 응용 프로그램 프록시** 로그 합니다.

5.  그런 다음 열 수 있습니다 합니다 **관리자** 로그 합니다.

6.  엽니다는 **작업** 메뉴에서 맨 왼쪽에 있는 선택한 **속성**합니다.

7.  아래는 **일반적인** 탭에서 옵션을 선택 **로깅을**합니다.

8.  마지막으로, 최대 로그 크기 및 최대 이벤트 로그 크기에 도달 하는 경우 사용자 지정할 수 있습니다.

### <a name="configuring-high-availability-for-windows-server-2016-services"></a>Windows Server 2016 서비스에 대 한 고가용성 구성

다음 섹션에서 고가용성 Windows Server 2016 환경을 설정 해야 하는 운영 작업에 지침을 제공 합니다.

#### <a name="adding-a-2016-ad-rms-server-for-high-availability"></a>고가용성에 대 한 2016 AD RMS 서버를 추가합니다.

추가 AD RMS 서버 고가용성 설치를 배포할 수 있습니다. AD RMS 서버에 대 한 트래픽이 증가할된 경우이 작업을 수행할 수 있습니다.

**고가용성에 대 한 2016 AD RMS 서버를 추가 하려면**

1.  원하는 Windows Server 2016 배포에서 AD RMS 역할을 설치 합니다.

2.  설치가 완료 되 면 링크를 선택 **추가 구성 수행**합니다.

3.  선택 **기존 AD RMS 클러스터에 참여할** 누릅니다 **다음**합니다.

4.  에 **구성 데이터베이스 선택** 페이지에서 지정한 2016 SQL server (FQDN)에 대 한 DNS에서 CNAME을 입력 합니다.

5.  클릭 **목록을** 두 번째 줄에 선택 합니다 **DefaultInstance** 드롭다운 목록에서.

6.  아래 **구성 데이터베이스 이름은**, 드롭 다운 메뉴를 선택 하 고 표시 되는 DRM 구성을 선택 합니다. 그리고 **다음**을 클릭합니다.

7.  에 **데이터베이스 정보** 페이지에서 제공 된 필드에 클러스터 키 암호를 입력 합니다. 그런 다음 클릭 **다음**합니다.

8.  마법사의 다음 페이지에서 AD RMS 서비스 계정 지정에 대 한 암호를 제공 하 고 클릭 **다음** 확인 한 후입니다.

9.  한 번 합니다 **클러스터 웹 사이트** 단순히 적절 한 웹 사이트를 선택 했는지는 확인 페이지가 표시 되 고 클릭 **다음**합니다.

10. 에 **서버 인증 인증서 선택** 페이지에서 가져온된 SSL 인증서를 선택 하 고 클릭 **다음**합니다.

11. **설치**를 클릭하여 설치를 시작합니다.

12. 구성이 완료 된 후에 AD RMS를 관리 하려면 다시 로그인 해야 합니다.

13. 다시 로그온 시 엽니다 **서버 관리자** 선택 **도구** 차례로 **Active Directory Rights Management**합니다. 관리 창 표시 하 고 클러스터에 클러스터의 추가 서버를 지정 해야 합니다.

14. 서버 설치를 확인 한 후 클러스터의 서로 다른 AD RMS 서버 간에 부하를 분산 하 여 부하 분산 서비스를 구성 합니다.

#### <a name="adding-a-windows-server-2016-ad-fs-server-for-high-availability"></a>고가용성을 위해 Windows Server 2016 AD FS 서버 추가

고가용성을 설정 하려면 추가 AD FS 서버를 배포할 수 있습니다. AD FS 서버에 대 한 트래픽이 증가할된 경우이 작업을 수행할 수 있습니다. **참고: 팜 동작 수준을 발생 시킨 후 새 database 항목이 입력 됩니다 (Adfs Configv3)의 SQL Server 2016으로 하 고이 단계를 진행 하기 전에 기존 구성 데이터베이스를 삭제 해야 합니다.**

**고가용성을 위해 Windows Server 2016 AD FS 서버를 추가 하려면**

1.  원하는 Windows Server 2016 배포에서 AD RMS 역할을 설치 합니다.

2.  설치가 완료 되 면 링크를 선택 **이 서버에 페더레이션 서비스 구성**합니다.

3.  마법사의 시작 섹션에서 옵션을 선택 **페더레이션 서버 팜에 페더레이션 서버 추가** 을 클릭 한 다음 **다음**합니다.

4.  적절 한 관리자 계정을 지정 하 고 클릭 **다음**합니다.

5.  에 **팜 지정** 페이지에서 선택 합니다 **SQL Server를 사용 하 여 기존 팜에 데이터베이스 위치를 지정** 그런 다음 데이터베이스 호스트 이름에 대 한 SQL 서비스에 대 한 CNAME을 입력 하 고 클릭 **다음**.

6.  아래는 **서비스 계정 지정** 영역 마법사의 AD FS 서비스 계정에 대 한 자격 증명을 입력 한 다음 클릭 **다음**합니다.

7.  **옵션 검토**, 클릭 **다음**합니다.

8.  클릭 **구성** 때 단추를 사용할 수 있습니다.

9.  구성 후 컴퓨터를 다시 시작 합니다.

10. 부하 분산 서버 설치를 필요에 따라 AD FS 서버를 확인 합니다.

#### <a name="adding-a-windows-server-2016-wap-server-for-high-availability"></a>고가용성을 위해 Windows Server 2016 WAP 서버 추가

고가용성을 설정 하려면 추가 WAP 서버를 배포할 수 있습니다. AD RMS 서버에 대 한 트래픽이 증가할된 경우이 작업을 수행할 수 있습니다.

**고가용성을 위해 Windows Server 2016 웹 응용 프로그램 프록시 서버를 추가 하려면**

1.  웹 응용 프로그램 프록시로 설치 하려는 서버에서 서버 관리자 콘솔로 이동 하 고 **역할 및 기능 추가**합니다.

2.  에 **역할 및 추가 기능 마법사**, 클릭 **다음** 하 여 서버 역할 선택 화면에 도달할 때까지 합니다.

3.  서버 역할 선택 화면에서 선택 **원격 액세스**를 클릭 하 고 **다음** 까지 서버 역할 선택 화면으로 돌아가게 됩니다.

4.  서버 역할 선택 화면에서 선택 **웹 응용 프로그램 프록시**, 클릭 **기능 추가**를 클릭 하 고 **다음**합니다.

5.  설치 선택 확인 화면에서 클릭 **설치**합니다.

6.  설치가 완료 되 면 클릭 **닫기**합니다.

7.  이제 서버를 구성 하는 시간입니다. 이렇게 하려면 웹 응용 프로그램 프록시 서버에서 원격 액세스 관리 콘솔을 엽니다. 엽니다는 **시작** 메뉴, 형식 **RAMgmtUI.exe**, 다음 응용 프로그램을 선택 합니다.

8.  탐색 창에서 클릭 **웹 응용 프로그램 프록시**합니다.

9.  원격 액세스 관리 콘솔에서 클릭 **웹 응용 프로그램 프록시 구성 마법사 실행**합니다. 마법사에서를 클릭 한 번 **다음**합니다.

10. 페더레이션 서버 화면 (구절 AD FS 서버의 정규화 된 도메인 이름 입력 adfs.contoso.com) 선택한 다음 AD FS 서버에서 관리자에 대 한 자격 증명을 입력 합니다.

11. AD FS Proxy 인증서 화면에서 현재 웹 응용 프로그램 프록시 서버에 설치 된 인증서 목록에서 AD FS 프록시에 대 한 웹 응용 프로그램 프록시에서 사용할 인증서를 선택한 다음 클릭 **다음**합니다.

12. 확인 화면에서 설정을 검토 한 다음 클릭 **구성**합니다.

13. 구성이 완료 되 면 클릭 **닫기**합니다.

14. 서버 설치를 확인 한 후 dmz에서 WAP 서버의 부하를 분산 합니다.

#### <a name="adding-a-sql-server-2016-node-for-always-on-high-availability"></a>Always On 고가용성에 대 한 SQL Server 2016 노드를 추가합니다.

추가 SQL server Always On 고가용성 설치 프로그램을 배포할 수 있습니다. AD RMS 서버에 대 한 트래픽이 증가할된 경우이 작업을 수행할 수 있습니다. **참고: 두 SQL Server 인바운드 포트 5022 열려 있는지 확인 하십시오.**

**Always On 고가용성에 대 한 SQL server 2016 서버를 추가 하려면**

1.  추가 SQL Server 2016 서버로 설치 하려는 서버에서 서버 관리자 콘솔로 이동 하 고 **역할 및 기능 추가**합니다.

2.  클릭 **다음** 때까지 합니다 **기능 선택** 대화 상자.

3.  선택 된 **장애 조치 클러스터링** 확인란을 선택 합니다. **참고: 두 SQL Server 장애 조치 클러스터링 기능 갖도록도 원래 SQL server 2016 서버에 대해이 단계를 따릅니다.**

4.  클릭 **설치** 장애 조치 클러스터링 기능을 설치 합니다.

5.  이제을 엽니다 **서버 관리자** 선택한 **도구** 한 다음 **장애 조치 클러스터 관리자**합니다.

6.  왼쪽된 메뉴 창에서 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자** 선택한 **클러스터 만들기**

7.  열립니다는 **클러스터 만들기 마법사**합니다.

8.  Always On 고가용성에 대 한을 사용 하 고 클릭 한 다음에 입력 하는 SQL server 2016 서버에 대 한 찾아보기 **다음**합니다.

9.  유효성 검사 경고를 받게 됩니다. 선택 **Yes** 클러스터 노드의 유효성을 검사 한 다음 클릭 **다음**합니다.

10. 아래는 **테스트 옵션** 페이지에서 옵션을 선택 **모든 테스트를 실행** 를 클릭 하 고 **다음입니다.**

11. **참고: 클러스터 유효성 검사 마법사를 사용 하지 않는 공유 저장소 하는 경우에 특히 여러 경고 메시지가 반환 예정입니다. 이외에 모든 오류 메시지를 찾을 경우 수정 해야 하는 Windows Server 장애 조치 클러스터를 만들기 전에**입니다.

12. 에 **클러스터 관리 액세스 지점** 대화 상자에서 Windows Server 장애 조치 클러스터에 대 한 클러스터 이름과 가상 IP 주소를 입력 한 다음 클릭 **다음**합니다.

13. 구성에 성공 했는지 확인 **요약** 누릅니다 **마침**합니다.

14. 에 **장애 조치 클러스터 관리자** 선택한 서버 클러스터를 마우스 오른쪽 단추로 클릭 **기타 작업** 선택한 **클러스터 쿼럼 설정 구성**

15. 클릭 **다음** 에 대 한 옵션을 선택 하 고 **쿼럼 감시 선택** 누릅니다 **다음** 다시 합니다.

16. 에 **쿼럼 감시 선택** 페이지에서 선택 합니다 **파일 공유 감시 구성** 옵션. 그리고 **다음**을 클릭합니다.

17. 선택 **찾아보기** 파일 공유 경로 대화 상자에서 사용 하려는 파일 공유의 경로 찾습니다. **다음**을 클릭합니다.

18. 확인 페이지에서 클릭 **다음**합니다.

19. 요약 페이지에서 클릭 **완료**합니다.

20. 이제 엽니다는 **시작** 메뉴 및 검색 **SQL Server 구성 관리자**합니다.

21. SQL Server 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.

22. 속성 대화 상자에서 선택 합니다 **AlwaysOn 고가용성** 탭 합니다. 확인 합니다 **AlwaysOn 가용성 그룹 사용** 확인란 합니다. **확인**을 클릭합니다. **참고:이 작업을 수행할 두 SQL server 2016 서버.**

23. SQL Server 서비스를 다시 시작 합니다.

24. 이제 엽니다는 **시작** 메뉴 및 검색 **SQL Server Management Studio** 왼쪽된 탐색 창에서 마우스 오른쪽 단추로 클릭 하 고 **가용성 그룹** 클릭**새 가용성 그룹 마법사** 클릭 **다음**합니다.

25. 에 **가용성 그룹 이름 지정** 페이지 그룹 이름 (Ex.SQLAvailabilityGroup2016)를 선택 합니다. 그리고 **다음**을 클릭합니다.

26. 아래는 **데이터베이스 선택** 섹션, 데이터베이스를 지정 합니다. 그런 후 "다음"을 클릭합니다. **참고: 일부 데이터베이스를 다시 백업 또는 전체 복구 모드로 설정 해야**합니다.

27. 두 번를 **복제본 지정** 페이지를 클릭 합니다 **복제본 추가** 단추 및 다른 2016 SQL Server를 선택 합니다.

28. 다른 서버를 추가한 후 확인란을 클릭 하 고 보조 서버는 읽기 가능한 보조 복제본 수를 설정 합니다.

29. 로 이동 합니다 **끝점** 탭을 클릭 합니다 **새로 고침** 옵션입니다. 여기서도 하는 동안 스크롤 및 기본 및 보조 노드에서 동일한 서비스 계정 인지 확인 합니다.

30. 이제 선택는 **백업 기본 설정** 탭을 선택 합니다 **보조 선호** 옵션입니다.

31. 로 이동 합니다 **수신기** 탭 합니다.

32. 지정 된 이름 (예: SQLListener) 포트 인지 확인 **1433** 을 클릭 한 다음 **다음**합니다.

33. 에 **초기 데이터 동기화 선택** 페이지 마법사의 선택 합니다 **전체** 옵션을 모든 SQL 서버에서 액세스할 수 있는 네트워크 위치를 지정 하 고 클릭 **다음**.

34. 마지막으로, 클릭 **완료** 프로세스가 완료 됩니다.

### <a name="decommission-windows-server-2012-r2-nodes"></a>Windows Server 2012 R2 노드를 서비스 해제

다음 섹션에서는 성공적으로 AD RMS 클러스터를 Windows Server 2016으로 업그레이드 한 후 Windows Server 2012 R2 서버를 제거 해야 하는 운영 작업에 지침을 제공 합니다.

#### <a name="removing-a-windows-server-2012-r2-ad-rms-server"></a>Windows Server 2012 R2 AD RMS 서버를 제거합니다.

업그레이드 후 불필요 한 AD RMS 서버를 제거할 수 있습니다. AD RMS 서버를 서비스 해제가 필요할 경우이 작업을 수행할 수 있습니다.

**제거 하는** **Windows Server 2012 R2 AD RMS 서버**

1.  Windows Server 2012 R2 AD RMS 서버에서 서버 관리자에서 선택 **관리** 위에서 메뉴를 마우스 오른쪽 단추로 선택한 후 **역할 및 기능 제거**합니다.

2.  **제거 역할 및 기능 마법사** 등록 한 열립니다는 **시작 하기 전에** 화면을 클릭 **다음**.

3.  에 **서버 선택** 화면에서 클릭 **다음**합니다.

4.  에 **서버 역할** 화면에서 옆에 확인 제거 **Active Directory Rights Management Services** 클릭 **다음**합니다.

5.  에 **기능** 화면에서 클릭 **다음**합니다.

6.  에 **확인** 화면에서 클릭 **제거**합니다.

7.  이 완료 되 면 서버를 다시 시작 합니다.

8.  이제이 서버를 종료 하 고 필요에 따라 리소스를 다시 할당할 수 있습니다.
