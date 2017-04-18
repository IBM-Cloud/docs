---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 모바일 연결 및 보안 구성
{: #iot4e_configureMCA}

{{site.data.keyword.amafull}}를 구성하여 모바일 통신 및 보안을 사용 가능하게 설정합니다. 이 태스크는 샘플 모바일 앱을 사용하는 데 필요하며 한 번만 수행하면 됩니다.
{:shortdesc}

시작하기 전에 사용자의 {{site.data.keyword.Bluemix_notm}} 조직에 {{site.data.keyword.iotelectronics}} 스타터의 인스턴스를 배치해야
 합니다. 스타터의 인스턴스를 배치하면 {{site.data.keyword.amafull}}를 포함하여 해당 컴포넌트 애플리케이션 및 서비스가 자동으로 배치됩니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iotelectronics}} 애플리케이션을 여십시오.

   **팁:** 애플리케이션은 {{site.data.keyword.Bluemix_notm}} 대시보드의 애플리케이션 섹션에 있습니다. 라우트가 아닌 이름을 클릭하십시오.

    ![대시보드의 {{site.data.keyword.iotelectronics}}](images/IoT4E_bm_dashboard.svg "대시보드의 {{site.data.keyword.iotelectronics}}")

2. **앱 보기**를 마우스 오른쪽 단추로 클릭하고 **링크 위치 복사**를 선택하여 {{site.data.keyword.iotelectronics}} 웹 앱의 URL을 복사하십시오. 

3. **연결** 탭에서 {{site.data.keyword.amashort}} 서비스를 클릭하여 여십시오. 

3. {{site.data.keyword.amashort}} 인증 페이지에서 **설정**을 클릭하여 인증을 사용으로 설정하십시오. 

4. **사용자 정의** 섹션에서 다음 인증 신임 정보를 입력하십시오. 

    - **영역 이름**: `myRealm`

    - **사용자 정의 ID 제공자 URL**: 첫 번째 단계에서 복사한 다음 형식의 API 애플리케이션의 URL을 붙여넣기하십시오. **https://<*myIoT4eStarterApp*>.mybluemix.net** 

    **중요:** 복사한 값에 `http`가 있는 경우에도 URL에 보안 프로토콜 `https`를 사용해야 합니다. 

    - **웹 애플리케이션 경로 재지정 URI**: 이 필드는 공백으로 두십시오. 

   ![{{site.data.keyword.amashort}}를 구성하십시오.](images/MCA_config_pg.svg "{{site.data.keyword.amashort}} 인증 페이지")

5. 설정을 저장하십시오. 이제 {{site.data.keyword.iotelectronics}} 서비스 콘솔 또는 {{site.data.keyword.Bluemix_notm}} 콘솔로 돌아갈 수 있습니다. 
