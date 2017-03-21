---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Professional Per Capacity 플랜 사용
{: #using_mobilefoundation_p4}

Professional Per Capacity 플랜을 사용하면 여러 모바일 운영 체제가 있는 모바일 애플리케이션을 수에 관계 없이 원하는 만큼 작성할 수 있습니다.
{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 서비스 인스턴스를 작성한 후 다음 프로시저를 읽고 서비스를 시작하십시오. 

## 전제 조건
{: #prerequisites_p4}

{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 서비스 인스턴스를 구성하기 전에 다음을 고려하십시오. 
* {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity는 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional(OLTP 지원) {{site.data.keyword.Bluemix_notm}} 플랜과 함께 사용하는 경우에만 지원됩니다. 

* {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스의 설정을 구성하려면 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스 신임 정보에 액세스할 수 있어야 합니다. 

**참고**: {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스는 {{site.data.keyword.Bluemix_notm}} `Organization` 또는 액세스 권한이 있는 기타 `Organization`의 모든 `Space`에 존재할 수 있습니다. {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 `Space`에 액세스할 수 있는 권한이 있는지 확인하십시오. 


## 데이터베이스 연결 추가
{: #configure_dashdb_p4}

###  첫 번째 단계
{: #firststeps_p4}

{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 서비스 인스턴스를 작성한 후 프로시저에 따라 시작하십시오. 

### dashDB 서비스 인스턴스에 대한 연결 설정
{: #connect_dashdb_p4}

{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 서비스 인스턴스가 작성된 후에 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스를 연결할 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스에 대한 연결 정보를 지정해야 하는 *Overview* 페이지가 표시됩니다.

**참고:** {{site.data.keyword.dashdbshort_notm}} for Analytics: Enterprise for Transactions 서비스 인스턴스가 이미 있는 경우, 동일한 인스턴스를 사용하여 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 연결하도록 구성할 수 있습니다.

기존 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스가 없는 경우에는 새로 작성할 수 있습니다.

다음 단계에 따라 새로운 dashDB for Transactions 서비스 인스턴스를 작성하십시오. 

1. *Overview* 페이지에서 **새 서비스 작성** 섹션을 선택하십시오.

+ 고가용성 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스를 원하는 경우 **고가용성 구성** 옵션에서 `Yes`를 선택하십시오.

+ 플랜 세부사항을 검토하고 **작성**을 클릭하십시오.

새 {{site.data.keyword.dashdbshort_notm}} for Transactions: EnterpriseForTransactions2.8.500 서비스 인스턴스가 작성되며, 전용 {{site.data.keyword.dashdbshort_notm}} 인스턴스에 8GB RAM과 2vCPU 및 500GB의 스토리지를 제공합니다.

다음 단계에 따라 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스 또는 방금 작성한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스에 연결하십시오. 

1. {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 {{site.data.keyword.Bluemix_notm}} `Organization`을 선택하십시오. 

+ 선택된 `Organization`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `Space`를 선택하십시오.    
**참고:** {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 `Organization`과 `Space`가 나열되지 않는 경우에는 해당 `Organization`과 `Space`의 구성원인지 여부를 확인하십시오. {{site.data.keyword.mobilefoundation_short}} 서비스가 {{site.data.keyword.dashdbshort_notm}} 서비스의 신임 정보에 액세스하므로 조직 및 영역에 대한 *Developer* 역할 액세스 권한을 가져야 합니다.

+ {{site.data.keyword.dashdbshort_notm}} `Service Name` 및 `Credentials`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

+  지정된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 대한 연결을 테스트하십시오.

+  **추가**를 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

잠시 후에는 {{site.data.keyword.mobilefoundation_short}} 서비스를 시작하는 데 도움이 되는 튜토리얼과 동영상을 제공하는 `Overview` 페이지에 액세스할 수 있습니다.

**참고**: 사용자의 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 의해 사용되도록 구성된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스를 변경할 수 없습니다. 그러나 각 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스가 선택된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스 내에 자체 스키마를 작성하므로, 다중 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 걸쳐 동일한 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스를 사용할 수 있습니다.

## MobileFirst 서버 시작
{: #start_mobilefoundation_p4}

* 기본 설정으로 {{site.data.keyword.mfserver_short_notm}}를 시작하려면 **기본 서버 시작**을 클릭하십시오.

* 이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.
    -  각각 1GB 메모리가 있는 두 개의 노드. 이 크기는 개발, 일반적인 테스트 활동, 소규모 프로덕션 워크로드에 충분합니다. 

    -	`username`과 `password`가 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

서버 프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다. 완료되면 대시보드가 표시되며, 여기서 다음을 볼 수 있습니다. 

  -	실행 중인 서버의 상태(상태, 크기). 

  -	사용자가 사용할 수 있도록 서버 라우트가 작성됩니다. 모바일 애플리케이션에서 이 라우트를 사용하여 {{site.data.keyword.mfserver_short_notm}}에 연결하십시오. 

  -	{{site.data.keyword.mfp_oc_short_notm}}에 액세스하기 위한 개인 `username` 및 `password`. `password`는 숨겨집니다. **비밀번호 표시** 아이콘을 클릭하면 볼 수 있습니다. 

*	**콘솔 실행**을 클릭하여 {{site.data.keyword.mfp_oc_short_notm}}을 여십시오.


<!--This console runs inside the container.--> 콘솔을 사용하여 모바일 앱, 어댑터, 모바일 디바이스를 관리하고 서버를 모바일 백엔드로 사용할 수 있으며 푸시 알림 전송 등의 작업을 수행할 수 있습니다. 

##  Mobile Analytics 서버 추가
{: #adding_analytics_server_p4}

 이제 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 Mobile Analytics 서버를 추가하여 {{site.data.keyword.mobilefirst}} 서버에서 모바일 애플리케이션을 모니터링할 수 있습니다. 

 Professional 플랜을 통해 컨테이너 그룹에 Mobile Analytics 서버를 작성하고 컨테이너 그룹에서 컨테이너 노드 수를 선택하여 구성을 사용자 정의할 수 있습니다. 

 데이터를 유지하기 위해 컨테이너에 볼륨도 연결할 수 있습니다. 볼륨을 한 번 선택하면 변경할 수 없습니다. 사용 가능한 기본 파일 공유 영역은 20GB입니다. 사용자가 분석 데이터를 유지할 추가 스토리지 영역이 필요하면 추가 파일 공유를 구매하고 이 파일 공유를 사용하여 볼륨을 작성해야 합니다. 그런 다음 분석 서버를 배치하는 동안 이 새 볼륨을 선택할 수 있습니다.

 {{site.data.keyword.containerlong}}에 볼륨 추가에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 대시보드를 사용하여 볼륨에 지속적 데이터 저장 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/docs/containers/container_volumes_ui.html){: new_window}을 참조하십시오. 

* **분석 추가**를 클릭하여 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 Mobile Analytics 서버를 추가하십시오.

* Mobile Analytics 서버 구성(Analytics 서버에 지원되는 최소 구성은 각각 1GB 메모리가 있는 두 개의 노드)을 선택할 수 있으며 각각 16GM 메모리가 있는 32개의 노드를 가진 최대 구성으로 Analytics 서버를 작성할 수 있습니다. 

프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다.   

* {{site.data.keyword.mfp_oc_short_notm}}에서 MobileFirst Analytics Console을 실행하십시오.

* {{site.data.keyword.mfserver_short_notm}}와 Mobile Analytics 서버 간에 싱글 사인온이 사용됩니다. Mobile Analytics 서버는 {{site.data.keyword.mfserver_short_notm}} 서버와 동일한 LTPA 키 및 사용자 신임 정보를 사용하여 구성합니다. {{site.data.keyword.mfp_oc_short_notm}}에 로그인하는 데 사용한 `username`과 `password`를 사용하여 Mobile Analytics 콘솔에 로그인할 수 있습니다. 

MobileFirst Analytics에 대한 자세한 정보는 [MobileFirst Foundation Operational Analytics ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}을 참조할 수 있습니다. 

**참고:** {{site.data.keyword.mobilefoundation_short}} 서버 인스턴스를 삭제하거나 {{site.data.keyword.mfserver_short_notm}}를 다시 작성하려고 할 때 Mobile Analytics 서버가 제거됩니다.

##  Mobile Analytics 서버 삭제
{: #deleting_analytics_server_p4}

이제 {{site.data.keyword.mobilefoundation_short}} 서비스 대시보드에서 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 추가된 Mobile Analytics 서버를 삭제할 수 있습니다.

* **분석 삭제**를 클릭하여 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 추가된 Mobile Analytics 서버를 삭제하십시오.

 이렇게 하면 분석 컨테이너 그룹이 삭제됩니다. 분석 컨테이너 삭제 프로세스에는 약 10분이 걸립니다. 화면을 새로 고쳐 업데이트된 상태를 볼 수 있습니다. 분석 컨테이너가 삭제되면 **분석 추가** 단추가 다시 사용 가능하게 되고 이 단추를 사용하여 Mobile Analytics 서버를 다시 추가할 수 있습니다(선택하는 경우).

## MobileFirst 서버 재작성
{: #recreate_mobilefoundation_p4}

*	**재작성**을 클릭하여 서버를 재작성하십시오.

* 이 조치는 기존 서버를 중지하고 데이터를 삭제합니다. 업데이트된 버전이 있는 경우 새 서버 인스턴스가 업데이트된 버전으로 작성됩니다. 이 조치를 완료하려면 수 분이 소요됩니다. 

**참고**: 앱과 어댑터에 대한 정보를 포함하여 이전 서버 인스턴스의 모든 데이터가 구성된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에서 유지되며 이 데이터는 서버를 다시 작성하는 데 사용됩니다. 

##	고급 구성 설정
{: #using_mfs_advanced_p4}

`Overview` 페이지에서 **고급 구성으로 서버 시작**을 사용하면 고급 또는 사용자 정의 설정으로 서버를 작성할 수 있습니다. 또한 **구성** 탭을 클릭하여 서버 구성을 사용자 정의할 수 있도록 서버 설정을 업데이트할 수도 있습니다. {{site.data.keyword.mobilefoundation_short}}은 일부 고급 설정에 대한 액세스를 제공합니다.

*	**토폴로지** 탭에서 필요한 서버 크기와 서버 인스턴스의 수를 선택할 수 있습니다. 기본값인 1GB 서버는 개발 및 간단한 테스트에 충분합니다. 
  - 사용자 요구사항에 따라 적절한 서버 크기를 선택하십시오.

  - **노드**는 작성된 노드의 수를 표시합니다. 

      - {{site.data.keyword.mobilefirst}} 서버 팜은 여기서 노드의 수를 구성하여 작성될 수 있습니다. 지원되는 최소 구성은 각각 1GB 메모리가 있는 두 개의 노드이며 지원되는 최대 구성은 각각 16GB 메모리가 있는 32개의 노드입니다. 

세부사항은 [{{site.data.keyword.mobilefoundation_long}} 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}을 참조하십시오. 
