---

copyright:
  years: 2016

---

#	Developer 플랜 사용
{: #using_mobilefoundation_p1}

*마지막 업데이트 날짜: 2016년 6월 15일*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}}: Developer 서비스 인스턴스를 작성한 후에 {{site.data.keyword.mfp_full_notm}} V8.0에 대한 라이센스 조항에 동의하여 시작하십시오. 잠시 후에는 {{site.data.keyword.mobilefoundation_short}} 서비스를 시작하는 데 도움이 되는 학습서 및 비디오를 제공하는 {{site.data.keyword.Bluemix_notm}}의 `개요` 페이지에 액세스할 수 있습니다.

## {{site.data.keyword.mobilefirst}} 서버 시작
{: #start_mobilefoundation_p1}
* 기본 설정으로 {{site.data.keyword.mfserver_short_notm}}를 시작하려면 **기본 서버 시작**을 클릭하십시오.

이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.
*	1GB 메모리 및 64GB 스토리지. 이 크기는 개발 및 간단한 테스트 활동에 충분합니다. 

*	`username` 및 `password`가 사용자를 위해 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다. 완료되면 대시보드가 표시되며, 여기서 다음을 볼 수 있습니다. 
*	실행 중인 서버의 상태(상태, 크기, 스토리지). 

*	사용자를 위해 작성된 서버 라우트. 이 라우트를 사용하여 공용 인터넷에서 모바일 서버에 접속할 수 있습니다. 모바일 애플리케이션은 해당 라우트를 사용하여 서버에 액세스합니다. 

*	{{site.data.keyword.mfp_oc_short_notm}}에 액세스하기 위한 개인 `사용자 이름` 및 `비밀번호`. `비밀번호`는 숨겨집니다.  **비밀번호 표시**를 클릭하여 이를 볼 수 있습니다. 

*	**콘솔 실행**을 클릭하여 {{site.data.keyword.mfp_oc_short_notm}}을 실행하십시오.


이 콘솔이 컨테이너 내에서 실행됩니다. 콘솔을 사용하여 모바일 앱 및 모바일 디바이스를 관리하고 서버를 모바일 백엔드로 사용하고 푸시 알림을 전송하는 등의 작업을 수행할 수 있습니다.

## {{site.data.keyword.mobilefirst}} 서버 재작성
{: #recreate_mobilefoundation_p1}

*	**재작성**을 클릭하여 서버를 재작성하십시오.

* 이 조치는 기존 서버를 중지하고 이를 삭제합니다. 모바일 서버의 모든 데이터는 유실됩니다. 새 서버 인스턴스가 작성됩니다. 이 조치를 완료하려면 수 분이 소요됩니다. 

##	고급 구성 설정
{: #using_mfs_advanced_p1}

`개요` 페이지에서 **고급 구성으로 서버 시작**을 사용하면 고급 또는 사용자 정의 설정으로 서버를 작성할 수 있습니다. 또한 **구성** 탭을 클릭하여 서버 구성을 사용자 정의할 수 있도록 서버 설정을 업데이트할 수도 있습니다. {{site.data.keyword.mobilefoundation_short}}은 일부 고급 설정에 대한 액세스를 제공합니다.

*	**토폴로지** 탭에서 컨테이너의 크기를 선택할 수 있습니다. 기본값인 1GB 서버는 개발 및 중간 규모의 테스트에 충분합니다. 

  - 사용자 요구사항에 따라 적절한 서버 크기를 선택하십시오.


* **노드**는 작성된 노드의 수를 표시합니다. 이 필드는 {{site.data.keyword.mobilefoundation_short}}: Developer에서 편집할 수 없습니다. Developer 플랜에서 {{site.data.keyword.IBM_notm}} 컨테이너 그룹의 노드 수는 기본적으로 **1**개입니다. 

세부사항은 [{{site.data.keyword.mobilefoundation_long}} 문서](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}를 참조하십시오.
