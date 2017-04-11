---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 安装并连接样本移动应用程序
{: #iot4i_gettingstarted}

{{site.data.keyword.iotinsurance_full}} 样本移动应用程序是 {{site.data.keyword.iotinsurance_short}} 的移动式客户机的参考实施。您可以使用应用程序在系统中注册新设备并接收设备的警报。
{:shortdesc}

**注**：{{site.data.keyword.iotinsurance_short}} 不再部署 {{site.data.keyword.amafull}} 或 {{site.data.keyword.mobilepushfull}}。{{site.data.keyword.iotinsurance_short}} 的较早版本使用 {{site.data.keyword.amashort}} 服务处理移动应用程序的响应。此处理会针对所有现有 {{site.data.keyword.iotinsurance_short}} 实例继续运作。但是，您必须创建定制验证流程，以使用移动应用程序和新 {{site.data.keyword.iotinsurance_short}} 实例。您还可以选择[创建 {{site.data.keyword.mobilepushshort}} 实例](../mobilepush/index.html)、对其进行配置并将其绑定到 {{site.data.keyword.iotinsurance_short}} API。

**先决条件：**开始之前，请确保满足以下先决条件：
  - Apple Xcode 8 或更高版本的集成开发环境。
  - iOS 9.0 或更高版本的 iPhone 移动设备。
  - 已在计算机上安装了 CocoaPods。请参阅 [CocoaPods Web站点 ![外部链接图标](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window}。
  - 将样本移动应用程序连接到服务实例时所需的[参数](#iot4i_mobileParam)。

## 构建样本移动应用程序
{: #building_mobile}
要尝试使用样本移动应用程序，请执行以下任务：

1. 将[样本移动应用程序的源代码存储库 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} 克隆到安装了 Xcode7.3 或更高版本的计算机上。
2. 通过在您的项目上运行 CocoaPods pod 安装命令安装所需的软件包并生成 IoT4I.xcworkspace 文件。要完成此任务，必须安装 CocoaPods。
3. 通过双击 IoT4I.xcworkspace 文件在 Xcode 中打开项目。
4. 将您的 iPhone 连接到计算机并将其选作构建目标。
5. 在文件列表中选择 IoT4I 文件以在“身份”对话框中进行显示。
6. 在 Xcode“身份”对话框中，进行以下更改：
  - 将**捆绑软件标识**更改为唯一标识，例如：**myIoT4Ibundle**。
  - 将**团队**设置为个人团队名称，然后单击**修复问题**。
7. 要将您的应用程序连接到 {{site.data.keyword.iotinsurance_short}} 实例，请在 **constants.swift** 文件中设置以下参数：  
    - [applicationRoute](#iot4i_mobileParam) = {{site.data.keyword.iotinsurance_short}} API 应用程序的 URL。您可以在 {{site.data.keyword.iotinsurance_short}} 服务控制台的“服务凭证”标签中找到此值。
    - [applicationId](#iot4i_mobileParam) = {{site.data.keyword.amashort}} 实例的 GUID。您可以通过打开 {{site.data.keyword.amashort}}，然后单击**移动选项**找到此值。此值称为应用程序 GUID / 租户标识。
8. 在您的计算机上，单击箭头以构建并运行当前方案。样本移动应用程序安装在您的手机上。有关更多信息，请参阅 [Apple 开发人员从 Xcode 在设备上运行应用程序的指示信息 ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window}。

  **注意：**如果您尝试构建时显示错误消息：*无法启动 IoT4I，因为您尚未验证 Developer App 证书在您的设备上是否可信*，请选择您自己作为受信的开发人员，如下所示：  
    1. 在您的手机上，转至**设置 > 常规 > 设备管理 > 您的开发人员标识**。
    2. 点击您的开发人员标识帐户名称，为您的开发人员标识建立信任。
    3. 系统提示时，确认开发人员标识已受信任。

## 启用移动应用程序推送通知
{: #iot4i_pushNotification}

执行以下任务以启用移动设备的推送通知。您必须具有有效的 Apple 开发人员帐户成员资格以使用推送通知服务。

1. 登录到 [Apple 开发人员帐户 ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window}。

2. 创建证书文件。
  1. 选择 **Certificates, Identifiers & Profiles**。
  2. 选择“Identifiers: App IDs”。
  3. 单击 Add 按钮 (+) 以创建新的应用程序标识。
  4. 在 **Description** 中输入应用程序的描述。
  5. 选择 **Explicit App ID** 并输入捆绑软件标识，例如，com.YourOrganizationName.iot4i.mobileApp。
  6. 在 **Push Notifications** 上选择 (V)，并单击 **Continue > Register > Done**。

3. 创建推送通知证书。
  1. 选择 **Certificates: All**。
  2. 单击 Add 按钮 (+) 以创建新的 APN 证书。
  3. 在“Add iOS Certificate”页面中，选择 **Apple Push Notification service SSL (Sandbox)** 并单击 **Continue**。
  4. 选择您在先前步骤中创建的应用程序标识并单击 **Continue**。
  5. 使用页面上的指示信息来创建 CSR 文件并单击 **Continue**。
  6. 选择所创建的 CSR 文件并单击 **Continue**。
  7. 下载并运行证书文件。

4. 创建概要文件。
  1. 选择 **Provisioning profile: Development**。
  2. 单击 Add 按钮 (+) 以创建新的开发概要文件。
  3. 选择 **iOS App Development** 并单击 **Continue**。
  4. 选择您先前创建的应用程序标识。 
  5. 选择 **Developer Certificates: All** 并单击 **Continue**。
  5. 选择 **All development devices (testing
devices)** 并单击 **Continue**。
  6. 指定概要文件名称并单击 **Continue**。
  7. 下载并运行生成的概要文件。

5. 创建公用密钥密码术标准 (PKCS) 12 文件并将其添加到 {{site.data.keyword.mobilepushshort}} 服务。
  1. 打开密钥链访问并选择 **My Certificates**。
  2. 右键单击 **Apple Development IOS Push Service: (bundleID)**，然后导出、保存和输入文件密码。
  3. 在 {{site.data.keyword.Bluemix_notm}} 控制台中，打开 {{site.data.keyword.mobilepushshort}} 服务。
  4. 单击**配置**。
  5. 在 Apple Push Notifications Certificate 部分中，上传 PKCS 12 文件并输入密码。
  6. 在 Xcode 中，将捆绑软件标识更改为您先前创建的标识。
  7. 运行应用程序并授予推送通知服务许可权。
