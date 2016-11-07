---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 모바일 연결 및 보안 구성
{: #iot4e_configureMCA}

*마지막 업데이트 날짜: 2016년 9월 19일*
{: .last-updated}

{{site.data.keyword.amafull}}를 구성하여 모바일 통신 및 보안을 사용 가능하게 설정합니다. 이 태스크는 샘플 모바일 앱을 사용하는 데 필요하며 한 번만 수행하면 됩니다.
{:shortdesc}

## 시작하기 전에

시작하기 전에 다음 태스크를 완료해야 합니다.
  - {{site.data.keyword.Bluemix_notm}} 조직에 {{site.data.keyword.iotelectronics}} 스타터의 인스턴스를
배치하십시오. 스타터의 인스턴스를 배치하면 {{site.data.keyword.amafull}}를 포함하여 해당 컴포넌트 애플리케이션 및 서비스가 자동으로 배치됩니다. 

  - 구성 프로세스는 사용하는 {{site.data.keyword.Bluemix_notm}} 콘솔 버전에 따라 조금씩 다르므로 해당 버전에 대한 지시사항을 읽어야 합니다. 

  다음 옵션을 찾아 사용 중인 버전을 판별할 수 있습니다. 
    - [새 {{site.data.keyword.Bluemix_notm}}](#configMCAnew). 새 {{site.data.keyword.Bluemix_notm}} 인터페이스를 사용 중인 경우 대시보드의 헤더 섹션에 **기존 인터페이스 사용** 옵션이 표시됩니다.
    - [기존 {{site.data.keyword.Bluemix_notm}}](#configMCAclassic). 기존 {{site.data.keyword.Bluemix_notm}} 인터페이스를 사용 중인 경우, 헤더 섹션에 **새 Bluemix 시도** 옵션이 표시됩니다. 

## 새 {{site.data.keyword.Bluemix_notm}} 인터페이스에서 {{site.data.keyword.amashort}} 구성
{: #configMCAnew}

  1. {{site.data.keyword.iotelectronics}} 스타터를 배치하여 스타터 앱의 시작하기 탭이 표시되면 이러한 지시사항의 다음 단계로 진행해야 합니다. 스타터 앱이 표시되지 않으면, {{site.data.keyword.Bluemix_notm}} 대시보드를 열고 스타터 애플리케이션 타일을 클릭하여 {{site.data.keyword.iotelectronics}} 스타터 애플리케이션을 시작하십시오. 

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스](images/IoT4E_bm_dashboard.png "대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스")

  2. **연결** 탭에서 {{site.data.keyword.amashort}} 서비스를 클릭하여 여십시오. 

    ![{{site.data.keyword.amashort}}를 찾는 방법](images/IoT4E_Connections.png "{{site.data.keyword.iotelectronics}} 연결")

  3. **인증 설정** 페이지에서 **모바일 옵션**을 클릭하여 사용하는 {{site.data.keyword.iotelectronics}} 스타터 앱의 URL을 찾으십시오. **라우트** 필드에 있는 URL을 복사하십시오. 

    ![{{site.data.keyword.amashort}} 모바일 옵션](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} 모바일 옵션")  

  4. ****인증 설정 페이지의 사용자 정의 섹션**에서 **구성**을 클릭하십시오.

       ![{{site.data.keyword.amashort}} 구성](images/MCA_config_pg.png "{{site.data.keyword.amashort}} 인증 설정 페이지")  

  5. 다음 인증 신임 정보를 입력한 후 **저장**을 클릭하십시오.
    - **영역 이름**: **myRealm**을 입력하십시오.
    - **사용자 정의 ID 제공자 URL**: 앞에서 복사한 URL을 입력하여 {{site.data.keyword.iotelectronics}} 스타터 앱을 다음 형식으로 식별하십시오. **https://<*myIoT4eStarterApp*>.mybluemix.net**
    - **웹 애플리케이션 경로 재지정 URI**: 이 필드는 비워 두십시오.

      ![{{site.data.keyword.amashort}} 사용자 인증 항목입니다.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} 사용자 정의 인증 항목")  

  6. 헤더 섹션에 있는 스타터 앱의 이름을 클릭하여 {{site.data.keyword.iotelectronics}} 스타터 콘솔의 연결 탭으로 돌아가십시오. 

   ![{{site.data.keyword.amashort}} 이동 경로](images/MCA_breadcrumb.png "{{site.data.keyword.amashort}} 이동 경로")

## 기존 {{site.data.keyword.Bluemix_notm}} 인터페이스에서 {{site.data.keyword.amashort}} 구성
{: #configMCAclassic}

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 스타터 애플리케이션 타일을 클릭하여 {{site.data.keyword.iotelectronics}} 스타터 애플리케이션을 시작하십시오. 

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 기존](images/IoT4E_bm_dashboard_c.png "대시보드의 {{site.data.keyword.iotelectronics}}, 기존")

2. {{site.data.keyword.iotelectronics}}의 인스턴스에서 {{site.data.keyword.amashort}} 서비스를 클릭하여 여십시오.   

  ![{{site.data.keyword.amashort}}를 찾는 방법](images/IoT4E_Connections_c.png "{{site.data.keyword.iotelectronics}} 연결")

2. **인증 설정** 페이지에서 **모바일 옵션**을 클릭하여 사용하는 {{site.data.keyword.iotelectronics}} 스타터 앱의 URL을 찾으십시오. **라우트** 필드에 있는 URL을 복사하십시오. 

  ![{{site.data.keyword.amashort}} 모바일 옵션](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} 모바일 옵션")  

3. ****인증 설정 페이지의 사용자 정의 섹션**에서 **구성**을 클릭하십시오.

 ![{{site.data.keyword.amashort}} 구성](images/MCA_config_pg.png "{{site.data.keyword.amashort}} 인증 설정 페이지")  

4. 다음 인증 신임 정보를 입력한 후 **저장**을 클릭하십시오.
   - **영역 이름**: **myRealm**을 입력하십시오.
   - **사용자 정의 ID 제공자 URL**: 앞에서 복사한 URL을 입력하여 {{site.data.keyword.iotelectronics}} 스타터 앱을 다음 형식으로 식별하십시오. **https://<*myIoT4eStarterApp*>.mybluemix.net**
   - **웹 애플리케이션 경로 재지정 URI**: 이 필드는 비워 두십시오.

    ![{{site.data.keyword.amashort}} 사용자 인증 항목입니다.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} 사용자 정의 인증 항목")  

5. 다음과 같은 방법으로 {{site.data.keyword.iotelectronics}} 스타터 콘솔의 연결 탭으로 돌아가십시오. 
  1. 헤더 섹션에서 **대시보드로 돌아가기** 옵션 옆에 있는 이중 화살표를 클릭하여 메뉴를 표시하십시오. 
  2. **개요**를 클릭하여 스타터 콘솔로 돌아가십시오.   

    ![{{site.data.keyword.amashort}} 이동 경로](images/MCA_breadcrumb_c.png "{{site.data.keyword.amashort}} 이동 경로")
