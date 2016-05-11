# 푸시 서비스 인스턴스 작성
{: #create-push-instance}

{{site.data.keyword.IBM}} {{site.data.keyword.mobilepushshort}}에서 시작하려면 먼저 {{site.data.keyword.Bluemix}} 애플리케이션(예: Node.js 앱)을 작성하십시오. 그런 다음 이 Bluemix 애플리케이션에 바인드하는 데 필요한 푸시 서비스 인스턴스 {{site.data.keyword.mobilepushfull}}를 작성합니다. Bluemix 카탈로그의 Boilerplate 섹션으로 이동하여 MobileFirst 서비스 스타터를 클릭하여 이를 수행할 수도 있습니다. 

**참고**: 환경을 관리하도록 조직을 구성하였으면, 모바일 앱을 위한 런타임과 서비스를 작성하려는 조직을 선택하십시오. 


1. Bluemix 애플리케이션이 없는 경우 작성해야 합니다(예: Node.js 앱). Bluemix 애플리케이션을 작성하려면 Bluemix 대시보드로 이동하여 **앱 작성**을 클릭하십시오. 

	**참고**: 애플리케이션이 있을 경우 7단계로 이동하여 서비스를 추가하십시오. ![서비스 인스턴스 작성](images/create_service_instance1.jpg "서비스 인스턴스 작성")

1. **앱 템플리트 선택**에서 **웹**을 클릭하십시오. 

3. **시작점 선택** 영역에서 **SDK for Node.js**를 선택하고 **계속**을 클릭하십시오. ![시작점](images/create_service_nodejs2.jpg)

4. **영역** 풀다운 메뉴에서 조직 영역을 선택하십시오. ![조직 영역 선택](images/create_a_service3.jpg)
1. **이름**에 앱의 이름을 입력하고 호스트에 호스트의 이름을 입력하십시오. 

1. **선택된 계획** 풀다운 메뉴에서 계획을 선택한 다음 **작성** 단추를 클릭하십시오. 애플리케이션이 스테이징될 때까지 대기하십시오. 

1. **개요** 링크를 클릭하십시오. ![서비스 추가](images/create_service_add4.jpg)
1. **서비스 추가**를 클릭하십시오. CATALOG 화면이 표시됩니다. 

1. **IBM 푸시 알림:**을 선택하고 **Space** 풀다운 메뉴에서 조직을 선택하십시오. ![조직 영역 풀다운 메뉴](images/create_service_org.jpg)
1. **서비스** 이름에 푸시 알림 서비스 이름을 입력하십시오. 

1. **선택된 계획**에서 계획을 선택하고 **작성** 단추를 클릭하십시오. 

1. **예**를 클릭하여 애플리케이션을 다시 스테이징하십시오. ![IBM 푸시 알림 서비스](images/create_service_notification5.jpg)

1. **푸시 알림**을 클릭하여 푸시 알림 대시보드를 표시하십시오. 
