---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 沙箱和生产方式

{: #push-sandboxandproduction-modes}

可以通过以下某种方式来使用 Push Notifications：沙箱或生产。沙箱是独立的测试环境，用于开发和测试 Push API 与服务器应用程序推送服务的集成。首先，使用“推送”仪表板配置沙箱和生产方式。然后，使用 [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} 将推送服务操作方式在沙箱和生产之间进行切换。缺省情况下，会启用沙箱方式。但是，在两种方式之间切换时，标记、设备和预订不会在这两种方式之间共享。


如果已准备好将应用程序部署到现场环境，请使用 Push REST API 选择生产方式。有关 REST API 的信息，请参阅 REST API。

要将推送服务操作方式从沙箱切换到生产，请执行以下操作：

1. 使用 PUT ApplicationID 设置 REST API 调用
2. 在 JSON 主体中，确认是否已使用 [GET ApplicationID 设置 REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} API 调用切换了该方式。响应应该为 "mode": "PRODUCTION"
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. 切换环境方式后，重新运行客户机代码来以生产方式注册设备。

有关 REST API 的信息，请参阅 REST API。
