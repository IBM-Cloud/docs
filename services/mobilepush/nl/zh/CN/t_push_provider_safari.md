---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为 Safari Web 浏览器配置凭证
{: #configure-credential-for-safari}
上次更新时间：2016 年 12 月 6 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} 服务现已扩展了功能，可以向 Safari 浏览器发送通知。请注意，受支持的版本为 Safari 10.0。

## 生成证书
  {: #certificate-generation}

确保您已拥有 Apple Developer 帐户。您需要注册 Web 站点推送标识，并生成证书，以配置您的 Safari 浏览器来接收通知。以下步骤将帮助您开始使用该功能。

1. 在 Apple Developer Member 中心，单击 **Certificates, ID & Profiles**。 
2. 单击 **Identifiers**，然后单击 **Website Push IDs**。
3. 通过选择加号图标来创建新条目。![推送仪表板](images/safari_1.jpg)

4. 在 Register Website Push ID 面板中，提供相应的 Web 站点推送标识描述和识别标识。建议使用反向域名格式，以“web”开头。例如：web.com.example.dailyweatherreports。
5. 注册 Web 站点推送标识。您现在已有 Web 站点推送标识 
6. 选择**编辑**以创建要用于 Web 站点推送标识的证书。
7. 在证书信息的“证书助理”窗口中，提供您的电子邮件标识和通用名称。将认证中心电子邮件地址保留为空白。
8. 单击**保存到磁盘**并选择**继续**。
9. 选择将证书保存到相应的文件夹。
10. 向导中提示时选择在磁盘上创建的 `.certSigningRequest`，以生成证书。请确保您已下载以 `.cer` 格式创建的 Web 站点推送证书。
11. 在“钥匙串访问”工具中打开证书。右键单击并导出为 p12 证书。记下在生成 p12 证书时提供的密码。


## 为通知配置
  {: #configuration-notification}
 
生成证书之后，您可以配置服务以将通知发送到 Safari。 

完成以下步骤：

1. 在 Push Notifications 服务仪表板中，单击**配置**。 
2. 选择 Web 选项卡。 
3. 在“Safari 推送”部分中，使用必要信息更新表单。 
	- **Web 站点名称**：这是您在通知中心中提供的名称。
	- **Web 站点推送标识**：使用 Web 站点推送标识的反向域字符串进行更新。例如，web.com.example.www。
	- **Web 站点 URL**：提供应该预订到推送通知的 Web 站点 URL。例如，https://www.example.com。
	- **允许的域**：这是可选参数。这是需要用户提供许可权的 Web 站点列表。请确保 URL 是以逗号分隔的值。请注意，如果未提供此列表，那么将使用 Web 站点 URL 中的值。 
	- **URL 格式字符串**：单击通知时解析的 URL。例如，["https://www.example.com"]。请确保 URL 使用 http 或 https 方案。
	- **Safari Web 推送证书**：上传 .p12 证书并提供密码。
4. 单击**保存**。	

![推送仪表板](images/push_configure_safari.jpg)	

现在，您已配置为将推送通知发送到 Safari 浏览器。

	
