---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About {{site.data.keyword.twittershort}}
{: #about_twitter}

Use {{site.data.keyword.twitterfull}} to incorporate Twitter content from the Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} or [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} streams into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

The content store is refreshed and indexed in real-time, making searches dynamic and fast. The service enriches Tweets with sentiment and other insights for multiple languages, based on deep natural language processing algorithms from [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. Real-time processing of Twitter data streams is fully supported and configurable through a rich set of query parameters and keywords. {{site.data.keyword.twittershort}} includes RESTful APIs that allow you to customize your searches and returns Tweets and enrichments in JSON format. Returned Tweets adhere to the [Gnip Activity Stream](http://support.gnip.com/){: new_window} format for Twitter data.

The {{site.data.keyword.twittershort}} service analyzes the Twitter Decahose and PowerTrack streams in real-time to provide the following enrichments for each Tweet's author:
* Gender
* Permanent location (defined by country, state, and city)

The following enrichments are also available for Tweet content:

* Sentiment (positive, negative, ambivalent, or neutral for Tweets in English, German, French, and Spanish)
* Positive/negative sentiment phrases contained in a Tweet (for Tweets in English, German, French, and Spanish)

To validate {{site.data.keyword.twittershort}} search results, the service provides a REST API method that confirms whether a particular Tweet is still accessible on Twitter. 

## Feedback and support 
{: #feedback_support}

If you have problems or questions, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the IBM Bluemix development teams. 
* If you have technical questions about developing or deploying an app with {{site.data.keyword.twittershort}}, post your question on Stack Overflow and tag your question with **bluemix** and **twitter**. 
* For questions about the service and getting started instructions, use the IBM [developerWorks dW Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} forum. Include the **insights-twitter** and **bluemix** tags.

See [Getting help](https://new-console.ng.bluemix.net/docs/support/index.html#getting-help){: new.window} for more details about using the forums. 

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://new-console.ng.bluemix.net/docs/support/index.html#contacting-support){: new.window}.
