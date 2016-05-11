---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 샌드박스 및 프로덕션 모드

{: #push-sandboxandproduction-modes}

샌드박스 또는 프로덕션 모드 중 하나에서 푸시 알림을 사용할 수 있습니다. 샌드박스는 서버 애플리케이션 푸시 서비스와 푸시 API 통합을 개발 및 테스트하는 자체 포함된 테스트 환경입니다. 먼저 푸시 대시보드를 사용하여 샌드박스와 프로덕션 모드를 구성합니다. [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}를 사용하여 샌드박스와 프로덕션 간의 푸시 서비스 조작 모드를 전환합니다. 기본적으로 샌드박스 모드가 사용 가능합니다.그러나 모드 간에 전환할 경우 해당 모드 사이에서 태그, 디바이스 및 구독이 공유되지 않습니다. 


애플리케이션을 라이브 환경에 배치할 준비가 된 경우 Push REST API를 사용하여 프로덕션 모드를 선택하십시오. REST API에 대한 자세한 정보는 REST API를 참조하십시오.

푸시 서비스 조작 모드를 샌드박스에서 프로덕션으로 전환하려면 다음을 수행하십시오. 

1. PUT ApplicationID Settings REST API 호출을 사용하십시오. 
2. JSON 본문에서 [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} API 호출을 사용하여 모드가 전환되었는지 확인하십시오. 예상되는 응답은 "mode": "PRODUCTION입니다.
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. 환경 모드가 전환된 후 클라이언트 코드를 다시 실행하여 디바이스를 PRODUCTION 모드로 등록하십시오. 

REST API에 대한 자세한 정보는 REST API를 참조하십시오.
