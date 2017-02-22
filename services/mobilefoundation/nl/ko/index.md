---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilefoundation_short}} 시작하기
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}}는 엔터프라이즈 모바일 앱을 개발, 테스트 및 작동할 수 있는 {{site.data.keyword.mfp_full}} 환경 설정을 신속히 처리합니다. {{site.data.keyword.mobilefoundation_short}}은 두 개의 다른 서비스 플랜 즉, Developer 및 Professional 1 Application 하에서 사용 가능합니다.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Professional 1 Application 플랜을 사용하면 Android, iOS, Windows 또는 모바일 웹 등 지원되는 운영 플랫폼 전체 또는 일부에서 빌드된 단일 애플리케이션을 관리할 수 있습니다. Developer 플랜은 <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> 개발과 테스트에 가장 적합합니다.

## {{site.data.keyword.mobilefoundation_short}}: Developer 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Developer의 인스턴스를 작성한 후 몇 번의 클릭으로 모바일 채널 빌드를 시작할 수 있습니다. 

*	기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오. 		

  `기본 서버 인스턴스에는 단일 노드와 1GB의 메모리가 포함됩니다.`

* 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p1.html#using_mfs_advanced_p1)을 참조하십시오. 

## {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 서비스의 인스턴스를 작성한 후에는 다음 단계를 완료하여 모바일 채널의 빌드를 시작할 수 있습니다. 

1.  {{site.data.keyword.Bluemix_notm}}에서 기존 {{site.data.keyword.dashdbshort}} for Transactions 서비스에 연결하십시오.

    1.  {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 {{site.data.keyword.Bluemix_notm}} `Organization`을 선택하십시오. 

    + 선택된 `Organization`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `Space`를 선택하십시오. 

    + {{site.data.keyword.dashdbshort_notm}} `Service Name` 및 `Credentials`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

    + **연결 테스트**를 클릭하여 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스에 대한 연결을 테스트하십시오.

    + **추가**를 클릭한 후, 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스에 대한 확인을 요청하는 팝업 창에서 **계속**을 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

    **참고:** {{site.data.keyword.dashdbshort_notm}} 연결을 {{site.data.keyword.mobilefoundation_short}} 인스턴스에 추가한 후에는 이를 변경할 수 없습니다. 

2.  서버를 작성하고 시작하십시오. 

    * 기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오. 		

      `기본 서버 인스턴스에는 단일 노드와 1GB의 메모리가 포함됩니다.`

    * 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p2.html#using_mfs_advanced_p2)을 참조하십시오. 

## {{site.data.keyword.mobilefoundation_short}}: Developer Pro 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Developer Pro 서비스의 인스턴스를 작성한 후에는 다음 단계를 완료하여 모바일 채널의 빌드를 시작할 수 있습니다.

  1.  {{site.data.keyword.Bluemix_notm}}에서 기존 {{site.data.keyword.dashdbshort}} for Transactions 서비스에 연결하십시오.

      1.  {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 {{site.data.keyword.Bluemix_notm}} `Organization`을 선택하십시오. 

      + 선택된 `Organization`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `Space`를 선택하십시오. 

      + {{site.data.keyword.dashdbshort_notm}} `Service Name` 및 `Credentials`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

      + **연결 테스트**를 클릭하여 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스에 대한 연결을 테스트하십시오.

      + **추가**를 클릭한 후, 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스에 대한 확인을 요청하는 팝업 창에서 **계속**을 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

      **참고:** {{site.data.keyword.dashdbshort_notm}} 연결을 {{site.data.keyword.mobilefoundation_short}} 인스턴스에 추가한 후에는 이를 변경할 수 없습니다. 

  2.  서버를 작성하고 시작하십시오. 

      * 기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오. 		

      * 이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.

          - 1GB의 메모리가 있는 단일 노드. 이 크기는 개발, 일반적인 테스트 활동, 소규모 프로덕션 워크로드에 충분합니다. 

          -	`username`과 `password`가 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

      * 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p3.html#using_mfs_advanced_p3)을 참조하십시오. 

## {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 플랜 시작하기

{{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 서비스의 인스턴스를 작성한 후에는 다음 단계를 완료하여 모바일 채널의 빌드를 시작할 수 있습니다.

  1.  {{site.data.keyword.Bluemix_notm}}에서 기존 {{site.data.keyword.dashdbshort}} for Transactions 서비스에 연결하십시오.

      1.  {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 있는 {{site.data.keyword.Bluemix_notm}} `Organization`을 선택하십시오. 

      + 선택된 `Organization`에 사용 가능한 영역 목록에서 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스가 존재하는 {{site.data.keyword.Bluemix_notm}} `Space`를 선택하십시오. 

      + {{site.data.keyword.dashdbshort_notm}} `Service Name` 및 `Credentials`를 선택하여 기존 {{site.data.keyword.dashdbshort_notm}} 서비스 인스턴스에 연결하십시오.

      + **연결 테스트**를 클릭하여 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스 인스턴스에 대한 연결을 테스트하십시오.

      + **추가**를 클릭한 후, 선택한 {{site.data.keyword.dashdbshort_notm}} for Transactions 서비스에 대한 확인을 요청하는 팝업 창에서 **계속**을 클릭하십시오. 이 조치는 구성된 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 서비스 인스턴스에 필수 테이블을 작성합니다.

      **참고:** {{site.data.keyword.dashdbshort_notm}} 연결을 {{site.data.keyword.mobilefoundation_short}} 인스턴스에 추가한 후에는 이를 변경할 수 없습니다. 

  2.  서버를 작성하고 시작하십시오. 

      * 기본 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **기본 서버 시작**을 클릭하십시오. 		

      * 이 선택은 다음 설정으로 {{site.data.keyword.mfserver_long_notm}}를 프로비저닝합니다.
          -  각각 1GB 메모리가 있는 두 개의 노드. 이 크기는 개발, 일반적인 테스트 활동, 소규모 프로덕션 워크로드에 충분합니다. 

          -	`username`과 `password`가 자동으로 생성됩니다. 서버가 시작되고 실행되면 이에 액세스할 수 있습니다. 

      * 토폴로지, 보안 및 기타 서버 구성에 대해 고급 구성으로 {{site.data.keyword.mobilefirst_notm}} 서버 인스턴스를 작성하려면 **고급 구성으로 서버 시작**을 클릭하십시오. 자세한 정보는 [고급 구성 설정](c_using_mfs_p4.html#using_mfs_advanced_p4)을 참조하십시오. 

[Mobile Foundation 서비스를 사용하여 MobileFirst 서버 설정<!-- on IBM Containers--> ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window}으로 이동하여 {{site.data.keyword.mobilefoundation_short}}을 시작하는 방법에 대해 학습하십시오.

##  알려진 제한사항

* {{site.data.keyword.mobilefoundation_short}} 서비스 UI가 사용자 선택된 로케일 특정 패턴을 숫자를 표시하는 데 사용하지 않습니다. 


# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

*	[IBM MobileFirst Platform Foundation V8.0.0 제품 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com){: new_window}
