---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 로깅 및 추적
{: #logging_tracing}

*마지막 업데이트 날짜: 2016년 3월 23일*

## 로그 파일
{: #log_files}

messages.log 또는 ffdc 디렉토리와 같은 표준 Liberty 로그는 IBM Bluemix에서 각 애플리케이션 인스턴스의 로그 디렉토리에 있습니다. 이러한 로그는 IBM Bluemix 콘솔에서 액세스하거나 cf logs 및 cf files 명령을 사용하여 액세스할 수 있습니다.
예를 들어, messages.log 파일을 확인하려면 다음 명령을 실행하십시오.
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

로그 레벨 및 다른 추적 옵션은 Liberty 구성 파일을 통해 설정할 수 있습니다. 자세한 정보는 [Liberty 프로파일: 추적 및 로깅](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0)을 참조하십시오. IBM Bluemix 콘솔을 사용하여 실행 중인 애플리케이션 인스턴스에서 추적을 조정할 수도 있습니다. 

## 추적 및 덤프 기능 사용
{: #using_trace_and_dump}

IBM Bluemix 사용자 인터페이스에 추적 및 덤프 기능이 있습니다.
* 실행 중인 애플리케이션 인스턴스에서 Liberty 로깅 traceSpecification을 확인하고 업데이트하려면 추적을 사용하십시오. 
* 실행 중인 애플리케이션 인스턴스에서 스레드 및 힙 덤프를 작성하고 조작하려면 덤프를 사용하십시오. 

이 조치를 수행하려면 사용자 인터페이스에서 Liberty 애플리케이션을 선택하십시오. 왼쪽 탐색 영역의 런타임에서 인스턴스 세부사항을 열 수 있습니다. 인스턴스를 한 개 또는 여러 개 선택합니다. 조치 메뉴 아래에서 추적 또는 덤프를 선택할 수 있습니다.

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
