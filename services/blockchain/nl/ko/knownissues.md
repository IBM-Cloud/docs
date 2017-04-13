---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN 알려진 문제
{: #etn_overview}



다음 HSBN 플랜 문제가 보고되었습니다. 

1. Hyperledger Fabric v0.6.1을 활용하는 고급 보안 비즈니스 네트워크 사용 시, 50개 이상의 체인코드 배치가 있는 경우 개발 단계 중에 주기적으로 네트워크를 재설정하도록 권장합니다. 네트워크를 재설정하면 배치된 체인코드와 수집된 데이터가 제거됩니다. 이를 통해 반복적 개발 단계에서 발생한 개선사항에 의해 대체되는 오래된 체인코드를 제거할 수 있습니다. 사후 개발 단계인 경우에는 체인코드 배치 수를 모니터하여 가장 중요한 체인코드를 사용하기 위한 용량을 남겨두어야 합니다. 
2. 네트워크 및 피어의 상태를 조회할 때 "503 Service Unavailable" 및 "502 Bad Gateway" 오류가 산발적으로 수신됩니다. 
3. vp1 로그에 "Server.Serve failed to complete security handshake" 메시지가 표시될 수 있습니다. 이는 심각하지 않은 오류이며 네트워크 오퍼레이션과 무관합니다. 
4. **서비스 신임 정보**가 자체적으로 작성되지 않을 수 있습니다. 이 경우, 다음과 같이 신임 정보를 생성하십시오. 

 a) 서비스 대시보드에서 **서비스 신임 정보** 탭을 클릭하십시오.

  ![서비스 신임 정보 HSBN](images/hsbn.png "서비스 신임 정보 HSBN")

 b) **서비스 신임 정보** 탭에서 **새 신임 정보** 단추를 클릭하십시오.

  ![새 신임 정보 HSBN](images/hsbn1.png "새 신임 정보 HSBN")

c) **새 신임 정보 추가**라는 새 창이 표시됩니다. 이 창 맨 아래의 **추가** 단추를 클릭하십시오. 

  ![새 신임 정보 추가 HSBN](images/hsbn2.png "새 신임 정보 추가 HSBN")

 d) 이제 다음 예와 비슷한 화면이 표시됩니다. **신임 정보 보기**를 클릭하면 HSBN 인스턴스의 서비스 신임 정보가 포함된 JSON 페이로드가 표시됩니다.   

  ![신임 정보 생성 HSBN](images/hsbn3.png "신임 정보 생성")


## 도움 받기

IBM Blockchain on Bluemix 네트워크에 대한 지원 및 도움은 [지원 받기](ibmblockchain_support.html)를 참조하십시오.
