---
title: Windows Server 2019 Standard Edition과 Datacenter Edition의 비교
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: c5ca3bfe-7ced-49f6-2932-80cab33fe914
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 2cb368b5ff4723c1afb53c5a9e787d9f8a39bef3
ms.sourcegitcommit: 40e4ba214954d198936341c4d6ce1916dc891169
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72690453"
---
# <a name="comparison-of-standard-and-datacenter-editions-of-windows-server-2019"></a>Windows Server 2019 Standard Edition과 Datacenter Edition의 비교

> 적용 대상: Windows Server 2019
  
## <a name="locks-and-limits"></a>잠금 및 제한

| 잠금 및 제한                 | Windows Server 2019 Standard | Windows Server 2019 Datacenter |  
| -------------------              | ---------------------------  | --------------------------- |  
| 최대 사용자 수          | CAL 기준                | CAL 기준 |
| 최대 SMB 연결 수          | 16,777,216                   | 16,777,216 |
| 최대 RRAS 연결 수         | 제한 없음                    | 제한 없음 |
| 최대 IAS 연결 수          | 2,147,483,647                | 2,147,483,647 |
| 최대 RDS 연결 수:          | 65,535                       | 65,535 |
| 64비트 소켓 최대 수 | 64                           | 64 |
| 최대 코어 수          | 제한 없음                    | 제한 없음 |
| 최대 RAM                      | 24TB                        | 24TB |
| 가상화 게스트로 이용 가능 여부 | 예(두 대의 가상 컴퓨터 및 라이선스당 하나의 Hyper-V 호스트)|예(<strong>무제한 가상 머신</strong>, 라이선스당 하나의 Hyper-V 호스트) |
| 서버의 도메인 가입 가능 여부        | 예                           | 예 |
| 경계 네트워크 보호/방화벽| 아니요                            | 아니요    |
| DirectAccess                    | 예                           | 예 |
| DLNA 코덱 및 웹 미디어 스트리밍 | 예(데스크톱 환경 포함 서버로 설치된 경우) | 예(데스크톱 환경 포함 서버로 설치된 경우) |

## <a name="server-roles"></a>서버 역할

|사용 가능한 Windows Server 역할|역할 서비스|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|----------|---------------------------|  
|Active Directory 인증서 서비스| |예|예|
|Active Directory 도메인 서비스| |예|예|
|AD FS(Active Directory Federation Services)| |예|예|
|AD LDS(Lightweight Directory Services)| |예|예|
|AD Rights Management Services| |예|예|
|디바이스 상태 증명| |예|예|
|DHCP 서버| |예|예|
|DNS 서버| |예|예|
|팩스 서버| |예|예|
|파일 및 저장소 서비스|파일 서버|예|예|
|파일 및 저장소 서비스|네트워크 파일용 BranchCache|예|예|
|파일 및 저장소 서비스|데이터 중복 제거|예|예|
|파일 및 저장소 서비스|DFS 네임스페이스|예|예|
|파일 및 저장소 서비스|DFS 복제|예|예|
|파일 및 저장소 서비스|파일 서버 리소스 관리자|예|예|
|파일 및 저장소 서비스|파일 서버 VSS 에이전트 서비스|예|예|
|파일 및 저장소 서비스|iSCSI 대상 서버|예|예|
|파일 및 저장소 서비스|iSCSI 대상 저장소 공급자|예|예|
|파일 및 저장소 서비스|NFS용 서버|예|예|
|파일 및 저장소 서비스|클라우드 폴더|예|예|
|파일 및 저장소 서비스|저장소 서비스|예|예|
|호스트 보호 서비스| |예|예|
|Hyper-V| |예|예(보호된 가상 컴퓨터 포함)|
|네트워크 컨트롤러| |아니오| <strong>예</strong> |
|네트워크 정책 및 액세스 서비스| |예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|인쇄 및 문서 서비스| |예|예|
|원격 액세스| |예|예|
|원격 데스크톱 서비스| |예|예|
|볼륨 정품 인증 서비스| |예|예|
|Web Services(IIS)| |예|예|
|Windows 배포 서비스| |예*|예*|
|Windows Server 필수 패키지 환경| |아니오 | 아니오 |
|Windows Server Update Services| |예|예|

*WDS 전송 서버는 Windows Server 2019에서 Server Core 설치에 새로운 기능입니다(Windows Server, 버전 1803부터 반기 채널에서도).


## <a name="features"></a>기능

