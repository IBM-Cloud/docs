---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} 스타터 애플리케이션 사용
{: #starter_app}


{{site.data.keyword.geospatialshort_Geospatial}}에는 {{site.data.keyword.Bluemix_short}} 환경을 시험하고 변경사항을 작성하여 푸시하기 위한 템플리트로 사용할 스타터 애플리케이션이 포함되어 있습니다.
{:shortdesc}

스타터 애플리케이션은 Las Vegas 인근에서 이동 중인 시뮬레이션된 디바이스 세트에 대한 데모 MQTT 브로커의 메시지를 사용합니다. 애플리케이션은 오퍼레이션 상태 및 발견한 이벤트에 대한 정보를 단순 웹 페이지에 출력합니다. 


웹 페이지에서 링크되는 Visualizer는 맵의 한 위치에서 다른 위치로 이동하는 디바이스를 모니터합니다. Visualizer는 스타터 애플리케이션에 링크되지 않으므로 스타터 애플리케이션의 사본에 작성된 변경사항의 영향을 받지 않습니다. Node.js로 작성되는 스타터 애플리케이션 코드에서는 REST API를 통해 {{site.data.keyword.geospatialshort_Geospatial}} 서비스를 구성하고 제어하는 방법을 보여줍니다.  


수정하지 않고 스타터 애플리케이션을 실행할 수 있습니다. 서비스를 사용하여 추가로 시험해 보려면 코드를 수정하고 변경사항을 다시 {{site.data.keyword.Bluemix_short}} 환경에 푸시할 수도 있습니다. 
