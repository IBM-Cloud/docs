---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

#	Developer 플랜 사용
{: #using_mobilefoundation_p1}

{{site.data.keyword.mobilefoundation_short}}: Developer 서비스 인스턴스를 작성하고 잠시 후 {{site.data.keyword.Bluemix_notm}}의 `개요` 페이지에 액세스할 수 있습니다. 이 페이지에서는 {{site.data.keyword.mobilefoundation_short}} 서비스를 시작하는 데 유용한 튜토리얼과 동영상을 제공합니다. 

## {{site.data.keyword.mobilefirst}} 서버 시작
{: #start_mobilefoundation_p1}
* 기본 설정으로 {{site.data.keyword.mfserver_short_notm}}를 시작하려면 **기본 서버 시작**을 클릭하십시오.

이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.
*	1GB의 메모리. 이 크기는 개발, 간단한 테스트 활동, 소규모 프로덕션 워크로드에 충분합니다. 

*	`username` 및 `password`가 사용자를 위해 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다. 완료되면 대시보드가 표시되며, 여기서 다음을 볼 수 있습니다. 
*	실행 중인 서버의 상태(상태, 크기). 

*	사용자를 위해 작성된 서버 라우트. 모바일 애플리케이션에서 이 라우트를 사용하여 {{site.data.keyword.mfserver_short_notm}}에 연결하십시오. 

*	{{site.data.keyword.mfp_oc_short_notm}}에 액세스하기 위한 개인 `username` 및 `password`. `password`는 숨겨집니다. **비밀번호 표시** 아이콘을 클릭하면 볼 수 있습니다. 

*	**콘솔 실행**을 클릭하여 {{site.data.keyword.mfp_oc_short_notm}}을 실행하십시오.


<!--This console runs inside the container.--> 콘솔을 사용하여 모바일 앱 및 모바일 디바이스를 관리하고 서버를 모바일 백엔드로 사용하고 푸시 알림을 전송하는 등의 작업을 수행할 수 있습니다. 

##  Mobile Analytics 서버 추가
{: #adding_analytics_server_dev}

 이제 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 Mobile Analytics 서버를 추가하여 {{site.data.keyword.mobilefirst}} 서버에서 모바일 애플리케이션을 모니터링할 수 있습니다. Developer 플랜을 통해 메모리가 1GB인 단일 노드가 포함된 컨테이너 그룹에 Mobile Analytics 서버를 작성합니다.

* **분석 추가**를 클릭하여 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 Mobile Analytics 서버를 추가하십시오.

프로비저닝 프로세스가 시작됩니다. 이 프로세스는 약 10분 정도 소요되며, 메시지 창은 이 조작의 진행상태를 표시합니다.   

* {{site.data.keyword.mfp_oc_short_notm}}에서 MobileFirst Analytics Console을 실행하십시오.

* {{site.data.keyword.mfserver_short_notm}}와 Mobile Analytics 서버 간에 싱글 사인온이 사용됩니다. Mobile Analytics 서버는 {{site.data.keyword.mfserver_short_notm}}와 동일한 LTPA 키 및 사용자 신임 정보를 사용하여 구성합니다. {{site.data.keyword.mfp_oc_short_notm}}에 로그인하는 데 사용한 `사용자 이름` 및 `비밀번호`를 사용하여 Mobile Analytics 콘솔에 로그인할 수 있습니다.

MobileFirst Analytics에 대한 자세한 정보는 [MobileFirst Foundation Operational Analytics ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}을 참조할 수 있습니다.

**참고:** {{site.data.keyword.mobilefoundation_short}} 서버 인스턴스를 삭제하거나 {{site.data.keyword.mfserver_short_notm}}를 다시 작성하려고 할 때 Mobile Analytics 서버가 제거됩니다.

##  Mobile Analytics 서버 삭제
{: #deleting_analytics_server_dev}

이제 {{site.data.keyword.mobilefoundation_short}} 서비스 대시보드에서 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 추가된 Mobile Analytics 서버를 삭제할 수 있습니다.

* **분석 삭제**를 클릭하여 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스에 추가된 Mobile Analytics 서버를 삭제하십시오.

 이렇게 하면 분석 컨테이너 그룹이 삭제됩니다. 분석 컨테이너 삭제 프로세스에는 약 10분이 걸립니다. 화면을 새로 고쳐 업데이트된 상태를 볼 수 있습니다. 분석 컨테이너가 삭제되면 **분석 추가** 단추가 다시 사용 가능하게 되고 이 단추를 사용하여 Mobile Analytics 서버를 다시 추가할 수 있습니다(선택하는 경우).


## {{site.data.keyword.mobilefirst}} 서버 재작성
{: #recreate_mobilefoundation_p1}

*	**재작성**을 클릭하여 서버를 재작성하십시오.

* 이 조치는 기존 서버를 중지하고 데이터를 삭제합니다. 모바일 서버의 모든 데이터는 유실됩니다. 업데이트된 버전이 있는 경우 새 서버 인스턴스가 업데이트된 버전으로 작성됩니다. 이 조치를 완료하려면 수 분이 소요됩니다. 

##	고급 구성 설정
{: #using_mfs_advanced_p1}

`Overview` 페이지에서 **고급 구성으로 서버 시작**을 사용하면 고급 또는 사용자 정의 설정으로 서버를 작성할 수 있습니다. 또한 **구성** 탭을 클릭하여 서버 구성을 사용자 정의할 수 있도록 서버 설정을 업데이트할 수도 있습니다. {{site.data.keyword.mobilefoundation_short}}은 일부 고급 설정에 대한 액세스를 제공합니다.

*	**토폴로지** 탭에서 필요한 서버 크기와 인스턴스 수를 선택할 수 있습니다. 기본값인 1GB 서버는 개발 및 중간 규모의 테스트에 충분합니다. 

  - 사용자 요구사항에 따라 적절한 서버 크기를 선택하십시오.

* **노드**는 작성된 노드의 수를 표시합니다. 이 필드는 {{site.data.keyword.mobilefoundation_short}}: Developer에서 편집할 수 없습니다. Developer 플랜에서 <!--in your {{site.data.keyword.IBM_notm}} container group--> 노드 수는 기본적으로 **1**입니다.

세부사항은 [{{site.data.keyword.mobilefoundation_long}} 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}을 참조하십시오.
