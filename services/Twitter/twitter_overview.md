---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About {{site.data.keyword.twittershort}}
{: #about_twitter}

*Last updated: 13 May 2016*

Use {{site.data.keyword.twitterfull}} to incorporate Twitter content from the Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} or [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} streams into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

The content store is refreshed and indexed in real-time, making searches dynamic and fast. The service enriches Tweets with sentiment and other insights for multiple languages, based on deep natural language processing algorithms from [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. Real-time processing of Twitter data streams is fully supported and configurable through a rich set of query parameters and keywords. {{site.data.keyword.twittershort}} includes RESTful APIs that allow you to customize your searches and returns Tweets and enrichments in JSON format. Returned Tweets adhere to the [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window} format for Twitter data.

The {{site.data.keyword.twittershort}} service analyzes the Twitter Decahose and PowerTrack streams in real-time to provide the following enrichments for each Tweet's author:
* Gender
* Permanent location (defined by country, state, and city)

The following enrichments are also available for Tweet content:

* Sentiment (positive, negative, ambivalent, or neutral for Tweets in English, German, French, and Spanish)
* Positive/negative sentiment phrases contained in a Tweet (for Tweets in English, German, French, and Spanish)

To validate {{site.data.keyword.twittershort}} search results, the service provides a REST API method that confirms whether a particular Tweet is still accessible on Twitter. 

## Feedback and support 
{: #feedback_support}

The {{site.data.keyword.twitterfull}} team wants to hear from you.

If you experience any issues with this service, visit the 
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} forum. Search for answers to previously submitted questions or ask a question. 
Include the **insights-twitter** and **bluemix** tags to enhance the response time.

If you questions that aren't addressed in developerWorks Answers, post your question on 
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} and tag your question with **twitter** and **bluemix**.

You can also view the status of the [Bluemix Platform](https://developer.ibm.com/bluemix/support/#status){: new.window} 
or [open a support ticket](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. For more information, see [Troubleshooting](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
