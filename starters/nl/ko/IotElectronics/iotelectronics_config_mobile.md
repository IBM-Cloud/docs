---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 모바일 앱 사용
{: #iot4e_using_mobile}
*마지막 업데이트 날짜: 2016년 6월 14일*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} 모바일 앱을 시작하여 경보를 수신하고 명령을 전송하며 연결된 어플라이언스의 상태를 확인할 수 있는 방법을 확인하십시오.
{:shortdesc}

다음 태스크를 완료하십시오.
1. [모바일 앱을 다운로드하십시오](#iot4e_downloadmobile).
2. [{{site.data.keyword.amafull}}를 구성하십시오](#iot4e_configureMCA).
3. [{{site.data.keyword.iotelectronics}} 환경에 모바일 디바이스를 연결하십시오](#iot4e_connecting_mobile).
4. [모바일 디바이스에서 어플라이언스를 등록하고 제어하십시오](#iot4e_adding_appliance).


 ## 모바일 앱 다운로드
 {: #iot4e_downloadmobile}
 모바일 앱을 가져오려면 Apple 앱 스토어에서 전화기에 이를 다운로드하여 설치하십시오. 전화기에서, 앱 스토어를 열고 "ibm iot"를 검색하십시오. **IBM IoT for Electronics**를 선택하고 설치하십시오.

 또는 [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8)를 사용하여 전화기에 이를 설치할 수 있습니다.

## {{site.data.keyword.amashort}} 구성
{: #iot4e_configureMCA}

모바일 앱을 연결하려면 {{site.data.keyword.amafull}}를 구성해야 합니다.  

  1. {{site.data.keyword.iotelectronics}}의 **연결** 탭에서, {{site.data.keyword.amashort}} 애플리케이션을 여십시오.({{site.data.keyword.Bluemix_notm}} 대시보드에서 애플리케이션에 액세스할 수도 있습니다.)  

    ![{{site.data.keyword.amashort}}를 찾을 방법](images/IoT4E_Connections.svg "{{site.data.keyword.iotelectronics}} 연결")

  2. **사용자 정의** 섹션에서 **구성**을 클릭하십시오.

   ![{{site.data.keyword.amashort}}를 구성하십시오.](images/MCA_config_pg.svg "{{site.data.keyword.amashort}} 인증 페이지 설정")  

  3. 다음 인증 신임 정보를 입력하십시오.
    - **영역 이름**: **myRealm**을 입력하십시오.
    - **URL**: URL을 입력하여 다음 형식으로 {{site.data.keyword.iotelectronics}} 스타터 앱을 식별하십시오. **https://<*myIoT4eStarterApp*>.mybluemix.net**  

      **팁:** URL에 안전한 `https://` 접두부를 사용해야 합니다. **모바일 옵션**을 클릭하여 스타터 앱의 URL을 찾을 수 있습니다.

  ![{{site.data.keyword.amashort}} 사용자 인증 항목입니다.](images/MCA_config_pg2.svg "{{site.data.keyword.amashort}} 사용자 정의 인증 항목")  

  4. 저장하십시오.

## {{site.data.keyword.iotelectronics}} 환경에 모바일 앱 연결
{: #iot4e_connecting_mobile}

모바일 앱에서 시뮬레이션된 디바이스를 보려면 {{site.data.keyword.iotelectronics}} Bluemix 환경에 모바일 앱을 연결해야 합니다.

모바일 앱을 연결하려면 다음 단계에 따르십시오.

  1. 사용자의 컴퓨터에서, {{site.data.keyword.iotelectronics}} 애플리케이션을 시작하고 **앱 보기**를 클릭하여 스타터 앱을 표시하십시오.  

  ![{{site.data.keyword.iotelectronics}} 앱 보기가 강조표시된 시작하기 페이지입니다.](images/IoT4E_getting_started.svg "{{site.data.keyword.iotelectronics}} 앱 보기를 통한 시작하기 페이지")  
  2. **연결된 어플라이언스를 원격으로 제어**를 선택하십시오.

  ![{{site.data.keyword.iotelectronics}} 이용자 앱 체험을 선택하십시오.](images/IoT4E_consumer_app.svg "{{site.data.keyword.iotelectronics}} 이용자 앱 체험")

  3. 하나 이상의 세탁기를 작성하십시오. 세탁기가 작성될 때까지 모바일 앱이 연결할 수 없습니다.

  4.	연결 QR 코드로 화면 이동하여 모바일 디바이스를 통해 이를 스캔하십시오. 연결 QR 코드는 `To connect the app to the environment, you'll be asked to scan this QR Code`로 레이블이 지정된 섹션에 있습니다.

  ![{{site.data.keyword.iotelectronics}} 연결 QR 코드를 스캔하십시오.](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} 연결 QR 코드")

  5. 로그인 신임 정보를 입력하십시오. 사용자 ID와 비밀번호는 길이 제한이 없습니다. 향후 세션을 위해 로그인 신임 정보를 기억하십시오.  

## 모바일 디바이스의 어플라이언스 등록 및 제어
{: #iot4e_adding_appliance}

어플라이언스 상태를 보고 알림을 수신하려면, 모바일 앱을 통해 어플라이언스를 등록해야 합니다.

어플라이언스를 등록하려면 다음 단계를 완료하십시오.

  1. 사용자의 컴퓨터에서, 시뮬레이션된 세탁기로 화면 이동하고 이를 클릭하여 해당 데이터 및 어플라이언스 QR 코드를 표시하십시오.

  ![세탁기를 선택하십시오.](images/IoT4E_mobile_washer_QR.svg "세탁기를 선택하십시오.")

  2.	모바일 디바이스를 통해 세탁기의 QR 코드를 스캔하여 휴대전화에 세탁기를 등록하십시오. 휴대전화에 세탁기 상태가 표시됩니다.

  3. 사용자의 컴퓨터에서 세탁기의 문제점을 선택하십시오(예: 보드 실패 또는 강한 진동). 문제점이 휴대전화에 경보를 전송합니다.
