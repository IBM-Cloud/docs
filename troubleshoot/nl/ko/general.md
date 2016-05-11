---

copyright:
  years: 2015, 2016

---


{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# 일반 서비스 문제점
{: #general}

*마지막 업데이트 날짜: 2015년 12월 9일*

{{site.data.keyword.Bluemix}} 서비스 문제점으로는 서비스 인스턴스를 삭제할 때 발생하는 게이트웨이 제한시간 초과 오류가 있습니다. 그러나 대부분의 경우 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}

## 서비스 인스턴스를 삭제하면 게이트웨이 제한시간 초과 오류 메시지가 표시됨
{: #ts_service_broker}

클라우드 제어기에서 이미 삭제된 서비스 인스턴스를 삭제하려고 할 경우 오류 메시지가 표시될 수 있습니다.
{:shortdesc}


서비스 인스턴스를 삭제하려고 할 때 ```게이트웨이 제한시간 초과```라는 서비스 브로커 오류 메시지가 표시됩니다.
{: tsSymptoms}


이 문제점은 서비스 인스턴스가 클라우드 제어기에서 이미 삭제된 경우에 발생합니다.
{: tsCauses}


이 문제점을 해결하려면 동일한 서비스 이름으로 서비스 인스턴스를 작성한 다음 이 인스턴스를 애플리케이션에 바인딩하십시오. 그러면 해당 서비스에서 사용하는 서비스 인스턴스와 애플리케이션을 삭제할 수 있습니다.    
{: tsResolve}


