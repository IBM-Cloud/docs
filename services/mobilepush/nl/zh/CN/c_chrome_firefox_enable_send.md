---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 向 Web 浏览器发送基本通知
{: #web_notifications}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

开发应用程序后，可以发送推送通知。 

1. 选择**发送通知**，并通过选择 **Web 通知**作为**发送至**选项来编辑消息。 
2. 键入需要在**消息**字段中传递的消息。
3. 您可以选择提供可选设置：
  - **通知标题**：这是作为消息警报标题显示的文本。
  - **通知图标 URL**：如果您的消息需要与应用程序通知图标一起传递，请在字段中提供图标的链接。
  - **生存时间**：通知服务器消息的有效性。
4. 对于发送到 Safari 浏览器的 Web 通知，需要一些附加信息：
  - **操作**：这是操作按钮的标签	。
  - **URL 自变量**：需要与此通知一起使用的 URL 自变量。请确保以 JSON 数组的形式提供。 
 
下面的图像显示仪表板中的 Web 通知选项。

  ![“通知”屏幕](images/DashboardWebpush.jpg)


## 后续步骤
  {: #next_steps_tags}

成功设置基本通知后，可以选择配置基于标记的通知和高级选项。

将这些 {{site.data.keyword.mobilepushshort}} 服务功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[高级通知](t_advance_badge_sound_payload.html)。



