---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 监视推送通知 
{: #monitor-notifications}
上次更新时间：2017 年 1 月 16 日
{: .last-updated}


IBM {{site.data.keyword.mobilepushshort}} 服务现已扩展了功能，可以通过用户数据生成图形，从而监视推送性能。您可以使用实用程序列出所有已发送的推送通知，或者列出所有已注册的设备，并以每天、每周或每月为基础来分析信息。

要为所有已发送的通知生成报告，请使用 [REST API](https://mobile.{DomainName}/imfpush/){: new_window} 中的“推送消息 GET”报告方法。 

![已发送的通知报告](images/monitoring_messages.jpg)


要为所有已注册的设备生成报告，请使用 [REST API](https://mobile.{DomainName}/imfpush/){: new_window} 中的“推送设备注册 GET”报告方法。

![已注册的设备报告](images/monitoring_devices.jpg)

有关如何更新 Android SDK 以监视通知信息的更多信息，请参阅[在 Android 设备上监视推送通知](c_android_enable.html#android_monitor)。


 
