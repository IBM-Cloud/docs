---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 모바일 앱 사용
{: #iot4e_using_mobile}
*마지막 업데이트 날짜: 2016년 9월 19일*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} 모바일 앱을 시작하여 경보를 수신하고 명령을 전송하며 연결된 어플라이언스의 상태를 확인할 수 있는 방법을 확인하십시오.
{:shortdesc}

## 시작하기 전에

모바일 앱을 사용하려면 먼저 다음 태스크를 완료해야 합니다.
  - {{site.data.keyword.Bluemix_notm}} 조직에 {{site.data.keyword.iotelectronics}} 스타터의 인스턴스를
배치하십시오. 스타터의 인스턴스를 배치하면 스타터의 컴포넌트 애플리케이션 및 서비스가 자동으로 배치됩니다. 
  - {{site.data.keyword.amafull}}를 구성하여 [모바일 통신 및 보안을 사용](iotelectronics_config_mca.html) 가능하게 설정하십시오. 

## 모바일 앱 시작하기
모바일 앱을 시작하려면 다음 태스크를 완료하십시오.
1. 사용하는 모바일 디바이스로 [모바일 앱을 다운로드](#iot4e_downloadmobile)하십시오.
2. [모바일 앱을 {{site.data.keyword.iotelectronics}} 환경에 연결](#iot4e_connecting_mobile)하고 어플라이언스를 등록하십시오.


 ### 모바일 앱 다운로드
 {: #iot4e_downloadmobile}
 모바일 앱을 가져오려면 Apple 앱 스토어에서 전화기에 이를 다운로드하여 설치하십시오. 전화기에서, 앱 스토어를 열고 "ibm iot"를 검색하십시오. **IBM IoT for Electronics**를 선택하고 설치하십시오.

 또는 [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8)를 사용하여 전화기에 이를 설치할 수 있습니다.


### 모바일 앱 연결
{: #iot4e_connecting_mobile}

사용하는 환경에 모바일 앱을 연결하고 어플라이언스를 등록하려면 다음 태스크를 수행하십시오. 

1. {{site.data.keyword.itoelectronics}} 스타터 앱을 여십시오. 지시사항은 [스타터 앱 열기](iot4ecreatingappliances.html#iot4e_openAppMain)를 참조하십시오. 

2. **연결된 어플라이언스를 원격으로 제어**를 선택하십시오.

    ![{{site.data.keyword.iotelectronics}} 스타터 인터페이스](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} 스타터 인터페이스")

3. **다음, 시뮬레이션된 새 세탁기 선택 또는 추가**로 레이블 지정된 섹션으로 화면 이동한 후 추가(+) 아이콘을 클릭하여 하나 이상의 세탁기를 작성하십시오. 새 세탁기가 작성됩니다.

    ![세탁기 추가](images/IoT4E_add_washer.png "세탁기 추가")

4.	연결 QR 코드로 화면 이동하여 모바일 디바이스를 통해 이를 스캔하십시오. 연결 QR 코드는 **앱을 환경에 연결하기 위해 이 QR 코드를 스캔하도록 요청됩니다.**로 레이블이 지정된 섹션에 있습니다.

  ![연결 QR 코드](images/iot4e_mobile_connect_QR.png "{{site.data.keyword.iotelectronics}} 연결 QR 코드")

5. 모바일 디바이스에서 로그인 신임 정보를 입력하십시오. 사용자 ID와 비밀번호는 길이 제한이 없습니다. 향후 세션을 위해 로그인 신임 정보를 기억하십시오. 이제 모바일 디바이스가 {{site.data.keyword.iotelectronics}} 환경에 등록되었으므로 개별 어플라이언스를 등록할 수 있습니다. 

6. 사용자의 컴퓨터에서, 시뮬레이션된 세탁기로 화면 이동하고 이를 클릭하여 해당 데이터 및 어플라이언스 QR 코드를 표시하십시오.

  ![세탁기를 선택하십시오.](images/IoT4E_mobile_washer_QR.png "세탁기를 선택하십시오.")

7.	모바일 디바이스를 사용하여 세탁기의 QR 코드를 스캔하십시오. 이제 세탁기가 등록되었으므로 휴대전화에 세탁기 상태 메시지가 표시됩니다. 

#### 다음 항목
이제 모바일 디바이스를 사용하여 경보를 보고 세탁기를 제어할 수 있습니다. 다음 단계를 수행하여 시도해 보십시오. 
  - 사용자의 컴퓨터에서 세탁기의 문제점을 선택하십시오(예: 보드 실패 또는 강한 진동). 문제점이 휴대전화에 경보를 전송합니다.
  - 모바일 디바이스에서 **세탁 시작**을 클릭하여 세탁기를 시작하십시오. 각 세탁 사이클이 진행됨에 따라 컴퓨터에 세탁기 상태 변화가 표시됩니다. 
