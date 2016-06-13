
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 为 Apple 推送通知服务 (APNs) 配置凭证

{: #create-push-credentials-apns}

通过 Apple 推送通知服务 (APNs)，应用程序开发者可以将远程通知从 Bluemix 上的 Push 服务实例（提供者）发送到 iOS 设备和应用程序。消息会发送到设备上的目标应用程序。您需要获取并配置您的 APNs 凭证。APNs 证书由 Push Notification Service 安全管理，在连接到 APNs 服务器（提供者）时需要使用该证书。

1. 获取 [Apple Developers](https://developer.apple.com/) 帐户。
2. [注册应用程序标识](#create-push-credentials-apns-register)
3. [创建开发和分发 APNs SSL 证书](#create-push-credentials-apns-ssl)
4. [创建开发供应概要文件](#create-push-credentials-dev-profile)
5. [创建应用商店分发供应概要文件](#create-push-credentials-apns-distribute_profile)
6. [在推送仪表板上设置 APNs](#create-push-credentials-apns-dashboard)



##注册应用程序标识
{: #create-push-credentials-apns-register}


应用程序标识（捆绑标识）是用于识别特定应用程序的唯一标识。每个应用程序都需要应用程序标识。像 Push Notifications Service 这类的服务都是配置给应用程序标识的。




1. 转至 [Apple Developer](https://developer.apple.com) 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 转至 [Apple Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991) 中的 **Registering App IDs** 部分，然后遵循指示信息来注册应用程序标识。

	**注**：注册应用程序标识时，请选择以下选项：
	* 推送通知

	![App 服务](images/appID_appservices_enablepush.jpg)

	* 显式标识后缀

	![显式标识](images/appID_bundleID.jpg)
3. 后续步骤：创建开发和分发 APNs SSL 证书。

##创建开发和分发 APNs SSL 证书
{: #create-push-credentials-apns-ssl}

在获取 APNs 证书之前，必须首先生成一个证书签名请求 (CSR)，然后将其提交给 Apple（认证中心 (CA)）。CSR 中包含您公司的标识信息，以及您用于签署 Apple 推送通知的公用密钥和专用密钥信息。然后，在 iOS 开发者门户网站上生成 SSL 证书。该证书与其公用密钥和专用密钥一起存储在“钥匙串访问”中。

**开始之前**

[注册应用程序标识](#create-push-credentials-apns-register)

APNs 可在两种方式下使用：沙箱和生产。

* 沙箱方式在开发和测试期间使用。
* 生产方式在通过 App Store（或其他企业分发机制）分发应用程序时使用。

必须分别针对开发环境和分发环境获取证书。证书与接收远程通知的应用程序的应用程序标识相关联。对于生产方式，最多可创建两个证书。Bluemix 使用证书与 APNs 建立 SSL 连接。

创建开发和分发 SSL 证书。


1. 转至 [Apple Developer](https://developer.apple.com)，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 在 **Identifiers** 区域中，单击 **App IDs**。
3. 在您的应用程序标识列表中，选择您新创建的应用程序标识，然后选择 **Settings**。
4. 在 **Push Notifications** 区域中，创建开发 SSL 证书，然后创建生产 SSL 证书。

 
	 ![推送通知 SSL 证书](images/certificate_createssl.jpg)

	这将显示 About Creating a Certificate a Signing Request 屏幕。

	![创建证书签名请求](images/request.jpg)

5. 在 Mac 上，启动**钥匙串访问**应用程序来创建一个证书签名请求 (CSR)。
6. 选择**钥匙串访问 > 证书助理 > 从证书颁发机构请求证书...** ![钥匙串访问](images/keychain_request_certificate.jpg)
7. 在**证书信息**中，输入与您的 Apple Developer 帐户相关联的电子邮件地址和常用名称。提供有意义的名称来帮助您识别此为开发（沙箱）证书还是分发（生产）证书；例如，**sandbox_apns_certificate** 或 **production_apns_certificate**。

8. 选择**存储到磁盘**，以将 **.certSigningRequest** 文件下载到桌面，然后单击**继续**。
9. 在**存储为**中，对 **.certSigningRequest** 文件命名，例如 **sandbox.certSigningRequest**，然后单击**存储**。
10. 单击**完成**。您现在就有一个 CSR 了。
11. 在 **About Creating a Certificate a Siging Request (CSR)** 中，单击 **Continue**。12. ![证书签名请求](images/request.jpg)
12. 在 **Generate** 屏幕中，单击 **Choose File...**，选择保存在桌面上的 CSR 文件。然后，单击 **Generate**。

	![生成证书](images/generate_certificate.jpg)

13. 证书准备就绪后，单击 **Done**。
14. 在 **Push Notifications** 屏幕中，单击 **Download** 以下载证书，然后单击 **Done**。![下载证书](images/certificate_download.jpg)
15. 在 Mac 上，转至**钥匙串访问 > 我的证书**，然后找到新安装的证书。双击该证书，以将其安装到“钥匙串访问”中。
16. 选择证书和专用密钥，然后选择**导出**，以将证书转换成个人信息交换格式（.p12 格式）。

	![导出证书和密钥](images/keychain_export_key.jpg)

17. 在**存储为**字段中，为证书提供有意义的名称，以便于日后识别；例如 **sandbox_apns.p12_certifcate** 或 **production_apns.p12**，然后单击**存储**。

   	![导出证书和密钥](images/certificate_p12v2.jpg)

18. 在**输入密码**字段中，输入用于保护导出项的密码，然后单击**好**。以后在“推送”仪表板上配置 APNs 设置时会用到此密码。

	![导出证书和密钥](images/export_p12.jpg)
19. **Key Access.app** 会提示您从**密钥串**屏幕导出密钥。输入 Mac 的管理员密码，以允许系统导出这些项，然后选择**总是允许**选项。这将在桌面上生成一个 .p12 证书。


##创建开发供应概要文件
{: #create-push-credentials-dev-profile}

供应概要文件与应用程序标识一起来确定哪些设备可以安装并运行您的应用程序，以及您的应用程序可以访问哪些服务。对于每个应用程序标识，都可创建两个供应概要文件：一个用于开发，另一个用于分发。Xcode 使用开发供应概要文件来确定允许哪些开发者构建应用程序，以及允许哪些设备在应用程序上进行测试。

**开始之前**

请确保您已执行以下操作：注册应用程序标识，针对 Push Notification Service 启用该标识，然后将其配置为使用开发和生产 APNs SSL 证书。

创建开发供应概要文件。

1. 转至 [Apple Developer](https://developer.apple.com) 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 转至 [Mac Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site)，滚动至 **Creating Development Provisioning Profiles**，然后遵循指示信息来创建开发概要文件。

	**注**：配置开发供应概要文件时，请选择以下选项：
	* **iOS App Development**
	* **对于 iOS 和 watchOS 应用程序**



##创建应用商店分发供应概要文件
{: #create-push-credentials-apns-distribute_profile}

使用应用商店供应概要文件可提交应用程序以分发到 App Store。

1. 转至 [Apple Developer](https://developer.apple.com) 门户网站，单击 **Member Center**，然后选择 **Certificates, Identifiers & Profiles**。
2. 双击所下载的供应概要文件，以将其安装到 Xcode 中。

##在推送通知仪表板上设置 APNs
{: #create-push-credentials-apns-dashboard}

要使用 Push Notification Service 发送通知，请上传 Apple 推送通知服务 (APNs) 所需的 SSL 证书。此外，也可以使用 REST API 来上传 APNs 证书。


**开始之前**


获取开发和生产 APNs SSL 证书，以及与每种类型的证书相关联的密码。有关信息，请参阅“为 APNs 创建和配置推送凭证”。

APNs 所需的证书为 .p12 证书，其中包含构建和发布应用程序所需的专用密钥和 SSL 证书。您必须从 Apple Developer Web 站点的 Member Center 生成证书（此操作需要有效的 Apple Developer 帐户）。对于开发（沙箱）环境和生产（分发）环境，需要不同的证书。

**注**：当 **.cer** 出现在钥匙串访问中之后，请将其导出到您的计算机，以创建 .p12 证书。

有关使用 APNs 的更多信息，请参阅 [iOS Developer Library: Local and Push Notification Programming Guide](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4)。

在“推送”仪表板上设置 APNs。

1. 在 Bluemix“仪表板”中打开后端应用程序，然后单击 **IBM Push Notifications** 服务，以打开“推送”仪表板。

	![IBM Push Notifications](images/bluemixdashboard_push.jpg)

	这将显示“推送”仪表板。
	
	![设置推送通知](images/wizard.jpg)
1
2. 在**配置**选项卡上，转至 **Apple 推送证书**部分，选择**沙箱**（开发）或**生产**（分发），然后将 p.12 证书上传到 Bluemix。

	![设置推送通知](images/credential_screen.jpg)
3. 在**密码**字段中，输入与 **.p12** 证书文件相关联的密码，然后单击**保存**。使用有效的密码成功上传证书后，即可开始发送通知。

