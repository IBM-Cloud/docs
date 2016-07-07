---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilefoundation_short}} 시작하기
{: #gettingstartedtemplate}

*마지막 업데이트 날짜: 2016년 6월 15일*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}}은 엔터프라이즈 모바일 앱을 개발, 테스트 및 작동할 수 있는 {{site.data.keyword.mfp_full}} 환경 설정을 신속히 처리합니다.
{{site.data.keyword.mobilefoundation_short}}은 두 개의 다른 서비스 플랜 즉, Developer 및 Professional 1 Application 하에서 사용 가능합니다.
{:shortdesc}

Professional 1 Application 플랜은 {{site.data.keyword.mobilefoundation_short}} 서버가 확장 가능한 컨테이너 그룹에 배치될 수 있게 합니다.Professional 1 Application 플랜을 사용하면 Android, iOS, Windows 또는 모바일 웹과 같이 지원되는 운영 체제 전체 또는 일부에서 빌드된 단일 애플리케이션을 관리할 수 있습니다. Developer 플랜은 2개 이상의 노드를 갖는 컨테이너 그룹에서 {{site.data.keyword.mobilefoundation_short}} 배치를 지원하지 않습니다. 이 플랜은 개발 및 테스트에 가장 적합합니다. 

## {{site.data.keyword.mobilefoundation_short}}: Developer 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Developer의 인스턴스를 작성한 후 몇 번의 클릭으로 모바일 채널 빌드를 시작할 수 있습니다. 

*	기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오.
		

  `기본 서버 인스턴스에는 단일 노드, 1GB 메모리 및 64GB 메모리 용량이 포함됩니다. `

* 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p1.html#using_mfs_advanced_p1)을 참조하십시오. 

## {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스의 인스턴스를 작성한 후에는 다음 단계를 완료하여 모바일 채널의 빌드를 시작할 수 있습니다. 

1.  {{site.data.keyword.Bluemix_notm}}에서 기존 {{site.data.keyword.dashdbshort}}: Enterprise Transactional 서비스에 연결하십시오.

    1.  현재 `조직`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `영역`을 선택하십시오. 

    2.  {{site.data.keyword.dashdbshort_notm}} `서비스 이름` 및 `신임 정보`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

    3.  **연결 테스트**를 클릭하여, 선택한 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 서비스 인스턴스에 대한 연결을 테스트하십시오.

    4.  **추가**를 클릭한 후, 선택한 {{site.data.keyword.dashdbshort_notm}} 서비스에 대한 확인을 요청하는 팝업 창에서 **계속**을 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

2.  서버를 작성하고 시작하십시오. 

    * 기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오. 		

      `기본 서버 인스턴스에는 단일 노드, 1GB 메모리 및 64GB 메모리 용량이 포함됩니다. `

    * 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p2.html#using_mfs_advanced_p2)을 참조하십시오. 

{{site.data.keyword.mobilefoundation_short}}을 시작하는 방법에 대해 학습하려면 [Mobile Foundation 서비스를 사용하여 IBM Containers에서 MobileFirst 서버 설정](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/)으로 이동하십시오.

# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

*	[IBM MobileFirst Platform Foundation V8.0.0 제품 문서](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
