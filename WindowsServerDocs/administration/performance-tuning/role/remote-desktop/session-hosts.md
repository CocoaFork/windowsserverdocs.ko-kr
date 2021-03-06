---
title: 원격 데스크톱 세션 호스트 성능 조정
description: 원격 데스크톱 세션 호스트에 대 한 성능 조정 지침
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS; DenisGun
author: phstee
ms.date: 10/22/2019
ms.openlocfilehash: b439b0cbab66f98a1f74faeb7bff996b30a188d5
ms.sourcegitcommit: 3262c5c7cece9f2adf2b56f06b7ead38754a451c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72812334"
---
# <a name="performance-tuning-remote-desktop-session-hosts"></a>원격 데스크톱 세션 호스트 성능 조정


이 항목에서는 원격 데스크톱 세션 호스트 (RD 세션 호스트) 하드웨어를 선택 하 고, 호스트를 튜닝 하 고, 응용 프로그램을 튜닝 하는 방법을 설명 합니다.

**항목 내용**

-   [성능을 위한 적절 한 하드웨어 선택](#selecting-the-proper-hardware-for-performance)

-   [원격 데스크톱 세션 호스트에 대 한 응용 프로그램 조정](#tuning-applications-for-remote-desktop-session-host)

-   [원격 데스크톱 세션 호스트 튜닝 매개 변수](#remote-desktop-session-host-tuning-parameters)

## <a name="selecting-the-proper-hardware-for-performance"></a>성능에 맞는 적절한 하드웨어 선택


RD 세션 호스트 서버 배포의 경우 선택 하는 하드웨어는 응용 프로그램 집합 및 사용자가 사용 하는 방법에 따라 결정 됩니다. 사용자 수 및 해당 환경에 영향을 주는 주요 요소는 CPU, 메모리, 디스크 및 그래픽입니다. 이 섹션에서는 RD 세션 호스트 서버와 관련 된 추가 지침을 포함 하며 대부분의 RD 세션 호스트 서버에 대 한 다중 사용자 환경과 관련이 있습니다.

### <a name="cpu-configuration"></a>CPU 구성

CPU 구성은 개념적으로 시스템에서 지원 해야 하는 세션 수에 따라 세션을 지 원하는 데 필요한 CPU를 곱하여 결정 되며, 임시 급증을 처리 하기 위해 버퍼 영역을 유지 합니다. 여러 논리 프로세서를 통해 비정상적인 CPU 정체 상황을 줄일 수 있습니다 .이는 일반적으로 유사한 수의 논리적 프로세서에 포함 된 몇 개의 오버 활성 스레드로 인해 발생 합니다.

따라서 시스템에서 논리적 프로세서 수가 많을 수록 CPU 사용량에 따라 기본 설정 되어야 하는 나머지 부분 여백을 낮춰 CPU 당 활성 부하의 비율이 커집니다. 기억해 야 할 중요 한 요소는 Cpu 수를 두 배로 늘리면 CPU 용량이 배가 되지 않는다는 것입니다.

### <a name="memory-configuration"></a>메모리 구성

메모리 구성은 사용자가 사용 하는 응용 프로그램에 따라 달라 집니다. 그러나 필요한 메모리 양은 다음 수식을 사용 하 여 예상할 수 있습니다. TotalMem = OSMem + SessionMem \* NS

OSMem은 운영 체제에서 실행 하는 데 필요한 메모리의 양 (예: 시스템 이진 이미지, 데이터 구조 등)이 고, SessionMem은 한 세션에서 실행 되는 메모리 프로세스의 양과 NS는 활성 세션의 대상 수입니다. 세션에 필요한 메모리 양은 주로 세션 내에서 실행 되는 응용 프로그램 및 시스템 프로세스의 전용 메모리 참조 집합에 의해 결정 됩니다. 공유 코드 또는 데이터 페이지는 시스템에 복사본이 하나만 있으므로 효과가 거의 없습니다.

페이지 파일을 백업 하는 디스크 시스템이 변경 되지 않는다고 가정 하는 한 가지 흥미로운 관찰은 시스템에서 지원 해야 하는 동시 활성 세션 수가 많을 수록 세션당 메모리 할당이 더 크다는 것입니다. 세션당 할당 된 메모리 양이 증가 하지 않는 경우 활성 세션에서 생성 하는 페이지 폴트 수가 세션 수와 함께 증가 합니다. 이러한 오류는 궁극적으로 i/o 하위 시스템에 과부하가 걸려 있습니다. 세션당 할당 된 메모리 양을 늘려서 페이지 폴트 발생 가능성이 감소 하 여 페이지 폴트의 전체 요금을 줄일 수 있습니다.

### <a name="disk-configuration"></a>디스크 구성

저장소는 RD 세션 호스트 서버를 구성할 때 가장 간과 되는 측면 중 하나 이며, 필드에 배포 된 시스템에서 가장 일반적인 제한이 될 수 있습니다.

일반적인 RD 세션 호스트 서버에서 생성 되는 디스크 작업은 다음 영역에 영향을 줍니다.

-   시스템 파일 및 응용 프로그램 이진 파일

-   페이지 파일

-   사용자 프로필 및 사용자 데이터

이상적으로 이러한 영역은 고유한 저장소 장치에 의해 백업 되어야 합니다. 스트라이프 RAID 구성 또는 다른 유형의 고성능 저장소를 사용 하면 성능이 더욱 향상 됩니다. 배터리 지원 쓰기 캐싱에 저장소 어댑터를 사용 하는 것이 좋습니다. 디스크 쓰기 캐싱이 있는 컨트롤러는 동기 쓰기 작업에 대 한 향상 된 지원을 제공 합니다. 모든 사용자에 게 별도의 hive가 있기 때문에 RD 세션 호스트 서버에서 동기 쓰기 작업이 훨씬 더 일반적입니다. 레지스트리 하이브는 동기 쓰기 작업을 사용 하 여 주기적으로 디스크에 저장 됩니다. 이러한 최적화를 사용 하도록 설정 하려면 디스크 관리 콘솔에서 대상 디스크에 대 한 **속성** 대화 상자를 열고 **정책** 탭에서 **디스크에 쓰기 캐싱 사용** 및 **Windows 쓰기 캐시 버퍼 끄기를 선택 합니다.** 장치 확인란을 플러시합니다.

### <a name="network-configuration"></a>네트워크 구성

RD 세션 호스트 서버에 대 한 네트워크 사용에는 다음과 같은 두 가지 주요 범주가 있습니다.

-   연결 트래픽 사용은 세션 내에서 실행 되는 응용 프로그램에서 나타나는 그리기 패턴 및 리디렉션된 장치 i/o 트래픽에 의해 거의 독점적으로 결정 됩니다. RD 세션 호스트

    예를 들어 텍스트 처리 및 데이터 입력을 처리 하는 응용 프로그램은 초당 약 10-100 킬로 비트의 대역폭을 사용 하는 반면, 리치 그래픽과 비디오 재생을 수행 하면 대역폭 사용량이 크게 증가 합니다.

-   로밍 프로필, 파일 공유에 대 한 응용 프로그램 액세스, 데이터베이스 서버, 전자 메일 서버 및 HTTP 서버와 같은 백 엔드 연결

    네트워크 트래픽의 볼륨과 프로필은 각 배포에만 적용 됩니다.

## <a name="tuning-applications-for-remote-desktop-session-host"></a>원격 데스크톱 세션 호스트에 대 한 응용 프로그램 조정


RD 세션 호스트 서버에서 대부분의 CPU 사용량은 앱을 기반으로 합니다. 데스크톱 앱은 일반적으로 응용 프로그램이 사용자 요청에 응답 하는 데 걸리는 시간을 최소화 하는 목표로 응답성에 최적화 됩니다. 그러나 서버 환경에서는 다른 세션에 부정적인 영향을 주지 않도록 작업을 완료 하는 데 필요한 총 CPU 사용량을 최소화 하는 것이 중요 합니다.

RD 세션 호스트 서버에서 사용할 앱을 구성 하는 경우 다음 제안 사항을 고려 하십시오.

-   백그라운드 유휴 루프 처리 최소화

    일반적인 예는 백그라운드 문법 및 맞춤법 검사, 검색을 위한 데이터 인덱싱 및 백그라운드 저장을 사용 하지 않도록 설정 하는 것입니다.

-   앱에서 상태 확인 또는 업데이트를 수행 하는 빈도를 최소화 합니다.

    이러한 동작을 사용 하지 않도록 설정 하거나 폴링 반복과 타이머 발생 간격을 증가 시키면 많은 활성 세션에서 이러한 활동의 영향이 빠르게 증폭 되기 때문에 CPU 사용량이 크게 향상 됩니다. 일반적인 예는 연결 상태 아이콘 및 상태 표시줄 정보 업데이트입니다.

-   동기화 빈도를 줄여 앱 간의 리소스 경합을 최소화 합니다.

    이러한 리소스의 예로는 레지스트리 키와 구성 파일이 있습니다. 응용 프로그램 구성 요소 및 기능의 예로는 상태 표시기 (예: 셸 알림), 백그라운드 인덱싱 또는 변경 모니터링, 오프 라인 동기화가 있습니다.

-   사용자 로그인 또는 세션 시작으로 시작 하도록 등록 된 불필요 한 프로세스를 사용 하지 않도록 설정 합니다.

    이러한 프로세스는 일반적으로 CPU를 많이 사용 하는 프로세스 이며, 아침 시나리오에서 매우 비용이 많이 들 수 있습니다. Msconfig.exe 또는 xsd.exe를 사용 하 여 사용자 로그인 시 시작 되는 프로세스 목록을 가져옵니다. 자세한 내용은 [autoruns.exe For Windows](https://technet.microsoft.com/sysinternals/bb963902.aspx)를 사용할 수 있습니다.

메모리 사용의 경우 다음 사항을 고려해 야 합니다.

-   앱에 의해 로드 된 Dll이 재배치 되지 않는지 확인 합니다.

    -   다음 그림에 표시 된 것 처럼 프로세스 [탐색기](https://technet.microsoft.com/sysinternals/bb896653.aspx)를 사용 하 여 Dll 뷰 처리를 선택 하 여 재배치 된 dll을 확인할 수 있습니다.

    -   여기에서 x .dll은 이미 기본 기준 주소를 사용 하 고 ASLR을 사용 하도록 설정 하지 않았기 때문에 y .dll이 재배치 된 것을 볼 수 있습니다.

        ![재배치 한 dll](../../media/perftune-guide-relocated-dlls.png)

        Dll을 재배치 하는 경우 세션 간에 코드를 공유 하는 것이 불가능 하므로 세션의 공간이 크게 증가 합니다. 이는 RD 세션 호스트 서버에서 발생 하는 가장 일반적인 메모리 관련 성능 문제 중 하나입니다.

-   CLR (공용 언어 런타임) 응용 프로그램의 경우 네이티브 이미지 생성기 (Ngen.exe)를 사용 하 여 페이지 공유를 늘리고 CPU 오버 헤드를 줄입니다.

    가능한 경우 다른 유사한 실행 엔진에 비슷한 기술을 적용 합니다.

## <a name="remote-desktop-session-host-tuning-parameters"></a>원격 데스크톱 세션 호스트 튜닝 매개 변수


### <a name="page-file"></a>페이지 파일

페이지 파일 크기가 충분 하지 않으면 응용 프로그램 또는 시스템 구성 요소에서 메모리 할당 오류가 발생할 수 있습니다. 메모리에서 커밋된 바이트 성능 카운터를 사용 하 여 시스템에 커밋된 가상 메모리 양을 모니터링할 수 있습니다.

### <a name="antivirus"></a>바이러스 백신

RD 세션 호스트 서버에 바이러스 백신 소프트웨어를 설치 하면 전반적인 시스템 성능, 특히 CPU 사용량이 크게 영향을 받습니다. 임시 파일을 포함 하는 모든 폴더, 특히 서비스 및 기타 시스템 구성 요소가 생성 하는 모든 폴더를 활성 모니터링 목록에서 제외 하는 것이 좋습니다.

### <a name="task-scheduler"></a>작업 스케줄러

작업 스케줄러를 사용 하 여 다른 이벤트에 대해 예약 된 작업 목록을 검토할 수 있습니다. RD 세션 호스트 서버의 경우 유휴 상태, 사용자 로그인 시 또는 세션 연결 및 연결 해제 시 실행 되도록 구성 된 작업에 특히 집중 하는 것이 유용 합니다. 배포의 세부 사항 때문에 이러한 작업은 대부분 필요 하지 않을 수 있습니다.

### <a name="desktop-notification-icons"></a>바탕 화면 알림 아이콘

바탕 화면의 알림 아이콘은 매우 저렴 한 새로 고침 메커니즘이 있을 수 있습니다. 시작 목록에서 등록 하는 구성 요소를 제거 하거나 앱 및 시스템 구성 요소의 구성을 변경 하 여 사용 하지 않도록 설정 하 여 알림을 사용 하지 않도록 설정 해야 합니다. **알림 사용자 지정 아이콘** 을 사용 하 여 서버에서 사용할 수 있는 알림 목록을 검사할 수 있습니다.

### <a name="remote-desktop-protocol-data-compression"></a>원격 데스크톱 프로토콜 데이터 압축

원격 데스크톱 프로토콜 압축은 그룹 정책를 사용 하 여 **컴퓨터 구성** &gt; **관리 템플릿** &gt; **Windows 구성 요소** &gt; **원격 데스크톱 서비스** 를 사용 하 여 구성할 수 있습니다 &gt; &gt; **원격 세션 환경을** **원격 데스크톱 세션 호스트** **RemoteFX 데이터의 압축을 구성할**&gt;. 다음 세 가지 값을 사용할 수 있습니다.

-   **더 작은 메모리를 사용 하도록 최적화** 는 세션당 최소 양의 메모리를 사용 하지만 압축률은 가장 낮고 대역폭 사용량은 가장 높습니다.

-   **메모리 및 네트워크 대역폭 균형** 조정 메모리 소비량 (세션당 약 200 KB)을 통해 대역폭 사용이 감소 됩니다.

-   **네트워크 대역폭을 줄일 수 있도록 최적화** 세션 당 약 2mb의 비용으로 네트워크 대역폭 사용량을 더욱 줄입니다. 이 설정을 사용 하려면 프로덕션 환경에 서버를 넣기 전에이 설정을 사용 하 여 최대 세션 수를 평가 하 고 해당 수준으로 테스트 해야 합니다.

원격 데스크톱 프로토콜 된 압축 알고리즘을 사용 하지 않도록 선택할 수도 있으므로 네트워크 트래픽을 최적화 하도록 설계 된 하드웨어 장치에만 사용 하는 것이 좋습니다. 압축 알고리즘을 사용 하지 않도록 선택 하는 경우에도 일부 그래픽 데이터가 압축 됩니다.

### <a name="device-redirection"></a>장치 리디렉션

장치 리디렉션은 **컴퓨터 구성** &gt; **관리 템플릿** &gt; **Windows 구성 요소** **&gt; 원격 데스크톱 서비스** 원격에서 그룹 정책를 사용 하 여 구성할 수 있습니다.  **데스크톱 세션 호스트** 는 **장치 및 리소스 리디렉션을** &gt; 서버 관리자의 **세션 컬렉션** 속성 상자를 사용 합니다.

일반적으로 장치 리디렉션은 서버 세션에서 실행 되는 클라이언트 컴퓨터 및 프로세스의 장치 간에 데이터가 교환 되기 때문에 서버 연결 RD 세션 호스트 사용 하는 네트워크 대역폭의 양을 늘립니다. 증가의 범위는 리디렉션된 장치에 대해 서버에서 실행 되는 응용 프로그램에 의해 수행 되는 작업 빈도의 기능입니다.

또한 프린터 리디렉션 및 플러그 앤 플레이 장치 리디렉션은 로그인 시 CPU 사용량을 늘립니다. 다음 두 가지 방법으로 프린터를 리디렉션할 수 있습니다.

-   프린터 드라이버를 서버에 설치 해야 할 때 프린터 드라이버 기반 리디렉션과 일치 이전 버전의 Windows Server에서는이 메서드를 사용 했습니다.

-   Windows Server 2008에 도입 된 간편한 인쇄 프린터 드라이버 리디렉션은 모든 프린터에 공통 프린터 드라이버를 사용 합니다.

연결 시 프린터 설치에 대 한 CPU 사용량을 줄일 수 있기 때문에 간단한 인쇄 방법을 사용 하는 것이 좋습니다. 일치 하는 드라이버 방법을 사용 하면 스풀러 서비스가 다른 드라이버를 로드 해야 하기 때문에 CPU 사용량이 증가 합니다. 대역폭 사용량의 경우 간편한 인쇄로 인해 네트워크 대역폭 사용량이 약간 증가 하지만 다른 성능, 관리 효율성 및 안정성 이점을 상쇄 하는 데에는 중요 하지 않습니다.

오디오 리디렉션은 네트워크 트래픽 흐름을 유발 합니다. 또한 오디오 리디렉션을 사용 하면 사용자가 일반적으로 CPU 사용량이 많은 멀티미디어 앱을 실행할 수 있습니다.

### <a name="client-experience-settings"></a>클라이언트 환경 설정

기본적으로 RDC (원격 데스크톱 연결)는 서버와 클라이언트 컴퓨터 간의 네트워크 연결 적합성에 따라 적절 한 환경 설정을 자동으로 선택 합니다. RDC 구성은 **자동으로 연결 품질 감지**에 유지 되는 것이 좋습니다.

고급 사용자의 경우 RDC는 원격 데스크톱 서비스 연결에 대 한 네트워크 대역폭 성능에 영향을 주는 다양 한 설정에 대 한 제어를 제공 합니다. 원격 데스크톱 연결 또는 RDP 파일의 설정에서 **환경** 탭을 사용 하 여 다음 설정에 액세스할 수 있습니다.

컴퓨터에 연결할 때 다음 설정이 적용 됩니다.

-   **배경 무늬 사용 안 함** (배경 무늬 사용 안 함: i: 0)은 리디렉션된 연결에 바탕 화면 배경 화면을 표시 하지 않습니다. 이 설정은 데스크톱 배경 무늬가 이미지 또는 그리기 비용이 많은 다른 콘텐츠로 구성 된 경우 대역폭 사용을 크게 줄일 수 있습니다.

-   **비트맵 캐시** (Bitmapcachepersistenable: i: 1)이 설정을 사용 하도록 설정 하면 세션에서 렌더링 되는 비트맵의 클라이언트 쪽 캐시가 생성 됩니다. 대역폭 사용량을 크게 향상 시킬 수 있으며, 다른 보안 고려 사항이 없는 한 항상 사용 하도록 설정 해야 합니다.

-   **끌 때 창의 내용 표시** (전체 창 끌기를 사용 하지 않도록 설정: i: 1)이 설정을 사용 하지 않도록 설정 하면 창을 끌 때 모든 콘텐츠 대신 창 프레임만 표시 하 여 대역폭을 줄일 수 있습니다.

-   **메뉴 및 창 애니메이션** (메뉴 anims: i: 1 및 커서 설정 사용 안 함: i: 1): 이러한 설정을 사용 하지 않도록 설정 하면 메뉴 (예: 페이딩) 및 커서에서 애니메이션을 사용 하지 않도록 설정 하 여 대역폭을 줄일 수 있습니다.

-   **글꼴 다듬기** (글꼴 다듬기 허용: i: 0)는 ClearType 글꼴 렌더링 지원을 제어 합니다. Windows 8 또는 Windows Server 2012 이상을 실행 하는 컴퓨터에 연결 하는 경우이 설정을 사용 하거나 사용 하지 않도록 설정 해도 대역폭 사용량에는 상당한 영향을 주지 않습니다. 그러나 Windows 7 및 Windows 2008 R2 이전 버전을 실행 하는 컴퓨터의 경우이 설정을 사용 하도록 설정 하면 네트워크 대역폭 사용량에 크게 영향을 줍니다.

다음 설정은 Windows 7 및 이전 버전의 운영 체제 버전을 실행 하는 컴퓨터에 연결 하는 경우에만 적용 됩니다.

-   **바탕 화면 컴퍼지션** 이 설정은 Windows 7 또는 Windows Server 2008 r 2를 실행 하는 컴퓨터에 대 한 원격 세션에 대해서만 지원 됩니다.

-   **비주얼 스타일** (테마 사용 안 함: i: 1)이 설정을 사용 하지 않도록 설정 하면 클래식 테마를 사용 하는 테마 그리기를 간소화 하 여 대역폭을 줄입니다.

원격 데스크톱 연결 내에서 **환경** 탭을 사용 하 여 네트워크 대역폭 성능에 영향을 주는 연결 속도를 선택할 수 있습니다. 다음 목록에는 연결 속도를 구성 하는 데 사용할 수 있는 옵션이 나와 있습니다.

-   **자동으로 연결 품질 검색** (연결 형식: i: 7)이 설정을 사용 하는 경우 연결 품질에 따라 최적의 사용자 환경을 제공 하는 설정이 자동으로 선택 원격 데스크톱 연결. Windows 8 또는 Windows Server 2012 이상을 실행 하는 컴퓨터에 연결 하는 경우이 구성을 권장 합니다.

-   **모뎀 (56 Kbps)** (연결 형식: i: 1)이 설정은 영구적 비트맵 캐싱을 사용 하도록 설정 합니다.

-   **저속 광대역 (256 Kbps-2Mbps)** (연결 형식: i: 2)이 설정은 영구적 비트맵 캐싱과 비주얼 스타일을 사용 하도록 설정 합니다.

-   **셀룰러/위성 (대기 시간이 긴 2mbps-16mbps)** (연결 형식: i: 3)이 설정은 바탕 화면 구성, 영구적 비트맵 캐싱, 비주얼 스타일 및 바탕 화면 배경을 사용 합니다.

-   **고속 광대역 (2 mbps – 10mbps)** (연결 형식: i: 4)이 설정을 사용 하면 바탕 화면 구성을 사용 하 고, 메뉴 및 창 애니메이션을 사용 하는 동안 창의 내용을 표시 하 고, 메뉴 및 창 애니메이션, 영구적 비트맵 캐싱, 비주얼 스타일 및 바탕 화면 배경을 사용할 수 있습니다.

-   **WAN (대기 시간이 긴 10mbps 이상)** (연결 형식: i: 5)이 설정은 바탕 화면 구성을 사용 하도록 설정 하 고, 메뉴 및 창 애니메이션, 영구적 비트맵 캐싱, 비주얼 스타일, 바탕 화면 배경 등을 사용 하도록 설정 합니다.

-   **LAN (10mbps 이상)** (연결 형식: i: 6)이 설정을 사용 하면 바탕 화면 구성을 사용 하 고, 메뉴 및 창 애니메이션, 영구적 비트맵 캐싱, 테마 및 바탕 화면 배경의 바탕 화면 구성을 사용 하 여 창을 표시할 수 있습니다.

### <a name="desktop-size"></a>바탕 화면 크기

원격 세션의 데스크톱 크기는 원격 데스크톱 연결의 표시 탭을 사용 하거나 RDP 구성 파일 (desktopwidth: i: 1152 및 desktopwidth: i: 864)을 사용 하 여 제어할 수 있습니다. 바탕 화면 크기가 클수록 해당 세션과 연결 된 메모리 및 대역폭 소비가 커집니다. 현재 최대 바탕 화면 크기는 4096 x 2048입니다.
