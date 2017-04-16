---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为 APNs 配置凭证
{: #create-push-credentials-apns}
上次更新时间：2017 年 1 月 16 日
{: .last-updated}

通过 Apple 推送通知服务 (APNs)，应用程序开发者可以将远程通知从 Bluemix 上的 {{site.data.keyword.mobilepushshort}} 服务实例（提供者）发送到 iOS 设备和应用程序。消息会发送到设备上的目标应用程序。 

您需要获取并配置您的 APNs 凭证。APNs 证书由 {{site.data.keyword.mobilepushshort}} 服务安全管理，在连接到 APNs 服务器（提供者）时需要使用该证书。

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


## 注册应用程序标识
{: #create-push-credentials-apns-register}


应用程序标识（捆绑标识）是用于识别特定应用程序的唯一标识。每个应用程序都需要应用程序标识。像 {{site.data.keyword.mobilepushshort}} 服务这类的服务都是配置给应用程序标识的。

1. 请确保您具有 [Apple Developer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/){: new_window} 帐户。
2. 转至 [Apple Developer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com){: new_window} 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
3. 转至 [Apple Developer Library ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} 中的 **Registering App IDs** 部分，然后遵循指示注册应用程序标识。

注册应用程序标识时，请选择以下选项：

* Push Notifications
![应用程序服务](images/appID_appservices_enablepush.jpg)
* 显式标识后缀
![显式标识](images/appID_bundleID.jpg)
4. 创建开发和分发 APNs SSL 证书。

## 创建开发和分发 APNs SSL 证书
{: #create-push-credentials-apns-ssl}

在获取 APNs 证书之前，必须首先生成一个证书签名请求 (CSR)，然后将其提交给 Apple（认证中心 (CA)）。CSR 中包含您公司的标识信息，以及您用于签署 Apple 推送通知的公用密钥和专用密钥信息。然后，在 iOS 开发者门户网站上生成 SSL 证书。该证书与其公用密钥和专用密钥一起存储在“钥匙串访问”中。

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

您可以在两种模式下使用 APN： 

* 用于开发和测试的沙箱模式。
* 在 App Store（或其他企业分发机制）中分发应用程序时的生产模式。

必须分别针对开发环境和分发环境获取证书。证书与接收远程通知的应用程序的应用程序标识相关联。对于生产方式，最多可创建两个证书。Bluemix 使用证书与 APNs 建立 SSL 连接。

<!-- Create a development and distribution SSL certificate. -->

1. 转至 [Apple Developer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com){: new_window} 网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 在 **Identifiers** 区域中，单击 **App IDs**。
3. 在您的应用程序标识列表中，选择您新创建的应用程序标识，然后选择 **Settings**。
4. 在 **Push Notifications** 区域中，创建开发 SSL 证书，然后创建生产 SSL 证书。

	 ![推送通知 SSL 证书](images/certificate_createssl.jpg)

5. 在 **About Creating a Certificate Signing Request (CSR) screen** 显示时，启用 Mac 上的**钥匙串访问**应用程序以创建证书签名请求 (CSR)。
6. 从菜单选择**钥匙串访问 > 证书助理 > 从证书颁发机构请求证书…** 
7. 在**证书信息**中，输入与您的 App Developer 帐户相关联的电子邮件地址和常用名称。提供有意义的名称来帮助您识别此为开发（沙箱）证书还是分发（生产）证书；例如，*sandbox_apns_certificate* 或 *production_apns_certificate*。
8. 选择**另存到磁盘**，以将 `.certSigningRequest` 文件下载到桌面，然后单击**继续**。
9. 在**另存为**菜单选项中，对 `.certSigningRequest` 文件命名并单击**保存**。
10. 单击**完成**。您现在就有一个 CSR 了。
11. 返回 **About Creating a Certificate Siging Request (CSR)** 窗口并单击 **Continue**。 
12. 在 **Generate** 屏幕中，单击 **Choose File...**，选择保存在桌面上的 CSR 文件。然后，单击 **Generate**。
![生成证书](images/generate_certificate.jpg)
13. 证书准备就绪后，单击 **Done**。
14. 在 **Push Notifications** 屏幕中，单击 **Download** 以下载证书，然后单击 **Done**。
![下载证书](images/certificate_download.jpg)
15. 在 Mac 上，转至**钥匙串访问 > 我的证书**，然后找到新安装的证书。双击该证书，以将其安装到“钥匙串访问”中。
16. 选择证书和专用密钥，然后选择**导出**，以将证书转换成个人信息交换格式（`.p12` 格式）。
![导出证书和密钥](images/keychain_export_key.jpg)
17. 在**存储为**字段中，为证书提供有意义的名称。例如，`sandbox_apns.p12_certifcate` 或 `production_apns.p12`，然后单击**保存**。
![导出证书和密钥](images/certificate_p12v2.jpg)
18. 在**输入密码**字段中，输入用于保护导出项的密码，然后单击**确定**。您可以使用此密码，在“推送”仪表板上配置 APNs 设置。
{: #step18}
	![导出证书和密钥](images/export_p12.jpg)
19. **Key Access.app** 会提示您从**密钥串**屏幕导出密钥。输入 Mac 的管理员密码，以允许系统导出这些项，然后选择**总是允许**选项。这将在桌面上生成一个 `.p12` 证书。


## 创建开发供应概要文件
{: #create-push-credentials-dev-profile}

供应概要文件与应用程序标识一起来确定哪些设备可以安装并运行您的应用程序，以及您的应用程序可以访问哪些服务。对于每个应用程序标识，都可创建两个供应概要文件：一个用于开发，另一个用于分发。Xcode 使用开发供应概要文件来确定允许哪些开发者构建应用程序，以及允许哪些设备在应用程序上进行测试。

请确保您已执行以下操作：注册应用程序标识，针对 {{site.data.keyword.mobilepushshort}} Service 启用该标识，然后将其配置为使用开发和生产 APNs SSL 证书。

创建开发供应概要文件，如下所示：

1. 转至 [Apple Developer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com){: new_window} 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 转至 [Mac Developer Library ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}，滚动至 **Creating Development Provisioning Profiles** 部分，然后遵循指示创建开发概要文件。
**注**：配置开发供应概要文件时，请选择以下选项：
	* **iOS App Development**
	* **对于 iOS 和 watchOS 应用程序**



## 创建应用商店分发供应概要文件
{: #create-push-credentials-apns-distribute_profile}

使用应用商店供应概要文件可提交应用程序以分发到 App Store。

1. 转至 [Apple Developer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com){: new_window} 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 双击所下载的供应概要文件，以将其安装到 Xcode 中。

## 在 {{site.data.keyword.mobilepushshort}} 仪表板上设置 APNs
{: #create-push-credentials-apns-dashboard}

要使用 {{site.data.keyword.mobilepushshort}} 服务发送通知，请上传 Apple 推送通知服务 (APNs) 所需的 SSL 证书。此外，也可以使用 REST API 来上传 APNs 证书。

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

APNs 所需的证书为 `.p12` 证书。这些证书包含构建和发布应用程序所需的专用密钥和 SSL 证书。您必须从 Apple Developer Web 站点的 Member Center 生成证书（此操作需要有效的 Apple Developer 帐户）。对于开发（沙箱）环境和生产（分发）环境，需要不同的证书。

**注**：当 `.cer` 文件出现在钥匙串访问中之后，请将其导出到您的计算机，以创建 `.p12` 证书。

有关使用 APN 的更多信息，请参阅 [iOS Developer Library: Local and Push Notification Programming Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}。

要在“推送通知”服务仪表板上设置 APNs，请完成以下步骤：

1. 在“推送通知”服务仪表板上选择**配置**。
2. 选择**移动**选项，以更新 **APNs 推送凭证**表单上的信息。
3. 根据需要选择**沙箱**（开发）或**生产**（分发），然后上传在先前[步骤](#step18)中创建的 `p.12` 证书。
![设置推送通知仪表板](images/wizard.jpg)
3. 在**密码**字段中，输入与 `.p12` 证书文件相关联的密码，然后单击**保存**。

使用有效的密码成功上传证书后，即可开始发送通知。