|Windows Server 기능(서버 관리자 또는 PowerShell을 사용하여 설치 가능)|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|---------------------------|  
|.NET Framework 3.5 |예|예|
|.NET Framework 4.7 |예|예|
|BITS(Background Intelligent Transfer Service)|예|예|
|BitLocker 드라이브 암호화|예|예|
|BitLocker 네트워크 잠금 해제|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|BranchCache|예|예|
|NFS용 클라이언트|예|예|
|컨테이너|예(무제한 Windows 컨테이너, Hyper-V 컨테이너 최대 2개)|예(<strong>무제한 Windows 컨테이너 및 Hyper-V 컨테이너</strong>) |
|데이터 센터 브리징|예|예|
|DirectPlay|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|강화된 저장소|예|예|
|장애 조치(failover) 클러스터링|예|예|
|그룹 정책 관리|예|예|
|호스트 보호 Hyper-V 지원|아니오| <strong>예</strong> |
|I/O 서비스 품질|예|예|
|IIS 호스팅 가능한 웹 코어|예|예|
|인터넷 인쇄 클라이언트|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|IPAM 서버|예|예|
|iSNS 서버 서비스|예|예|
|LPR 포트 모니터|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|관리 OData IIS 확장|예|예|
|미디어 파운데이션|예|예|
|메시지 큐|예|예|
|다중 경로 I/O|예|예|
|MultiPoint 커넥터|예|예|
|네트워크 부하 분산|예|예|
|피어 이름 확인 프로토콜|예|예|
|qWave(Quality Windows Audio Video Experience)|예|예|
|RAS 연결 관리자 관리 키트|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|원격 지원|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|원격 차등 압축|예|예|
|RSAT|예|예|
|RPC over HTTP 프록시|예|예|
|이벤트 컬렉션 설치 및 부팅|예|예|
|단순 TCP/IP 서비스|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|SMB 1.0/CIFS 파일 공유 지원|설치됨|설치됨|
|SMB 대역폭 제한|예|예|
|SMTP 서버|예|예|
|SNMP 서비스|예|예|
|소프트웨어 부하 분산 장치|예|예|
|저장소 복제본|예|예|
|텔넷 클라이언트|예|예|
|TFTP 클라이언트|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|패브릭 관리를 위한 VM 보호 도구|예|예|
|WebDAV 리디렉터|예|예|
|Windows 생체 인식 프레임워크|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|Windows Defender 기능|설치됨|설치됨|
|Windows Identity Foundation 3.5|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|Windows 내부 데이터베이스|예|예|
|Windows PowerShell|설치됨|설치됨|
|Windows Process Activation Service|예|예|
|Windows Search Service|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|Windows Server 백업|예|예|
|Windows Server 마이그레이션 도구|예|예|
|Windows 표준 기반 저장소 관리|예|예|
|Windows TIFF IFilter|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|
|WinRM IIS 확장|예|예|
|WINS 서버|예|예|
|무선 LAN 서비스|예|예|
|WoW64 지원|설치됨|설치됨|
|XPS 뷰어|예(데스크톱 환경 포함 서버로 설치된 경우)|예(데스크톱 환경 포함 서버로 설치된 경우)|

|일반적으로 사용 가능한 기능|Windows Server 2019 Standard|Windows Server 2019 Datacenter|  
|-------------------|----------|---------------------------|  
|모범 사례 분석기|예|예|
|직접 액세스|예|예|
|동적 메모리(가상화의 경우)|예|예|
|Hot Add/Replace RAM|예|예|
|Microsoft Management Console|예|예|
|최소 서버 인터페이스|예|예|
|네트워크 부하 분산|예|예|
|Windows PowerShell|예|예|
|Server Core 설치 옵션|예|예|
|서버 관리자|예|예|
|SMB 다이렉트 및 SMB over RDMA|예|예|
|소프트웨어 정의 네트워킹|아니오| <strong>예</strong> |
|스토리지 마이그레이션 서비스|예|예|
| 저장소 복제본         | 예(하나의 파트너 관계 및 단일 2TB 볼륨이 포함된 하나의 리소스 그룹)    | 예(<strong>제한 없음</strong>) |
|저장소 공간|예|예|
|저장소 공간 다이렉트|아니오| <strong>예</strong> |
|볼륨 정품 인증 서비스|예|예|
|VSS (Volume Shadow Copy Service) integration|예|예|
|Windows Server Update Services|예|예|
|Windows 시스템 리소스 관리자|예|예|
|서버 라이선싱 로깅|예|예|
|활성화 상속|데이터센터에서 호스트된 경우 게스트로 가능| <strong>호스트 또는 게스트가 될 수 있음</strong> |
|클라우드 폴더|예|예|
