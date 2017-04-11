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

# Getting started with {{site.data.keyword.mqa}} (Deprecated)
{: #gettingstartedtemplate}

**The {{site.data.keyword.mqafull}} service is deprecated.** For more information about the status and dates, see the [Retirement of Bluemix Mobile Quality Assurance blog entry ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}.
{:deprecated}

{{site.data.keyword.mqafull}} equips teams to capture tester and live-user experience to continuously build and deliver high-quality mobile apps.
{: shortdesc}

To get up and running quickly with the {{site.data.keyword.mqa}} service, follow these steps:

1. After you create an instance <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->of the {{site.data.keyword.mqa}} service, you can access the {{site.data.keyword.mqa}} Console by clicking your tile in the **Services** section of the {{site.data.keyword.Bluemix}} Dashboard.

	The {{site.data.keyword.mqa}} service launches.

2. Add a mobile app to the {{site.data.keyword.mqa}} instance by selecting **Add MQA App** and providing a name for the app.

3. Download the {{site.data.keyword.mqa}} [Client SDKs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} and complete instrumenting your app by continuing with one of the following procedures:

	* [Instrument MQA with an Android app](mqa_inst_app_android.html)
	* [Instrument MQA with an iOS app](mqa_inst_app_ios.html)
	* [Instrument MQA with a Cordova app](mqa_inst_app_cord.html)

	A single SDK is used to instrument both pre-production and production apps. You can use the ```MODE:``` parameter to specify *QA* for pre-production mode, or specify *MARKET* for production mode. Specify the pre-production mode so that internal testers can provide detailed information about bugs and crashes that occur with your app. Specify the production mode so that users can provide detailed information about your app. If your app is in production, {{site.data.keyword.mqa}} facilitates getting feedback from users right within the app.

4. After you have instrumented your app, you can view more detailed quality information for it by selecting one of the following options on the interface of your {{site.data.keyword.mqa}} service instance:

	<dl>
		<dt><strong>Sessions</strong></dt>
		<dd>Review information about crashes, bugs, feedback, and the state of the device during the session.  See [Viewing session details ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} in IBM Knowledge Center for more information.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Crashes</strong></dt>
		<dd>Review information about what happened to cause crashes. See [Crash reports ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} in IBM Knowledge Center for more information.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Bugs</strong></dt>
		<dd>Review information reported by users such as bug reports, screen captures, and device details. See [Bug reports ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} in IBM Knowledge Center for more information.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>Review user feedback responses to see who wrote the feedback, and when. See [User feedback ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} in IBM Knowledge Center for more information.</dd>
		<dt><strong>Sentiment score (if configured)</strong></dt>
		<dd>Review the user sentiment score over time and versions to monitor, measure, and improve app quality. See [User sentiment ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} in IBM Knowledge Center for more information.</dd>
		<dt><strong>Registered devices</strong></dt>
		<dd>Review the list of devices that are used during a testing session and information about these devices. See [Viewing device information ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} in IBM Knowledge Center for more information.</dd>
	</dl>

	These metrics include the following data:

	* Pre-production data for crashes, bugs, feedback, and sessions.
	* Production data for crashes, feedback, sentiment, and sessions.

	![Screen capture of the interface where you can view quality metrics for an app.](images/quality_metrics_saas4.gif)

	By viewing this information for your apps, you can determine whether to investigate specific issues further. For example, if the crash rate for an app spikes, you can click the crash rate to view more detailed information on crash reports for that app.

5. To view the overall sentiment score for the app, you must configure sentiment analysis:

	1. In the *Sentiment Score* section, click the link to configure sentiment analysis for the selected app.

	2. On the Application Details page, [configure sentiment analysis ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} and save your changes.


# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}

* [Video: Getting Started with Mobile Quality Assurance in Bluemix ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Video: Sentiment Analysis in Mobile Quality Assurance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Add IBM Mobile Quality Assurance to your mobile quality regimen ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Build mobile apps that work: Five tips from an expert panel ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Build a mobile app that isn't perfect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps for mobile apps challenges and best practices ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Sample: bluelist-mqa ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
