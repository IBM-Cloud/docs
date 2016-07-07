---

copyright:
  years: 2016

---

#	Professional 1 Application 플랜 사용
{: #using_mobilefoundation_p2}

*마지막 업데이트 날짜: 2016년 6월 15일*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스 인스턴스를 작성한 후에 다음 프로시저를 읽고 서비스를 시작합니다.

## 전제 조건
{: #prerequisites_p2}

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스 인스턴스를 구성하기 전에 다음을 고려하십시오.
* {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application은 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional(OLTP 지원) {{site.data.keyword.Bluemix_notm}} 플랜과 함께 사용하는 경우에만 지원됩니다.

* {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스 설정을 구성하기 전에 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스 및 신임 정보를 사용할 수 있어야 합니다.

**참고**: {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스는 {{site.data.keyword.Bluemix_notm}} `조직` 내의 임의의 `영역`에 존재할 수 있습니다.{{site.data.keyword.mobilefoundation_short}} 서비스를 {{site.data.keyword.dashdbshort_notm}} 서비스가 존재하는 영역이 아닌 다른 {{site.data.keyword.Bluemix_notm}} `영역`에 배치하도록 선택한 경우 {{site.data.keyword.dashdbshort_notm}} 서비스에 액세스할 수 있는 권한이 있는지 확인해야 합니다. 


## 데이터베이스 연결 추가
{: #configure_dashdb_p2}

###  첫 번째 단계
{: #firststeps_p2}

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스 인스턴스를 작성한 후에 {{site.data.keyword.mfp_full_notm}} V8.0에 대한 라이센스 조항에 동의하여 시작하십시오. 

### {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 대한 연결 설정
{: #connect_dashdb_p2}

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스 인스턴스가 작성된 후에 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 서비스 인스턴스에 대한 연결 정보를 지정하는 데 필요한 *개요* 페이지가 표시됩니다.

1.  현재 `조직`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `영역`을 선택하십시오. 

+ {{site.data.keyword.dashdbshort_notm}} `서비스 이름` 및 `신임 정보`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

+  지정된 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 서비스 인스턴스에 대한 연결을 테스트하십시오.

+  **계속**을 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

**참고**: 사용자의 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 의해 사용되도록 구성된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스를 변경할 수 없습니다. 그러나 각 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스가 선택된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스 내에 자체 스키마를 작성하므로, 다중 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 걸쳐 동일한 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스를 사용할 수 있습니다.

* 잠시 후에는 {{site.data.keyword.mobilefoundation_short}} 서비스를 시작하는 데 도움이 되는 학습서 및 비디오를 제공하는 `개요` 페이지에 액세스할 수 있습니다.

## {{site.data.keyword.mobilefirst}} 서버 시작
{: #start_mobilefoundation_p2}

* 기본 설정으로 {{site.data.keyword.mfserver_short_notm}}를 시작하려면 **기본 서버 시작**을 클릭하십시오.

* 이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.
    -  1GB 메모리 및 64GB 스토리지. 이 크기는 개발 및 일반적인 테스트 활동에 충분합니다.

    -	`username` 및 `password`가 사용자를 위해 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

서버 프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다. 완료되면 대시보드가 표시되며, 여기서 다음을 볼 수 있습니다. 

  -	실행 중인 서버의 상태(상태, 크기, 스토리지). 

  -	사용자를 위해 작성된 서버 라우트. 이 라우트를 사용하여 공용 인터넷에서 모바일 서버에 접속할 수 있습니다. 모바일 애플리케이션은 해당 라우트를 사용하여 서버에 액세스합니다. 

  -	{{site.data.keyword.mfp_oc_short_notm}}에 액세스하기 위한 개인 `사용자 이름`` 및 `비밀번호`. `비밀번호는 숨겨집니다.  **비밀번호 표시**를 클릭하여 이를 볼 수 있습니다. 

*	**콘솔 실행**을 클릭하여 {{site.data.keyword.mfp_oc_short_notm}}을 여십시오.


이 콘솔이 컨테이너 내에서 실행됩니다. 콘솔을 사용하여 모바일 앱 및 모바일 디바이스를 관리하고 서버를 모바일 백엔드로 사용하고 푸시 알림을 전송하는 등의 작업을 수행할 수 있습니다.

## {{site.data.keyword.mobilefirst}} 서버 재작성
{: #recreate_mobilefoundation_p2}

*	**재작성**을 클릭하여 서버를 재작성하십시오.

* 이 조치는 기존 서버를 중지하고 이를 삭제합니다. 새 서버 인스턴스가 작성됩니다. 이 조치를 완료하려면 수 분이 소요됩니다. 

**참고**: 앱 및 어댑터에 대한 정보를 포함하여 이전 서버 인스턴스의 모든 데이터가 구성된 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에서 지속되며 서버를 재작성한 후에도 이러한 데이터를 사용할 수 있습니다. 

##	고급 구성 설정
{: #using_mfs_advanced_p2}

`개요` 페이지에서 **고급 구성으로 서버 시작**을 사용하면 고급 또는 사용자 정의 설정으로 서버를 작성할 수 있습니다. 또한 **구성** 탭을 클릭하여 서버 구성을 사용자 정의할 수 있도록 서버 설정을 업데이트할 수도 있습니다. {{site.data.keyword.mobilefoundation_short}}은 일부 고급 설정에 대한 액세스를 제공합니다.

*	**토폴로지** 탭에서 컨테이너의 크기를 선택할 수 있습니다. 기본값인 1GB 서버는 개발 및 간단한 테스트에 충분합니다. 
  - 사용자 요구사항에 따라 적절한 서버 크기를 선택하십시오.

  - **노드**는 작성된 노드의 수를 표시합니다. 
      - {{site.data.keyword.IBM_notm}} 컨테이너 그룹에 필요한 최소 및 최대 노드 수를 구성할 수 있습니다. 컨테이너 그룹은 고가용성 및 확장성을 제공합니다. 

      - {{site.data.keyword.mobilefirst}} 서버 팜은 여기서 노드의 수를 구성하여 작성될 수 있습니다.

세부사항은 [{{site.data.keyword.mobilefoundation_long}} 문서](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}를 참조하십시오. 
