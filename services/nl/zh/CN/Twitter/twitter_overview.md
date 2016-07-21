---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 关于 {{site.data.keyword.twittershort}}
{: #about_twitter}

*上次更新时间：2016 年 5 月 13 日*
{: .last-updated}

使用 {{site.data.keyword.twitterfull}} 可将 Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} 或 [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} 流中的 Twitter 内容包含在 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

内容存储将实时刷新并建立索引，使搜索呈现动态，搜索速度快。该服务根据 [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window} 中的深度自然语言处理算法，通过不同语言的观点和其他见解丰富了推文。全面支持实时处理 Twitter 数据流，通过一组丰富的查询参数和关键字可进行配置。{{site.data.keyword.twittershort}} 包含 RESTful API，用于支持定制搜索，以及返回 JSON 格式的推文和丰富内容。返回的推文符合用于 Twitter 数据的 [Gnip 活动流](http://support.gnip.com/sources/twitter/data_format.html){: new_window}格式。

{{site.data.keyword.twittershort}} 服务可实时分析 Twitter Decahose 和 PowerTrack 流，以便为每个推文作者提供以下丰富内容：
* 性别
* 永久住址（通过国家或地区、省/直辖市/自治区和市/县/区进行定义）

此外，还为推文内容提供了以下丰富内容：

* 观点（用英语、德语、法语和西班牙语发布的对推文的正面、负面、矛盾或中立观点）
* 推文中包含的正面/负面观点短语（适用于用英语、德语、法语和西班牙语发布的推文）

为了验证 {{site.data.keyword.twittershort}} 搜索结果，该服务提供了 REST API 方法来确定特定的推文在 Twitter 上是否仍可访问。 

## 反馈与支持 
{: #feedback_support}

{{site.data.keyword.twitterfull}} 团队希望听取您的意见。

如果使用此服务时遇到任何问题，请访问 IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} 论坛。搜索先前提交问题的答案，或者询问问题。请包括 **insights-twitter** 和 **bluemix** 标记，以增强响应时间。

如果您的问题在 developerWorks Answers 中没有解答，请将您的问题发布到 [Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} 上，并使用 **twitter** 和 **bluemix** 对问题进行标记。

您还可以查看 [Bluemix Platform](https://developer.ibm.com/bluemix/support/#status){: new.window} 的状态，或者[开具支持凭单](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}。有关更多信息，请参阅[故障诊断](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}。
