---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 서비스
{: #services}

{{site.data.keyword.Bluemix}} 모바일 대시보드 **서비스** 보기에서 기존 서비스를 보거나 새 서비스를 작성할 수 있습니다. 모바일 대시보드는 프로젝트에서 관리 중인 모든 Bluemix 서비스를 볼 수 있는 단일 위치를 제공합니다.   

**서비스** 보기에서 서비스를 삭제하는 경우 서비스와 연관된 프로젝트에서 서비스 연결을 끊습니다. 프로젝트에 서비스를 다시 연결하려면 새 서비스 인스턴스를 작성하십시오. 

## {{site.data.keyword.Bluemix_notm}} 모바일 서비스 개요
{: #mobile_services_overview}

다음 표는 {{site.data.keyword.Bluemix_notm}} 모바일 서비스를 표시합니다. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 개별 서비스를 사용하거나 서비스를 모바일 프로젝트에 통합할 수 있습니다.

<table summary="이 표는 {{site.data.keyword.Bluemix_notm}} 모바일 서비스를 설명하고 서비스 문서에 대한 링크를 제공합니다.">
<caption>표 1. {{site.data.keyword.Bluemix_notm}} 모바일 서비스</caption>
<th>{{site.data.keyword.Bluemix_notm}} 모바일 서비스</th>
<th>설명</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} 아이콘"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">{{site.data.keyword.mobileanalytics_full}} 서비스를 사용하여 모바일 앱의 성능과 사용 방법에 대한 인사이트를 얻을 수 있습니다.<br/><br/>
이 서비스 운영에 대한 자세한 정보는 <a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 문서 링크">{{site.data.keyword.mobileanalytics_short}} 문서</a>를 살펴보십시오.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} 서비스 아이콘"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">{{site.data.keyword.amafull}} 서비스를 사용하여 모바일 앱에 보안 기능을 추가할 수 있습니다. 기존의 Google 또는 Facebook 계정을 사용하여 앱에 로그인할 수 있도록 클라이언트 인증 및 ID 제공자를 구성할 수 있습니다.<br/><br/>
이 서비스 운영에 대한 자세한 정보는 <a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 문서 링크">{{site.data.keyword.amashort}} 문서</a>를 살펴보십시오.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} 서비스 아이콘"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">{{site.data.keyword.mobilefoundation_long}} 서비스를 사용하여 엔터프라이즈 모바일 앱을 개발하고, 테스트하고, 운영할 수 있는 {{site.data.keyword.mfp_full}} 환경을 신속하게 설정할 수 있습니다.<br/><br/>
이 서비스 운영에 대한 자세한 정보는 <a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 문서 링크">{{site.data.keyword.mobilefoundation_short}} 문서</a>를 살펴보십시오.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} 서비스 아이콘"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">{{site.data.keyword.mqafull}} 서비스를 사용하여 앱에 대한 모바일 품질 서비스를 검색 및 설정할 수 있습니다. 모바일 앱에 대한 상위 레벨의 품질 메트릭을 보고 작업 중인 앱의 문제를 신속하게 파악할 수 있습니다. 이러한 메트릭에는 충돌, 버그, 사용자 피드백 및 사용자 감성에 대한 정보가 포함됩니다. 앱에 대한 이 정보를 보고 특정 문제를 더 자세히 조사할지 여부를 결정할 수 있습니다.<br/><br/>
이 서비스 운영에 대한 자세한 정보는 <a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 문서 링크">{{site.data.keyword.mqa}} 문서</a>를 살펴보십시오. </td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} 서비스 아이콘"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">{{site.data.keyword.mobilepushfull}} 서비스는 플랫폼 간에 대상 지정된 모바일 및 웹 푸시 알림을 전송하고 관리하기 위한 통합 플랫폼을 제공합니다.
<br/><br/>
{{site.data.keyword.mobilepushshort}}에서는 디바이스, 디바이스 플랫폼, 웹 브라우저에 대한 애플리케이션 사용자의 맵핑을 관리하고, 이에 대한 푸시 알림을 디스패치하는 작업을 처리합니다. 모바일 및 웹 브라우저 애플리케이션 사용자에게 브로드캐스트, 유니캐스트(디바이스 ID 및 사용자 ID 기반), 태그(또는 주제)를 푸시 알림으로 보낼 수 있습니다. 또한 SDK 및 REST API를 사용하여 클라이언트 애플리케이션을 추가로 개발할 수도 있습니다.
<br/><br/>
<a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 문서 링크">{{site.data.keyword.mobilepushshort}} 문서</a>에서 이 서비스의 운용에 대해 자세히 알아보십시오. </td>
</table>

## 모바일 서비스 통합
{: #services_integration}
{{site.data.keyword.cloudant}}와 같은 기존 {{site.data.keyword.Bluemix_notm}} 모바일 서비스를 프로젝트에 통합할 수 있습니다. 


#### {{site.data.keyword.cloudant}} 통합
{: #cloudant_integration}

기존 {{site.data.keyword.cloudant}} 서비스를 통합하려면, 다음 단계를 따르십시오.

1. {{site.data.keyword.cloudant}} 서비스 인스턴스를 클릭하십시오.
2. **실행**을 클릭하십시오.
3. **데이터베이스** 보기에서 데이터베이스 이름을 클릭하십시오.
4. **API**를 클릭하고 데이터베이스 이름을 통해 **API 키** 값을 복사하십시오.

   **참고**: 데이터베이스 이름 뒤에 있는 컨텐츠를 복사하지 마십시오.

5. **권한** > **API 키 생성**을 클릭하고 **키** 및 **비밀번호** 값을 복사하십시오.
6. 모바일 대시보드 **프로젝트** 보기로 다시 이동하십시오.
7. 편집할 프로젝트를 클릭하십시오.
8. **데이터** > **+ 데이터 소스** > **Cloudant**를 클릭하고 데이터 소스 이름을 제공한 후 **추가**를 클릭하십시오.
9. **Cloudant 구성**을 클릭하십시오.
10. 이전에 복사한 **API 키** 값을 **API URL**에 제공하십시오.
11. 이전에 복사한 **키** 값을 **사용자**에 제공하십시오.
12. 이전에 복사한 **비밀번호** 값을 **비밀번호**에 제공하십시오.
13. **확인**을 클릭하십시오.
