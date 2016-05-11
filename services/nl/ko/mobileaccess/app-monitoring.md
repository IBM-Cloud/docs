---

copyright:
  years: 2015, 2016
  
---

# 애플리케이션 모니터링
{: #app-monitoring}

{{site.data.keyword.amafull}}는 보안 기능 이외에도 모바일 애플리케이션에 대한 모니터링 및 분석을 제공합니다.
{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 클라이언트 로그 및 모니터 데이터를 기록할
수 있습니다. 개발자는 이 데이터를 {{site.data.keyword.amashort}} 서비스로 전송할 시기를
제어할 수 있습니다. {{site.data.keyword.amashort}} 서비스에서 발생하는 모든 보안 이벤트(예:
인증 성공 또는 실패)는 자동으로 로깅됩니다. 

데이터가 {{site.data.keyword.amashort}}에 전달되면 {{site.data.keyword.amashort}}
모니터링 대시보드를 사용하여 모바일 애플리케이션, 디바이스 및 클라이언트 로그에 대한 분석 정보를 얻을
수 있습니다. 기본적으로 애플리케이션이
{{site.data.keyword.amashort}}에서 보호되는 자원에 대해 작성하는 요청에 대한 정보가
기록됩니다.

자동으로 기록되는 데이터에는 인증, 새 디바이스 및 새 사용자 수와 같은 정보가 포함됩니다.
또한 다음 정보를 보고하도록 {{site.data.keyword.amashort}} 클라이언트 SDK를 구성할 수 있습니다. 

### 모바일 애플리케이션의 사용 통계
{: #usage-stats}

몇 번의 단순 API 호출로 애플리케이션 라이프사이클 이벤트를 기록하고 기록된 데이터를 {{site.data.keyword.amashort}}
서비스로 전송하도록 모바일 애플리케이션을 구성할 수 있습니다. 앱 열림,
수신된 푸시 알림의 수 등을 기록할 수 있습니다. 

### 클라이언트측 로그 캡처
{: #client-side-logcapture}

실제 사용되는 애플리케이션에는 때때로 수정하는 데 개발자의 노력이 필요한 문제점이 발생하기도 합니다.
이러한 문제점을 다시 만들어 내기는 어렵습니다. <!--in R&D.--> 코드를 작업한 개발자는 문제를 테스트할 수 있는 환경이나 정확한 디바이스가
부족할 수 있습니다. 이러한 경우, 로그가 작성되는 환경에서 문제가 발생한 경우라 클라이언트 디바이스에서 디버그 로그를 검색하는 것이
도움이 됩니다. 

## 캡처한 데이터 보존
{: #preserve-captureddata}

캡처한 모든 데이터를 클라이언트측에 보존할 수 있는 방법은 없습니다. 사용자가
오프라인에서 모바일 애플리케이션을 실행하고 동시에 캡처한 분석 및 로그 데이터를 누적할 수 있습니다.
클라이언트가 오프라인인 경우 파일 시스템 공간에 제한이 있기 때문에, 이전에 로그된 이벤트는 더 최근에 로그된
이벤트를 유지하기 위해 영구 제거해야 합니다. 개발자가 제공된 API를 사용하여 캡처한 데이터를
{{site.data.keyword.amashort}} 서비스로 전송할 시기를 결정해야 합니다. 

## {{site.data.keyword.amashort}} 모니터링 대시보드 사용
{: #monitoring-dashboard}

1. {{site.data.keyword.Bluemix}} 대시보드를 열고 {{site.data.keyword.Bluemix_notm}}
애플리케이션을 클릭하십시오. 

2. {{site.data.keyword.Bluemix_notm}} 애플리케이션 대시보드가 열려 있는 경우 {{site.data.keyword.amashort}}
타일을 클릭하십시오. 

3. {{site.data.keyword.amashort}} 대시보드의 왼쪽 메뉴에서 `모니터링` 링크를 클릭하십시오. 

## 다음 단계
{: #next-steps}
* [로거 활성화, 구성 및 사용](app-monitoring-logger.html)
* [사용량 분석 수집](app-monitoring-gathering-analytics.html)
