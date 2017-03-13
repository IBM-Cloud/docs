---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mqa}} 시작하기(더 이상 사용되지 않음)
{: #gettingstartedtemplate}

**{{site.data.keyword.mqafull}} 서비스는 더 이상 사용되지 않습니다. ** 상태 및 날짜에 대한 자세한 정보는 [Retirement of Bluemix Mobile Quality Assurance 블로그 항목 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}을 참조하십시오.
{:deprecated}

{{site.data.keyword.mqafull}}는 테스터와 라이브 사용자 경험을 파악하여 고품질의 모바일 앱을 지속적으로 빌드하고 전달할 수 있도록 다양한 기능을 제공합니다.
{: shortdesc}

{{site.data.keyword.mqa}} 서비스를 빠르게 실행하려면 다음 단계를 따르십시오. 

1. <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->{{site.data.keyword.mqa}} 서비스의 인스턴스를 작성하고 나면 {{site.data.keyword.Bluemix}} 대시보드의 **서비스** 섹션에서 타일을 클릭하여 {{site.data.keyword.mqa}} 콘솔에 액세스할 수 있습니다. 

	{{site.data.keyword.mqa}} 서비스를 실행합니다. 

2. **MQA 앱 추가**를 선택하고 앱에 대한 이름을 제공하여 {{site.data.keyword.mqa}} 인스턴스에 모바일 앱을 추가하십시오. 

3. {{site.data.keyword.mqa}} [클라이언트 SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window}을 다운로드하고 다음 프로시저 중 하나를 계속 진행하여 앱 인스트루먼트를 완료하십시오. 

	* [Android 앱을 사용하여 MQA 인스트루먼트](mqa_inst_app_android.html)
	* [iOS 앱을 사용하여 MQA 인스트루먼트](mqa_inst_app_ios.html)
	* [Cordova 앱을 사용하여 MQA 인스트루먼트](mqa_inst_app_cord.html)

	사전 프로덕션 및 프로덕션 앱을 인스트루먼트하는 데 하나의 SDK가 사용됩니다. `MODE:` 매개변수를 사용하여 사전 프로덕션 모드를 위해 *QA*를 지정하거나 프로덕션 모드를 위해 *MARKET*을 지정할 수 있습니다. 내부 테스터가 앱에 발생하는 버그 및 충돌에 대한 자세한 정보를 제공할 수 있도록 사전 프로덕션 모드를 지정하십시오. 프로덕션 모드를 지정하면 사용자가 앱에 대한 자세한 정보를 제공할 수 있습니다. 앱이 프로덕션 상태인 경우 {{site.data.keyword.mqa}}는 앱 내에서 사용자로부터 바로 피드백을 받을 수 있습니다. 

4. 앱을 인스트루먼트한 후에는 {{site.data.keyword.mqa}} 서비스 인스턴스의 인터페이스에서 다음 옵션 중 하나를 선택하여 자세한 품질 정보를 볼 수 있습니다. 

	<dl>
		<dt><strong>세션</strong></dt>
		<dd>세션이 진행되는 동안 충돌, 버그, 피드백 및 디바이스 상태에 대한 정보를 검토합니다. 자세한 정보는 IBM Knowledge Center의 [Viewing session details ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window}을 참조하십시오. </dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>충돌</strong></dt>
		<dd>충돌을 일으킨 원인에 대한 정보를 검토합니다. 자세한 정보는 IBM Knowledge Center의 [Crash reports ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window}을 참조하십시오. </dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>버그</strong></dt>
		<dd>버그 보고서, 화면 캡처 및 디바이스 세부사항 등 사용자가 보고한 정보를 검토합니다. 자세한 정보는 IBM Knowledge Center의 [Bug reports ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window}을 참조하십시오. </dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>피드백</strong></dt>
		<dd>누가 언제 피드백을 작성했는지 확인할 수 있는 사용자 피드백 응답을 검토합니다. 자세한 정보는 IBM Knowledge Center의 [User feedback ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window}을 참조하십시오. </dd>
		<dt><strong>감성 점수(구성된 경우)</strong></dt>
		<dd>시간 및 버전별로 사용자 감성 점수를 검토하여 앱 품질을 모니터링하고, 측정하고 개선합니다. 자세한 정보는 IBM Knowledge Center의 [User sentiment ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window}을 참조하십시오. </dd>
		<dt><strong>등록된 디바이스</strong></dt>
		<dd>세션을 테스트하는 동안 사용한 디바이스 목록과 이들 디바이스에 대한 정보를 검토합니다. 자세한 정보는 IBM Knowledge Center의 [Viewing device information ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window}을 참조하십시오. </dd>
	</dl>

	이 메트릭에는 다음과 같은 데이터가 포함됩니다. 

	* 충돌, 버그, 피드백 및 세션에 대한 사전 프로덕션 데이터
	* 충돌, 피드백, 감성 및 세션에 대한 프로덕션 데이터

	![앱에 대한 품질 메트릭을 볼 수 있는 인터페이스의 화면 캡처.](images/quality_metrics_saas4.gif)

	앱과 관련된 이러한 정보를 확인함으로써 특정 문제를 보다 심도 있게 조사할 것인지 여부를 판단할 수 있습니다. 예를 들어, 앱의 충돌율이 높아지면 충돌율을 클릭하여 해당 앱의 충돌 보고서에 대한 자세한 정보를 확인할 수 있습니다.

5. 앱에 대한 전반적인 감성 점수를 확인하려면 감성 분석을 구성해야 합니다.

	1. *감성 점수* 섹션에서 선택된 앱에 대해 감성 분석을 구성하는 링크를 클릭하십시오.

	2. 애플리케이션 세부사항 페이지에서 [configure sentiment analysis ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window}을 수행하고 변경사항을 저장하십시오. 


# 관련 링크
{: #rellinks notoc}

## 학습서 및 샘플
{: #samples notoc}

* [동영상: Getting Started with Mobile Quality Assurance in Bluemix ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [동영상: Sentiment Analysis in Mobile Quality Assurance ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Add IBM Mobile Quality Assurance to your mobile quality regimen ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Build mobile apps that work: Five tips from an expert panel ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Build a mobile app that isn't perfect ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps for mobile apps challenges and best practices ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [샘플: bluelist-mqa ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
