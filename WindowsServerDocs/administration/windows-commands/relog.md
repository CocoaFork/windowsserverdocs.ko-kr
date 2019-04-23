---
title: relog
description: 성능 카운터 로그 파일에서 성능 카운터 정보를 추출 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7480f6c0-9953-4d70-9b1c-b27e09d8db13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6804c25af04907edc8180b6a37be7efcc470f259
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869364"
---
# <a name="relog"></a>relog

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텍스트 TSV (탭으로 구분 된 텍스트) 용, 텍스트-CSV (쉼표로 구분 된 텍스트) 용, 이진 또는 SQL과 같은 다른 형식으로 성능 카운터 로그에서 성능 카운터를 추출합니다.   

## <a name="syntax"></a>구문  
```  
relog [<FileName> [<FileName> ...]] [/a] [/c <path> [<path> ...]] [/cf <FileName>] [/f  {bin|csv|tsv|SQL}] [/t <Value>] [/o {OutputFile|DSN!CounterLog}] [/b <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/e <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/config {<FileName>|i}] [/q]  
```  

### <a name="parameters"></a>매개 변수  

|매개 변수|설명|
|--|--|
|*FileName* [*FileName...*]|기존 성능 카운터 로그의 경로 이름을 지정합니다. 여러 개의 입력된 파일을 지정할 수 있습니다.|
|-A |출력 파일을 덮어쓰지 않고 추가합니다. 이 옵션을 추가 하는 기본값을 항상은 SQL 형식에 적용 되지 않습니다.  |
|-c *path* [*path ...*]|로그 하는 성능 카운터 경로 지정 합니다. 여러 카운터 경로 지정 하려면 공백으로 구분 하 고 카운터 경로를 따옴표로 묶습니다 (예를 들어, **"* * * Counterpath1* * * Counterpath2 **"**)|  
|-cf *FileName*|다시 기록할 파일에 포함 되어야 하는 성능 카운터를 나열 하는 텍스트 파일의 경로 이름을 지정 합니다. 입력된 파일에 목록 카운터 경로 한 줄씩 하려면이 옵션을 사용 합니다. 기본 설정은 원래 로그 파일에 있는 모든 카운터 다시 로그 된입니다.|  
|-f {bin\| csv\|tsv\|SQL}|출력 파일 형식의 경로 이름을 지정합니다. 기본 형식은 **bin**합니다. SQL 데이터베이스에 대 한 출력 파일에 지정 된 *DSN! CounterLog*합니다. DSN (데이터베이스 시스템 이름)을 구성 하는 ODBC 관리자를 사용 하 여 데이터베이스 위치를 지정할 수 있습니다.  |
|-t *값*|샘플 간격에 지정 "*N*" 레코드입니다. 다시 기록할 파일에 모든 n 번째 데이터 요소를 포함합니다. 기본값은 모든 데이터 요소입니다.|  
|-o {*OutputFile* \| *"SQL:DSN! Counter_Log*} DSN가 ODMC DSN이 시스템에 정의 합니다.|SQL 데이터베이스 카운터 쓸 위치 또는 출력 파일의 경로 이름을 지정 합니다. <br>참고: ODBC 데이터 원본에 DSN을 정의 해야 Relog.exe의 64 비트 및 32 비트 버전 (64 비트 및 32 비트 각각)|
|-b \<*M*/*D*/*YYYY*> [[*HH*:]*MM*:]*SS*|지정 시간 입력된 파일에서 첫 번째 레코드를 복사 하기 위한 시작 합니다. 날짜 및 시간에 정확한 형식으로 묶어야 *M***/*** D***/*** YYYYHH ***:*** MM ***:*** SS*.|  
|-e \<*M*/*D*/*YYYY*> [[*HH*:]*MM*:]*SS* |입력된 파일에서 마지막 레코드를 복사 하기 위한 종료 시간을 지정 합니다. 날짜 및 시간에 정확한 형식으로 묶어야 *M***/*** D***/*** YYYYHH ***:*** MM ***:*** SS*.|  
|-config {*FileName* \| *i*}|명령줄 매개 변수를 포함 하는 설정 파일의 경로 이름을 지정 합니다. 사용 하 여 *-i* 명령줄에 배치할 수 있는 입력된 파일의 목록에 대 한 자리 표시자로 구성 파일에 있습니다. 그러나 명령줄에서 필요가 없습니다 사용 하 여 *i*합니다. 또한 여러 입력된 파일 이름을 지정 하려면 *.blg와 같은 와일드 카드를 사용할 수 있습니다.|  
|-q|성능 카운터와의 시간 범위 입력된 파일에 지정 된 파일에 로그를 표시 합니다.|  
|-y|모든 질문에 "yes" 응답 하 여 확인 메시지를 무시 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명  
카운터 경로 형식:  
-   일반 카운터 경로의 형식은 다음과 같습니다: [\\\<컴퓨터 >] \\ \<개체 > [\<부모 >\\< 인스턴스 #Index >] \\ \< 카운터 >]는 올바른 이름이 나 와일드 카드 문자는 부모, 인스턴스, 인덱스 및 형식의 카운터 구성 요소 포함 될 수 있습니다 위치 합니다. 컴퓨터, 부모, 인스턴스 및 인덱스 구성 요소에 대 한 모든 카운터 필요 하지 않습니다.  
-   카운터 자체에 따라 사용 하 여 카운터 경로 확인 합니다. 예를 들어 LogicalDisk 개체는 인스턴스 <Index>, 이므로 < #index > 또는 와일드 카드를 제공 해야 합니다. 따라서 다음 형식을 사용할 수 있습니다: **\LogicalDisk (\*/\*#\*)\\\***  
-   프로세스 개체 비교에서 인스턴스를 필요로 하지 않는 \<인덱스 >. 따라서 다음 형식을 사용할 수 있습니다: **\Process (\*) \ID 프로세스**  
-   와일드 카드 문자를 부모 이름을 지정 하는 경우 지정 된 인스턴스 및 카운터 필드와 일치 하는 지정된 된 개체의 모든 인스턴스가 반환 됩니다.  
-   인스턴스 이름에 와일드 카드 문자 지정을 지정 된 인덱스에 해당 하는 모든 인스턴스 이름이 와일드 카드 문자를 일치 하는 경우 지정 된 개체와 부모 개체의 모든 인스턴스가 반환 됩니다.  
-   카운터 이름에 와일드 카드 문자는 지정 하는 경우 지정된 된 개체의 모든 카운터 반환 됩니다.  
-   부분적인 카운터 경로 문자열에 일치 항목 (예를 들어 pro *) 지원 되지 않습니다.  

카운터 파일:  
-   카운터 파일은 하나 이상의 기존 로그에서 성능 카운터를 나열 하는 텍스트 파일입니다. 로그에서 전체 카운터 이름을 복사 또는 **/q** 출력 \<컴퓨터 >\\\<개체 >\\\<인스턴스 >\\ \< 카운터 > 형식입니다. 각 줄에 하나의 카운터 경로 나열 합니다.  

카운터를 복사 합니다.  
-   를 실행 하면 **다시 기록할** 복사본에서에서 지정 된 카운터 모든 레코드는 입력된 파일에 필요한 경우 형식으로 변환 합니다. 와일드 카드 경로 카운터 파일에 허용 됩니다.  
입력된 파일 하위 집합 저장:  
-   사용 하는 **/t** 입력된 파일에 삽입 되도록 지정 하려면 매개 변수 출력 파일의 간격 마다 <n>번째 레코드입니다. 기본적으로 데이터는 모든 레코드에서 다시 로그 됩니다.  
사용 하 여 **/b** 및 **/e** 로그 파일과 함께 매개 변수  
-   출력 로그가 전에 레코드를 포함 시작 시간을 지정할 수 있습니다 (즉, **/b**) 형식이 지정 된 값의 계산 값을 필요로 하는 카운터에 대 한 데이터를 제공 하도록 합니다. 출력 파일 타임 스탬프를 사용 하는 입력된 파일에서 마지막 레코드를 갖게 됩니다 보다 작은 **/e** (즉, 종료 시간) 매개 변수입니다.  
사용 하 여 **/config** 옵션:  
-   함께 사용 하는 설정 파일의 내용을 **/config** 옵션에는 다음과 같은 형식을 가져야 합니다.  
    -   \<CommandOption >\\\<값 >, 여기서 \<CommandOption > 명령줄 옵션 및 \<값 >의 값을 지정 합니다.

통합 하는 방법에 대 한 자세한 내용은 **relog** 에서 Windows Management Instrumentation (WMI) 스크립트로 "WMI 스크립팅"을 참조 합니다 [Microsoft Windows Resource Kit 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=4665)합니다.  

## <a name="BKMK_Examples"></a>예제  
고정된 간격 30에서 기존 추적 로그를 다시 샘플링 하 고, 카운터 경로 나열 하 고, 출력 파일 및 형식:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.csv /t 30 /f csv  
```  
기존 추적 로그를 다시 샘플링 30 일정 한 간격, 카운터 경로 및 출력 파일을 나열 합니다.  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.blg /t 30  
```
기존 추적을 다시 샘플링 하려면 데이터베이스에 로그인 합니다.
```
relog "c:\perflogs\daily_trace_log.blg" -f sql -o "SQL:sql2016x64odbc!counter_log"
```

## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
<!---
-   The following is a list of the possible formats:  
    -   \<computer>\\\<Object>(\<Parent>/\<Instance#Index>)\<Counter>  
    -   \<computer>\<Object>(<Parent>/<Instance>)\\<Counter>  
    -   \\\\<computer>\\<Object>(<Instance#Index>)\\<Counter>  
    -   \\\\<computer>\\<Object>(<Instance>)\\<Counter>  
    -   \\\\<computer>\\<Object>\\<Counter>  
    -   \\<Object>(<Parent>/<Instance#Index>)\\<Counter>  
    -   \\<Object>(<Parent>/<Instance>)<Counter>  
    -   \\<Object>(<Instance#Index>)\\<Counter>  
    -   \\<Object>(<Instance>)\\<Counter>  
    -   \\<Object>\\<Counter>  
--->