---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Windows 시간 서비스 도구 및 설정
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 10/16/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 7cf3b3f2bb9a2c9f95c50aa6a7b7690f89cdd0af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840664"
---
# <a name="windows-time-service-tools-and-settings"></a>Windows 시간 서비스 도구 및 설정
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상

이 항목에서는 Windows 시간 서비스 (w32time))에 대 한 설정 및 도구에 대 한 알아봅니다. 

도메인에 가입 된 클라이언트 컴퓨터에 대 한 시간을 동기화 하려는 경우 참조 [자동 도메인 시간 동기화를 위해 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)합니다. Windows 시간 서비스를 구성 하는 방법에 대 한 추가 항목을 참조 하세요 [Windows 시간 서비스 구성 정보를 찾을 수 있는 위치](https://docs.microsoft.com/windows-server/networking/windows-time-service/windows-time-service-top)합니다.  
  
>[!CAUTION]  
>하지 Net time 명령을 사용 하 여 구성 하거나 Windows 시간 서비스가 실행 되는 경우 시간을 설정 해야 합니다.  
>
>또한 Windows XP를 실행 하는 오래 된 컴퓨터 또는 이전에 명령 Net time /querysntp 있는 컴퓨터에를 동기화 하기 위해 구성 된 시간 NTP (Network Protocol) 서버의 이름을 표시 되지만 시간 클라이언트 컴퓨터의 경우에 사용 하는 NTP 서버 NTP 또는 AllSync로 구성 합니다. 해당 명령이 이후 되지 않습니다.  
  
대부분의 도메인 구성원 컴퓨터 형식이 시간 클라이언트 NT5DS 도메인 계층 구조에서 시간을 동기화 하는 것을 의미 합니다. 만 일반적인 예외는 일반적으로 외부 시간 원본을 사용 하 여 시간을 동기화 하도록 구성 된 포리스트 루트 도메인의 주 도메인 컨트롤러 (PDC) 에뮬레이터 작업 마스터로 작동 하는 도메인 컨트롤러입니다. 컴퓨터의 시간 클라이언트 구성을 보려면 Windows Server 2008 및 Windows Vista부터에서 관리자 권한 명령 프롬프트에서 W32tm /query /configuration 명령을 실행 하 고 읽기를 **형식** 명령 출력에 줄. 자세한 내용은 [Windows 시간 서비스 작동 방식](https://docs.microsoft.com/windows-server/networking/windows-time-service/How-the-Windows-Time-Service-Works)합니다. 명령을 실행할 수 있습니다 **reg 쿼리 HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** 의 값을 읽고 **NtpServer** 명령 출력에 있습니다.  
  
> [!IMPORTANT]  
> Windows Server 2016 이전 W32Time 서비스 시간에 민감한 응용 프로그램 요구 사항에 맞게 설계 되지 않았습니다.  그러나 Windows Server 2016에 대 한 업데이트 수 1ms에 대 한 솔루션을 구현 하려면 도메인의 정확도입니다.  참조 [Windows 2016 정확한 내용 시간](accurate-time.md) 하 고 [지원 정확도 높은 환경에 대 한 Windows 시간 서비스를 구성 하는 경계](https://docs.microsoft.com/windows-server/networking/windows-time-service/support-boundary) 자세한 내용은 합니다.  
  
## <a name="windows-time-service-tools"></a>Windows 시간 서비스 도구  
다음 도구는 Windows 시간 서비스와 연결 합니다.  
  
#### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows 시간  
**범주**  

이 도구는 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 기본 설치의 일부로 설치 됩니다.  
  
**버전 호환성**  
  
이 도구는 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 기본 설치에서 작동합니다.  
  
Windows 시간 서비스 설정을 구성 하려면 W32tm.exe 사용 됩니다. 시간 서비스를 사용 하 여 문제를 진단 하려면 데도 수 있습니다. W32tm.exe는 구성, 모니터링 또는 Windows 시간 서비스 문제 해결에 대 한 기본 명령줄 도구입니다.  
  
다음 표에서 W32tm.exe 사용 되는 매개 변수를 설명 합니다.  
  
**W32tm.exe 기본 매개 변수**  
  
|매개 변수|설명|  
|-------------|---------------|  
|W32tm /?|W32tm 명령줄 도움말|  
|W32tm /register|서비스로 실행 하도록 시간 서비스를 등록 하 고 기본 구성 레지스트리에 추가 합니다.|  
|W32tm /unregister|시간 서비스의 등록을 취소 하 고 모든 구성 정보가 레지스트리에서 제거 합니다.|  
|w32tm /monitor<br /><br />[/domain:<domain name>] [/computers:<name>[,<name>[,<name>...]]] [/threads:<num>]|도메인-모니터링 하는 도메인을 지정 합니다. 도메인 이름을 지정 하지 않으면, 또는 도메인 아니고 컴퓨터 옵션을 지정 하는 경우에 기본 도메인이 사용 됩니다. 이 옵션을 두 번 이상 사용할 수 있습니다.<br /><br />컴퓨터-지정 된 컴퓨터 목록을 모니터링 합니다. 컴퓨터 이름은 공백 없이 쉼표로 구분 됩니다. 경우는 이름 앞에 ' *', PDC로 처리 됩니다. 이 옵션을 두 번 이상 사용할 수 있습니다.<br /><br />스레드-동시에 분석 하는 컴퓨터의 수를 지정 합니다. 기본값은 3입니다. 허용된 범위는 1 ~ 50입니다.|  
|w32tm /ntte <NT time epoch>|에 NT 시스템 시간을 변환 (10 ^-7)에서 읽을 수 있는 형식으로, 1601 년 1 월 1-0 h s 간격입니다.|  
|w32tm /ntpte <NTP time epoch>|NTP 시간을 변환 (2 ^-32) s 간격에서 0 h 1-1900 년 1 월을 읽을 수 있는 형식입니다.|  
|w32tm /resync<br /><br />[/computer:<computer>]<br /><br />[/nowait]<br /><br />[/rediscover]<br /><br />[/soft]|모든 누적된 오류 통계 내용을 해당 클록을 가능한 한 빨리 다시 동기화 해야 하는 컴퓨터에 알려 줍니다.<br /><br />컴퓨터:<computer> -다시 동기화 해야 하는 컴퓨터를 지정 합니다. 지정 하지 않으면 로컬 컴퓨터 다시 동기화 합니다.<br /><br />nowait-; 되려면 다시 동기화를 기다리지 않음 즉시 반환 합니다. 그렇지 않으면 반환 하기 전에 완료 하려면 다시 동기화를 기다립니다.<br /><br />다시 검색-네트워크 구성을 다시 검색 네트워크 원본에 다시 확인 하 고 다시 동기화 합니다.<br /><br />소프트-기존 오류 통계를 사용 하 여 다시 동기화 합니다. 유용 하지 않음, 호환성을 위해 제공 합니다.|  
|w32tm /stripchart<br /><br />/computer:<target><br /><br />[/period:<refresh>]<br /><br />[/dataonly]<br /><br />[/ 샘플:<count>]<br/><br/>[/rdtsc]<br/>|이 컴퓨터와 다른 컴퓨터 사이의 오프셋 줄무늬 차트를 표시 합니다.<br /><br />컴퓨터:<target> -컴퓨터에 대 한 오프셋을 측정 합니다.<br /><br />기간:<refresh> -샘플에는 시간 (초) 사이의 시간입니다. 기본값은 2 초입니다.<br /><br />dataonly-그래픽 하지 않고 데이터만 표시 합니다.<br /><br />샘플:<count> 수집- <count> 예제를 중지 합니다. 지정 하지 않으면 샘플이까지 수집 됩니다 **Ctrl + C** 눌러져 있습니다.<br/><br/>rdtsc:이 옵션 각 샘플에 대 한 RdtscStart, 헤더와 함께 쉼표로 구분 된 값을 출력 RdtscEnd, FileTime, RoundtripDelay NtpOffset 텍스트 그래픽 대신 합니다.<br/><ul><li>[RdtscStart – RDTSC (읽기 타임 스탬프 카운터)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) NTP 요청 생성 되기 직전에 수집 된 값입니다.</li><li>RdtscEnd – NTP 응답 수신 및 처리 된 후 바로 수집된 RDTSC (읽기 타임 스탬프 카운터) 값입니다.</li><li>FileTime – NTP 요청에 사용 되는 로컬 FILETIME 값입니다.</li><li>RoundtripDelay – NTP 요청을 생성 하는 간격 (초)에서 경과 된 시간과 NTP 왕복 계산에 따라 계산 받은 NTP 응답을 처리 합니다.</li><li>NTPOffset-로컬 컴퓨터 및 NTP 서버 간의 시간 (초)의 시간 오프셋 NTP 오프셋된 계산에 따라 계산 됩니다.</li></ul>|
|w32tm /config<br /><br />[/computer:<target>]<br /><br />[/update]<br /><br />[/ manualpeerlist:<peers>]<br /><br />[/syncfromflags:<source>]<br /><br />[/LocalClockDispersion:<seconds>]<br /><br />[/reliable:(YES&#124;NO)]<br /><br />[/largephaseoffset:<milliseconds>]|컴퓨터:<target> -구성을 조정 <target>합니다. 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.<br /><br />업데이트-구성 변경 내용을 적용 하려면 변경의 원인인 시간 서비스에 알립니다.<br /><br />manualpeerlist:<peers> -수동 피어 목록을 설정 <peers>, DNS 및/또는 IP 주소의 공백으로 구분 된 목록입니다. 여러 피어를 지정 하는 경우이 옵션을 따옴표로 묶어야 합니다.<br /><br />syncfromflags:<source> -어떤 원본에서 동기화 해야 하는 NTP 클라이언트를 설정 합니다. <source> 해야 이러한 키워드는 쉼표로 구분 된 목록 (없습니다 대/소문자 구분):<br /><br />수동-수동 피어 목록에서 피어를 포함 합니다.<br /><br />DOMHIER-도메인 컨트롤러 (DC) 도메인 계층 구조에서 동기화 합니다.<br /><br />LocalClockDispersion:<seconds> -W32Time 시간 구성된 소스에서 획득할 수 없으면 때 가정 하는 내부 클록의 정확도 구성 합니다.<br /><br />신뢰할 수 있는: (YES&#124;아니요) 설정-이 컴퓨터의 신뢰할 수 있는 시간 원본 인지 합니다.<br /><br />이 설정은 도메인 컨트롤러에서 의미 있는 됩니다.<br /><br />예-이 컴퓨터는 신뢰할 수 있는 시간 서비스.<br /><br />아니요-이 컴퓨터는 신뢰할 수 있는 시간 서비스가 아닙니다.<br /><br />largephaseoffset:<milliseconds> -로컬 사이의 시간 차이 설정 및 네트워크 W32Time는 스파이크를 고려 하는 시간입니다.|  
|w32tm /tz|현재 표준 시간대 설정을 표시 합니다.|  
|w32tm /dumpreg<br /><br />[/subkey:<key>]<br /><br />[/computer:<target>]|지정 된 레지스트리 키와 연결 된 값을 표시 합니다.<br /><br />기본 키는 HKLM\System\CurrentControlSet\Services\W32Time<br /><br />(루트 키 시간 서비스에 대 한).<br /><br />하위 키:<key> -하위 키와 연결 된 값을 표시 <key> 기본 키입니다.<br /><br />컴퓨터:<target> -레지스트리 설정을 컴퓨터에 대 한 쿼리 <target>|  
|w32tm /query [/ 컴퓨터:<target>] {원본 &#124; /configuration &#124; 피어 링/ &#124; /status} [] / [자세한 정보]|이 매개 변수를 먼저 Windows Vista 및 Windows Server 2008의 Windows 시간 클라이언트 버전에서 사용할 수 있습니다.<br /><br />컴퓨터의 Windows 시간 서비스 정보를 표시 합니다.<br /><br />**컴퓨터:<target>**  -의 정보를 쿼리할 **<target>** 합니다. 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.<br /><br />**원본** -시간 원본을 표시 합니다.<br /><br />**구성** -런타임 및 설정에서 제공 하는 위치 구성을 표시 합니다. 세부 정보 표시 모드로 정의 되지 않거나 사용 되지 않는 설정은 너무를 표시 합니다.<br /><br />**피어** -피어 및 해당 상태 목록을 표시 합니다.<br /><br />**상태** -표시 Windows 시간 서비스 상태입니다.<br /><br />**verbose** -자세한 정보를 표시 하려면 세부 정보 표시 모드를 설정 합니다.|  
|w32tm /debug {/ 사용 안 함 &#124; {/ /file:<name> /크기:<bytes> /entries:<value> [/truncate]}}|이 매개 변수를 먼저 Windows Vista 및 Windows Server 2008의 Windows 시간 클라이언트 버전에서 사용할 수 있습니다.<br /><br />로컬 컴퓨터의 Windows 시간 서비스 전용 로그를 사용 하지 않도록 설정 하거나 사용 합니다.<br /><br />**사용 하지 않도록 설정** -개인 로그를 사용 하지 않도록 설정 합니다.<br /><br />**사용 하도록 설정** -개인 로그를 사용 하도록 설정 합니다.<br /><br />-   **파일:<name>**  -절대 파일 이름을 지정 합니다.<br />-   **크기:<bytes>**  -순환 로깅에 대 한 최대 크기를 지정 합니다.<br />-   **항목:<value>**  -번호로 지정 되 고 로그에 기록 되어야 하는 정보의 유형을 지정 하는 쉼표로 구분 하 여 플래그의 목록을 포함 합니다. 유효한 숫자는 0 ~ 300입니다. 숫자 범위는 0-100,103 같은 단일 숫자 외에도 유효한 106 합니다. 0-300 값은 모든 정보를 기록입니다.<br /><br />**truncate** -존재 하는 경우 파일을 자릅니다.|  

---  
에 대 한 자세한 내용은 **W32tm.exe**, 도움말 및 지원 센터에서 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2를 참조 하세요.  
  
## <a name="windows-time-service-registry-entries"></a>Windows 시간 서비스 레지스트리 항목  
다음 레지스트리 항목은 Windows 시간 서비스와 연결 합니다.  
  
이 정보는 문제 해결에 필요한 설정을 적용 되었는지 확인 하는 사용에 대 한 참조로 제공 됩니다. 하면 직접 편집 하지 않는 레지스트리 다른 대체 방법이 없는 경우를 제외 하는 것이 좋습니다. 레지스트리를 수정 하지 전에 유효성을 검사 나 Windows 레지스트리 편집기에서 적용 되 고 결과적으로, 잘못 된 값을 저장할 수 있습니다. 이 시스템에 복구할 수 없는 오류가 발생할 수 있습니다.  
  
가능 하면 그룹 정책 또는 다른 Windows 도구를 같은 Microsoft 관리 콘솔 (MMC)를 사용 하 여 레지스트리를 직접 편집 하는 것이 아니라 작업을 수행 하 합니다. 레지스트리를 편집해야 하는 경우 각별히 주의하세요.  
  
> [!WARNING]  
> 일부 그룹 정책 개체 (GPO)에 대 한 시스템 관리 템플릿 파일 (System.adm)에 구성 된 미리 설정 된 값은 해당 기본 레지스트리 항목을 다릅니다. GPO를 사용 하 여 모든 Windows 시간 설정을 구성 하려는 경우 반드시 검토 될 [Windows 시간 서비스 그룹 정책 설정에 대 한 기본 설정 값은 Windows Server 2003의 해당 Windows 시간 서비스 레지스트리 항목에서 다른 ](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다.  
  
Windows 시간 서비스에 대 한 여러 레지스트리 항목이 동일한 이름의 그룹 정책 설정으로 동일합니다. 그룹 정책 설정에 이름이 같은 레지스트리 항목에 해당 합니다.  
  
>**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\\**

  
이 레지스트리 위치는 레지스트리 키입니다. Windows 시간 설정은 이러한 키의 모든 값에 저장 됩니다.
* [매개 변수](#Parameters)
* [Config](#Configuration)
* [NtpClient](#NtpClient)
* [NtpServer](#NtpServer)
  

대부분의 레지스트리 W32Time 절의 값 내부적으로 사용 W32Time 정보를 저장 합니다. 언제 든 지 이러한 값을 수동으로 변경할 수 해야 합니다. 수정 하지 마십시오이 섹션의 설정 중 필요한 설정을 사용 하 여 익숙한는 새 값을 예상 대로 작동 하는 경우가 아니면. 다음 레지스트리 항목은 다음 위치에

**HKLM\SYSTEM\CurrentControlSet\Services\W32Time**  

정책을 만들 때 설정은 다음 위치를 통해 우선 적용 되지 않습니다는 다음 위치에서 구성 됩니다.

**HKLM\SOFTWARE\Policies\Microsoft\Windows\W32time**

W32time 키 정책을 사용 하 여 만들어집니다.  정책을 제거 하면,이 키도 제거 됩니다.

다른 기본 위치:

**HKLM\SYSTEM\CurrentControlSet\Services\W32time**

레지스트리에서 클록 틱에 저장 된 일부 매개 변수 및 시간 (초)의 일부가 있습니다. 변환할 시간 클록 틱의 시간 (초):  
  
-   1 분 = 60 초  
  
-   1 초 = 1000 밀리초  
  
-   1 ms에 설명 된 대로 Windows 시스템에서 10,000 클록 틱 = [DateTime.Ticks Property](https://docs.microsoft.com/dotnet/api/system.datetime.ticks?redirectedfrom=MSDN&view=netframework-4.7.2#System_DateTime_Ticks)합니다.  
  
예를 들어 5 분 5 * 60 할\*1000\*10000 = 3000000000 클록 틱입니다. 

모든 버전에는 Windows 7, Windows 8, Windows 10, Windows Server 2008 및 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012R2, Windows Server 2016 포함 됩니다.  일부 항목은 최신 Windows 버전에서 사용할 수만 있습니다.


#### <a name="hklmsystemcurrentcontrolsetservicesw32timeparameters"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters

|레지스트리 항목|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|All|항목 피어 간의 동기화에 비표준 모드 조합 허용 됨을 나타냅니다. 도메인 구성원에 대 한 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1입니다.|
|NtpServer|All|항목에는 하나 이상의 DNS 이름 또는 IP 주소가 한 줄으로 구성 된 컴퓨터를 타임 스탬프를 가져올 피어 공백으로 구분 된 목록을 지정 합니다. 각 DNS 이름 또는 나열 된 IP 주소는 고유 해야 합니다. 도메인에 연결 하는 컴퓨터는 같은 공식 미국 시간 클록을 더 신뢰할 수 있는 시간 원본과 동기화 해야 합니다.  <ul><li>0x01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive-이 모드에 대 한 자세한 내용은 참조 하세요. [Windows 시간 서버: 3.3 작업의 모드](https://go.microsoft.com/fwlink/?LinkId=208012)합니다.</li><li>0x08 클라이언트</li></ul><br />도메인 멤버에서이 레지스트리 항목에 대 한 기본값이 있습니다. 독립 실행형 클라이언트 및 서버에서 기본값은 time.windows.com,0x1 합니다.<br /><br />참고: 사용 가능한 NTP 서버에 대 한 자세한 내용은 참조 하세요. [Microsoft 기술 자료 문서 262680-인터넷에서 사용할 수 있는 네트워크 시간 프로토콜 SNTP () 시간 서버 목록](https://go.microsoft.com/fwlink/?LinkId=186067)|
|ServiceDll|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 하 고이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 구성원 및 독립 실행형 클라이언트와 서버 모두에서이 DLL에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.  |
|ServiceMain|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 하 고이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버에서 기본값은 SvchostEntry_W32Time 합니다. 독립 실행형 클라이언트 및 서버에서 기본값은 SvchostEntry_W32Time 합니다.  "|
|형식|All|항목에서 동기화를 허용 하는 피어 링 하는 것을 나타냅니다.  <ul><li>**NoSync**. 시간 서비스를 다른 원본과 동기화 하지 않습니다.</li><li>**NTP.** 시간 서비스에서 지정한 서버에서 동기화 된 **NtpServer**합니다. 레지스트리 항목입니다.</li><li>**NT5DS**. 시간 서비스 도메인 계층 구조에서 동기화합니다.  </li><li>**AllSync**. 시간 서비스는 모든 사용 가능한 동기화 메커니즘을 사용합니다.  </li></ul>도메인 멤버에서 기본값인 **NT5DS**합니다. 독립 실행형 클라이언트 및 서버에서 기본값은 **NTP**합니다.   |
---
#### <a name="hklmsystemcurrentcontrolsetservicesw32timeconfig"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config

|레지스트리 항목|버전|설명|
|------------------------------------|---------------|----------------------------|
|AnnounceFlags|All|항목이이 컴퓨터는 신뢰할 수 있는 시간 서버 됨으로 표시 되는지 여부를 제어 합니다. 컴퓨터 시간 서버와도 표시 하지 않으면 신뢰할 수 있는 것으로 표시 되지 않습니다.<br /> -0x00 시간 서버가 아닌  <br /> -0x01 항상 시간 서버  <br /> -0x02 자동 시간 서버  <br /> -0x04 항상 신뢰할 수 있는 시간 서버  <br /> -0x08 자동 신뢰할 수 있는 시간 서버  <br />도메인 구성원에 대 한 기본값은 10입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 10입니다.|
|EventLogFlags|All|항목 이벤트 시간 서비스 로그를 제어 합니다.  <br />시간 이동 합니다. 0x1  <br />소스 변경: 0x2  <br />도메인 구성원의 기본값은 2입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 2입니다.  |
|FrequencyCorrectRate|All|클록이 수정 속도 제어 하는 항목입니다. 이 값이 너무 작아서 이면 시계 안정적이 지 않은 및 overcorrects 합니다. 값을 너무 큰 경우 시계를 동기화 하려면 시간이 오래 걸립니다. 도메인 구성원의 기본값은 4입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 4입니다.  <br /><br />0은 FrequencyCorrectRate 레지스트리 항목에 대 한 잘못 된 값을 참고 합니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 컴퓨터에서 값을 0으로 설정 된 경우 Windows 시간 서비스를 자동으로 변경 됩니다 1입니다.  |
|HoldPeriod|All|항목은 스파이크 감지 상태로 로컬 시계 동기화 신속 하 게 하기 위해 비활성화 되어 있는 기간을 제어 합니다. 급증 하는 경우 해당 시간을 나타내는 시간 예제를 몇 초 해제 되 고 적절 한 시간 샘플 일관 되 게 반환 된 후 일반적으로 수신 도메인 구성원의 기본값은 5입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 5입니다.  |
|LargePhaseOffset|All|항목 시간 오프셋 보다 큰 또는 10에서이 값을 지정 합니다<sup>-7</sup> 초 급증 하는 것으로 간주 됩니다. 많은 양의 트래픽이 같은 네트워크 중단이 발생 하는 급등을 유발할 수 있습니다. 급증은 오랜 기간 동안 유지 하지 않으면 무시 됩니다. 도메인 멤버에서 기본값은 50000000 합니다. 독립 실행형 클라이언트 및 서버에서 기본값은 50000000 합니다.  |
|LastClockRate|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 하 고이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버에서 기본값은 156250 합니다. 독립 실행형 클라이언트 및 서버에서 기본값은 156250 합니다.  |
|LocalClockDispersion|All|항목 제어 때 가정해 야 하는 초 단위로 경향에 기본 제공 시계 원본이 있습니다. 도메인 구성원의 기본값은 10입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 10입니다.|
|MaxAllowedPhaseOffset|All|항목에는 최대 오프셋 (초)는 W32Time 클록 속도 사용 하 여 컴퓨터 시계를 조정 하려고 지정 합니다. 오프셋이이 비율을 초과 하면 W32Time 직접 컴퓨터 시계를 설정 합니다. 도메인 구성원에 대 한 기본값은 300입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1입니다.  [자세한 내용은 아래를 참조 하세요](#MaxAllowedPhaseOffset)합니다.|
|MaxClockRate|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 하 고이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 구성원에 대 한 기본값은 155860 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 155860 합니다.  |
|MaxNegPhaseCorrection|All|서비스에서 수행 하는 시간 (초)에서 가장 큰 음수 시간 수정을 지정 합니다. 서비스에서이 값 보다 큰 변경이 필요 하다 고 결정 하는 경우 그 대신 이벤트를 기록 합니다. 특별 한 경우: 0xFFFFFFFF 항상 시간 수정 확인을 의미 합니다. 도메인 구성원에 대 한 기본값은 0xFFFFFFFF입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 54,000 (15 시간).  |
|MaxPollInterval|All|항목은 최대 간격을 초 단위로 지정 log2, 시스템 폴링 간격에 대 한 허용 합니다. 예약 된 간격에 따라 시스템 폴링해야, 하지만 작업을 수행 하도록 요청 하면 샘플을 생성 하는 공급자 거부할 수 있습니다 note 합니다. 도메인 컨트롤러에 대 한 기본값은 10입니다. 도메인 구성원에 대 한 기본값은 15입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 15입니다.  |
|MaxPosPhaseCorrection|All|서비스에서 수행 하는 초 단위는 최대 양수 시간 수정을 지정 합니다. 서비스에서이 값 보다 큰 변경이 필요 하다 고 결정 하는 경우 그 대신 이벤트를 기록 합니다. 특별 한 경우: 0xFFFFFFFF 항상 시간 수정 확인을 의미 합니다. 도메인 구성원에 대 한 기본값은 0xFFFFFFFF입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 54,000 (15 시간).  |
|MinClockRate|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 하 고이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 구성원에 대 한 기본값은 155860 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 155860 합니다.  |
|MinPollInterval|All|항목 최소 간격을 초 단위로 지정 log2, 시스템 폴링 간격에 대 한 허용 합니다. 시스템에서는 샘플을 이보다 더 자주 요청 하지 않고, 하지만 공급자 수 샘플은 예약 된 간격 이외의 시간에 생성 note 합니다. 도메인 컨트롤러에 대 한 기본값은 6입니다. 도메인 구성원에 대 한 기본값은 10입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 10입니다.  |
|PhaseCorrectRate|All|항목 단계 오류를 수정할는 속도 제어 합니다. 작은 값을 지정 단계 오류를 신속 하 게 해결 하지만 불안정 해질 수 클록 발생할 수 있습니다. 값을 너무 큰 경우 단계 오류를 해결 하려면 시간이 오래 걸립니다. <br /><br />도메인 구성원의 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 7입니다.<br /><br />참고: 0은 PhaseCorrectRate 레지스트리 항목에 대 한 잘못 된 값입니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 컴퓨터에서 값을 0으로 설정 된 경우 Windows 시간 서비스를 자동으로 변경 1.  |
|PollAdjustFactor|All|항목을 시스템에 대 한 폴링 간격을 늘리거나 의사 결정을 제어 합니다. 값이 클수록, 폴링 간격을 낮출 수를 발생 시키는 오류 양이 줄어듭니다. 도메인 구성원의 기본값은 5입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 5입니다. |
|SpikeWatchPeriod|All|항목 지정 의심 스러운 오프셋을 유지 해야 하는 시간 (초)에서 올바른 것으로 수락 하기 전에 합니다. 도메인 구성원의 기본값은 900입니다. 독립 실행형 클라이언트 및 워크스테이션에서 기본값은 900입니다.  |
|TimeJumpAuditOffset|All|점프 감사 임계값 시간 (초)에서 지정 하는 부호 없는 정수입니다. 시간 서비스 시계를 직접 설정 하 여 로컬 시계를 조정 하는 경우 시간 수정이이 값 보다 많은 시간 서비스가 감사 이벤트를 기록 합니다.|
|UpdateInterval|All|항목 수정 조정 단계 간의 클록 틱 수를 지정합니다. 도메인 컨트롤러에 대 한 기본값은 100입니다. 도메인 구성원에 대 한 기본값은 30,000 개입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 360,000 합니다.  <br /><br />**참고**: 0은 UpdateInterval 레지스트리 항목에 대 한 잘못 된 값입니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2를 실행 하는 컴퓨터에서 값을 0으로 설정 된 경우 Windows 시간 서비스를 자동으로 변경 1.<br /><br />다음 세 개의 레지스트리 항목을 W32Time 기본 구성의 일부가 아닌 있지만 향상 된 로깅 기능을 얻기 위해 레지스트리를 추가할 수 있습니다. EventLogFlags 설정은 그룹 정책 개체 편집기에서 값을 변경 하 여 시스템 이벤트 로그에 기록 된 정보를 수정할 수 있습니다. 기본적으로 시간 서비스는 새 시간 원본으로 전환 될 때마다 이벤트 뷰어에서 로그를 만듭니다.<br /><br />**경고**: 일부 그룹 정책 개체 (GPO)에 대 한 시스템 관리 템플릿 파일 (System.adm)에 구성 된 미리 설정 된 값은 해당 기본 레지스트리 항목을 다릅니다. GPO를 사용 하 여 모든 Windows 시간 설정을 구성 하려는 경우 반드시 검토 될 [Windows 시간 서비스 그룹 정책 설정에 대 한 기본 설정 값은 Windows Server 2003의 해당 Windows 시간 서비스 레지스트리 항목에서 다른 ](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다. |
|UtilizeSslTimeData|Windows 10 빌드 1511 게시|항목 1는 W32Time 시계 매우 정확 하지 않은 초기값으로 여러 SSL 타임 스탬프를 사용할지를 나타냅니다.|
---
W32Time 로깅을 사용 하도록 설정 하려면 다음 레지스트리 항목을 추가 해야 합니다.  

|레지스트리 항목|버전|설명|
|------------------------------------|---------------|----------------------------|
|FileLogEntries|All|항목에는 Windows 시간 로그 파일에서 생성 하는 항목의 양을 제어 합니다. 기본값은 none, Windows 시간 작업을 기록 하지 않습니다. 유효한 값은 0 ~ 300입니다. 이 값은 일반적으로 Windows 시간을 만들어 이벤트 로그 항목을 영향을 주지 않습니다.|
|FileLogName|All|항목의 Windows 시간 로그 파일 이름과 위치를 제어합니다. 기본값은 비어 있으며 변경할 수 없는 경우가 아니면 **FileLogEntries** 변경 됩니다. 유효한 값에는 전체 경로 및 Windows 시간 로그 파일을 만드는 데 사용할 파일 이름입니다. 이 값에는 일반적으로 Windows 시간을 만들어 이벤트 로그 항목이 적용 되지 않습니다.  |
|FileLogSize|All|Windows 시간 로그 파일의 순환 로깅 동작을 제어 하는 항목입니다. 때 **FileLogEntries** 하 고 **FileLogName** 는 정의 된 항목의 크기를 바이트 단위로 정의 로그 파일을 새 항목을 사용 하 여 가장 오래 된 로그 항목을 덮어쓰기 전에 도달할 수 있도록 합니다. 이 설정에 대 한 1000000 또는 큰 값을 사용 하십시오. 이 값에는 일반적으로 Windows 시간을 만들어 이벤트 로그 항목이 적용 되지 않습니다.  |

---

#### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpclient"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient

|레지스트리 항목|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|All|항목 피어 간의 동기화에 비표준 모드 조합 허용 됨을 나타냅니다. 도메인 구성원에 대 한 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1입니다.|
|CompatibilityFlags|All|항목에는 다음 호환성 플래그 및 값을 지정합니다. <br /><br />-   DispersionInvalid: 0x00000001  <br />-   IgnoreFutureRefTimeStamp: 0x00000002  <br /> -   AutodetectWin2K: 0 x 80000000  <br />-   AutodetectWin2KStage2: 0x40000000  <br /><br />도메인 구성원에 대 한 기본값은 0x80000000입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 0x80000000입니다.  |
|CrossSiteSyncFlags|All|서비스 컴퓨터의 도메인 외부 동기화 파트너를 선택 하는지 여부를 결정 하는 항목입니다. 옵션 및 값을 다음과 같습니다.  <br /><br />-None. 0  <br />-   PdcOnly: 1  <br />-   All: 2  <br /><br />NT5DS 값을 설정 하지 않으면이 값은 무시 됩니다. 도메인 구성원에 대 한 기본값은 2입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 2입니다.  |
|DllName|All|시간 공급자에 대 한 DLL의 위치를 지정합니다.  <br /><br />도메인 구성원 및 독립 실행형 클라이언트와 서버 모두에서이 DLL에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.|
|Enabled|All|항목은 NtpClient 공급자는 현재 시간 서비스에서 사용 되는지 여부를 나타냅니다.  <br /><ul><li>예 1</li><li>아니요 0</li></ul>도메인 구성원의 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 1입니다.|
|EventLogFlags|All|항목은 Windows 시간 서비스에 의해 기록 된 이벤트를 지정 합니다.<ul><li>0x1 연결 변경</li><li>0x2 큰 샘플 오차 (이 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2에 적용만)</li></ul>도메인 구성원의 기본 값이 0x1 합니다. 독립 실행형 클라이언트 및 서버에 기본 값이 0x1 합니다.|
|InputProvider|All|항목에는 NtpServer에서 시간 정보를 가져오는 InputProvider로 NtpClient 사용 여부를 나타냅니다. NtpServer는 로컬 시계를 동기화 하는 데 도움이 되는 시간 예제를 반환 하 여 네트워크에서 클라이언트 시간 요청에 응답 하는 시간 서버입니다. <ul><li>Yes = 1  </li><li>이상 = 0 </li></ul><p>도메인 구성원 및 독립 실행형 클라이언트에 대 한 기본 값: 1  |
|LargeSampleSkew|All|항목에는 시간 (초)을 로그인에 대 한 큰 샘플 기울이기를 지정 합니다. 을 준수 하기 위해 보안 및 Exchange Commission (초) 사양과 3 초로 설정 되어야 합니다. EventLogFlags 오차 0x2 큰 샘플에 대 한 명시적으로 구성 된 경우에이 설정에 대 한 이벤트가 기록 됩니다. 도메인 구성원의 기본값은 3입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 3입니다.  |
|ResolvePeerBackOffMaxTimes|All|최대 반복 하는 경우 대기 간격을 두 번의 실패와 동기화 하는 피어를 찾으려고 시도 지정 합니다. 값이 0 대기 간격은 항상 최소 의미 합니다. 도메인 구성원의 기본값은 7입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 7입니다. |
|ResolvePeerBackoffMinutes|All|항목에는 초기 간격 (분)와 동기화 하는 피어를 찾으려고 시도 하기 전에 대기을 지정 합니다. 도메인 구성원의 기본값은 15입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 15입니다.  |
|SpecialPollInterval|All|항목 (초) 수동 피어에 대 한 특별 한 폴링 간격을 지정합니다. 0x1 SpecialInterval 플래그를 사용 하는 경우 폴링 간격 대신이 폴링 간격 W32Time 사용 하 여 운영 체제에서 결정 합니다. 도메인 멤버에서 기본값은 3, 600입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 604,800 합니다.<br/><br/>새 빌드 1702에 대 한 SpecialPollInterval MinPollInterval 및 MaxPollInterval 구성 레지스트리 값으로 포함 되어 있습니다.|
|SpecialPollTimeRemaining|All|항목은 W32Time에서 유지 됩니다. Windows 운영 체제에서 사용 되는 예약 된 데이터를 포함 합니다. W32Time에 컴퓨터를 다시 시작한 후 다시 동기화는 초에서 시간을 지정 합니다. 이 설정 변경 하면 예기치 않은 결과가 발생할 수 있습니다. 및 독립 실행형 클라이언트와 서버 모두 도메인 구성원에서 기본 값을 비워 둡니다.  |

---

#### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpserver"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer

|레지스트리 항목|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|All|항목은 클라이언트와 서버 간의 동기화에 비표준 모드 조합 허용 됨을 나타냅니다. 도메인 구성원에 대 한 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1입니다.|
|DllName|All|시간 공급자에 대 한 DLL의 위치를 지정합니다.<br /><br />도메인 구성원 및 독립 실행형 클라이언트와 서버 모두에서이 DLL에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.  |
|Enabled|All|항목은 NtpServer 공급자는 현재 시간 서비스에서 사용 되는지 여부를 나타냅니다. <ul><li>예 1</li><li>아니요 0</li></ul>도메인 구성원의 기본값은 1입니다. 독립 실행형 클라이언트 및 서버에서 기본값은 1입니다.  |
|InputProvider|All|항목에는 NtpServer에서 시간 정보를 가져오는 InputProvider로 NtpClient 사용 여부를 나타냅니다. NtpServer는 로컬 시계를 동기화 하는 데 도움이 되는 시간 예제를 반환 하 여 네트워크에서 클라이언트 시간 요청에 응답 하는 시간 서버입니다. <ul><li>Yes = 1  </li><li>이상 = 0 </li></ul><p>도메인 구성원 및 독립 실행형 클라이언트에 대 한 기본 값: 1  |

---

#### <a name="maxallowedphaseoffset-information"></a>MaxAllowedPhaseOffset 정보
컴퓨터 시계를 점진적으로 설정 하는 W32Time에서 오프셋 되어야 합니다 보다 작은 **MaxAllowedPhaseOffset** 값 및 동시에 다음 수식을 충족 합니다.  

```  
|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2  
``` 
CurrentTimeOffset 여기서 1ms = 10, 000 클록 틱 Windows 시스템 클록 틱을 단위로 측정 됩니다.  
  
SystemClockRate 및 PhaseCorrectRate 또한 클록 틱 단위로 측정 됩니다. SystemClockRate를 가져오려면 다음 명령을 사용 하 여를 클록 틱의 시간 (초) 수식을 사용 하 여 초에서 변환 * 1000\*10000:  
  
```  
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  
  
SystemclockRate는 시스템 클록의 속도. 156000 시간 (초)을 사용 하 여 예를 들어,는 SystemclockRate는 수 = 0.0156000 * 1000 \* 10000 = 156000 클록 틱입니다.  
  
MaxAllowedPhaseOffset 초 이기도합니다. 변환할 클록 틱, MaxAllowedPhaseOffset 곱하기 * 1000\*10000입니다.  
  
다음 두 예제에 적용 하는 방법을 보여 줍니다.  
  
**예 1**: 4 분 시간 다릅니다 (예를 들어 시간은 오전 11시 05분 및 시간 샘플 피어 로부터 수신 하 고 오전 11시 09분은 올바른 것으로 알려져).  
```
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
|currentTimeOffset| = 4mins = 4*60\*1000\*10000 = 2400000000 ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
2400000000 < 6000000000 = TRUE  
```
위의 수식을 충족 하는 고? 
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 2,400,000,000 / (30000*1) < 156000/2  
  
Is 80,000 < 78,000  
  
NO/FALSE  
```  
따라서 W32tm 설정 클록 다시 즉시 합니다.  
  
> [!NOTE]  
> 이 경우 느린 시계를 다시 설정 하려는 경우에 PhaseCorrectRate 또는 레지스트리에서 updateInterval도 true에서 수식 결과를 얻으려면의 값을 조정 해야 합니다.  
  
**예 2**: 3 분 시간이 다릅니다.  
```  
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
currentTimeOffset = 3mins = 3*60\*1000\*10000 = 1800000000 clock ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
1800000000 < 6000000000 = TRUE  
```  
위의 수식을 충족 하는 고?
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 3 mins (1,800,000,000) / (30000*1) < 156000/2  
  
Is 60,000 < 78,000  
  
YES/TRUE  
```  
이 경우 시계가 다시 설정 됩니다 느리게 합니다.  
  
## <a name="windows-time-service-group-policy-settings"></a>Windows 시간 서비스 그룹 정책 설정  
그룹 정책 개체 편집기를 사용 하 여 대부분의 W32Time 매개 변수를 구성할 수 있습니다. 여기에 NTPServer 또는 NTPClient, 시간 동기화 메커니즘을 구성 하 고 컴퓨터 구성에서 신뢰할 수 있는 시간 원본으로 사용할 컴퓨터를 구성 합니다.  
  
> [!NOTE]  
> Windows 시간 서비스에 대 한 그룹 정책 설정은 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 도메인 컨트롤러에서 구성할 수 있으며 Windows Server 2003, Windows Server를 실행 하는 컴퓨터에만 적용할 수 있습니다. 2003 R2, Windows Server 2008 및 Windows Server 2008 R2.  
  
그룹 정책 설정을 다음 위치에서 그룹 정책 개체 편집기 스냅인에서 W32Time를 구성 하는 데 찾을 수 있습니다.  
  
-   컴퓨터 구성 \ 관리 템플릿 Templates\System\Windows 시간 서비스  
  
    구성할 **전역 구성 설정을** 여기 있습니다.  
  
-   컴퓨터 구성 \ 관리 템플릿 Templates\System\Windows 시간 Service\Time 공급자  
  
    구성할 **Windows NTP 클라이언트** 여기에 설정 합니다.  
  
    사용 하도록 설정 **Windows NTP 클라이언트** 여기 있습니다.  
  
    사용 하도록 설정 **Windows NTP 서버** 여기 있습니다.  
  
> [!WARNING]  
> 일부 그룹 정책 개체 (GPO)에 대 한 시스템 관리 템플릿 파일 (System.adm)에 구성 된 미리 설정 된 값은 해당 기본 레지스트리 항목을 다릅니다. GPO를 사용 하 여 모든 Windows 시간 설정을 구성 하려는 경우 반드시 검토 될 [Windows 시간 서비스 그룹 정책 설정에 대 한 기본 설정 값은 Windows Server 2003의 해당 Windows 시간 서비스 레지스트리 항목에서 다른 ](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다.  
  
다음 표에서 각 설정과 연결 된 미리 설정된 된 값은 Windows 시간 서비스와 연결 된 전역 그룹 정책 설정을 나열 합니다. 각 설정에 대 한 자세한 내용은 해당 레지스트리 항목을 참조 하세요. "[Windows 시간 서비스 레지스트리 항목](#w2k3tr_times_tools_uhlp)"이이 주제에서 이전 합니다. 다음 설정은 라고 하는 단일 GPO에 포함 됩니다 **전역 구성 설정을**합니다.  
  
**Windows 시간을 사용 하 여 연결 된 전역 그룹 정책 설정**  
  
|그룹 정책 설정|미리 설정된 된 값|  
|------------------------|------------------|  
|AnnounceFlags|10|  
|EventLogFlags|2|  
|FrequencyCorrectRate|4|  
|HoldPeriod|5|  
|LargePhaseOffset|1280000|  
|LocalClockDispersion|10|  
|MaxAllowedPhaseOffset|300|  
|MaxNegPhaseCorrection|54,000 (15 시간)|  
|MaxPollInterval|15|  
|MaxPosPhaseCorrection|54,000 (15 시간)|  
|MinPollInterval|10|  
|PhaseCorrectRate|7|  
|PollAdjustFactor|5|  
|SpikeWatchPeriod|90|  
|UpdateInterval|100|  
  
다음 표에서 사용 가능한 설정 합니다 **Windows NTP 클라이언트 구성** GPO 및 Windows 시간 서비스와 연결 된 미리 설정된 된 값입니다. 각 설정에 대 한 자세한 내용은 해당 레지스트리 항목을 참조 하세요. "[Windows 시간 서비스 레지스트리 항목](#w2k3tr_times_tools_uhlp)"이이 주제에서 이전 합니다.  
  
**연결 된 Windows 시간 NTP 클라이언트 그룹 정책 설정**  
  
|그룹 정책 설정|기본값|  
|------------------------|-----------------|  
|NtpServer|time.windows.com,0x1|  
|형식|기본 옵션:<br /><br />-   **NTP.** 도메인에 가입 되지 않은 컴퓨터에서 사용 합니다.<br />-   **NT5DS.** 도메인에 가입 된 컴퓨터에서 사용 합니다.|  
|CrossSiteSyncFlags|2|  
|ResolvePeerBackoffMinutes|15|  
|ResolvePeerBackoffMaxTimes|7|  
|SpecialPollInterval|3600|  
|EventLogFlags|0|  
  
## <a name="network-ports-used-by-the-windows-time-service"></a>Windows 시간 서비스에서 사용 되는 네트워크 포트  
Windows 시간 NTP 사양에 모든 시간 동기화 통신에 UDP 포트 123 사용 해야 하는 다음과 같습니다. 이 포트는 Windows 시간에 예약 되어 및 예약 된 유지 항상 합니다. 컴퓨터의 시계 동기화 또는 다른 컴퓨터에는 시간을 제공 될 때마다 해당 통신 UDP 포트 123에서 수행 됩니다.  
  
> [!NOTE]  
> 멀티홈 컴퓨터 라고도 하는 여러 네트워크 어댑터를 사용 하 여 컴퓨터를 보유 하는 경우 네트워크 어댑터에 따라 Windows 시간 서비스를 선택적으로 사용할 수 없습니다.  
  
## <a name="related-information"></a>관련된 정보  
다음 리소스를이 섹션에서는 관련 된 추가 정보를 포함 합니다.  
  
-   RFC *1305* IETF RFC 데이터베이스에서  

