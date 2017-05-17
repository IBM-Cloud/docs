---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 使用移动应用程序
{: #iot4e_using_mobile}

开始使用 {{site.data.keyword.iotelectronics_full}} 移动应用程序，以了解如何使用移动设备（如智能手机或平板电脑）接收警报、发送命令并检查已连接设备的状态。
{:shortdesc}

开始使用移动应用程序之前，您必须在 {{site.data.keyword.Bluemix_notm}} 组织中部署 {{site.data.keyword.iotelectronics}} 入门模板的实例。部署入门模板的实例可自动部署入门模板的组件应用程序和服务。

要开始使用移动应用程序，请完成以下任务：
1. [下载移动应用程序](#iot4e_downloadmobile)至移动设备。
2. [将移动应用程序连接到 {{site.data.keyword.iotelectronics}} 环境](#iot4e_connecting_mobile)，并注册设备。


## 下载移动应用程序
{: #iot4e_downloadmobile}
您可以获取 iOS 或 Android 移动设备的移动应用程序。
- **iOS 设备** - 从 Apple App Store 下载应用程序。在移动设备上，打开 App Store，并搜索“ibm iot”。选择 **IBM IoT for Electronics** 并安装。或者，您也可以使用 [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8)，将其安装到移动设备上。
- **Android 设备** - 从 Google Play Store 下载应用程序。在移动设备上，打开 App Store，并搜索“ibm iot”。选择 **IBM IoT for Electronics** 并安装。

## 连接移动应用程序
{: #iot4e_connecting_mobile}

要将移动应用程序连接到环境并注册设备，请执行以下任务：

1. 打开 {{site.data.keyword.iotelectronics}} Starter 应用程序。有关指示信息，请参阅[打开 Starter 应用程序](iot4ecreatingappliances.html#iot4e_openAppMain)。

2. 选择**远程控制连接的设备**。

    ![{{site.data.keyword.iotelectronics}} Starter 体验](images/IoT4E_remotely_option.svg "{{site.data.keyword.iotelectronics}} Starter 体验")

3. 通过滚动到标签为**接下来，选择或添加新的模拟洗衣机**的部分，并单击 + 图标来创建一台或多台洗衣机。此时将创建新洗衣机。

    ![添加洗衣机](images/IoT4E_add_washer.svg "添加洗衣机")

4.	滚动到“连接 QR 码”，并使用移动设备对其进行扫描。“连接 QR 码”位于**要将应用程序连接到环境，您需要扫描此 QR 码**部分。

  ![连接 QR 代码。](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} 连接 QR 代码")

5. 在移动设备上，输入登录凭证。用户标识和密码可为任意长度。请记住您的登录凭证，以供未来会话使用。现在您的移动设备已注册到 {{site.data.keyword.iotelectronics}} 环境，您可随时注册单个设备。

6. 在您的计算机上，滚动到模拟洗衣机，然后单击它，以显示其数据和设备 QR 码。

  ![选择洗衣机。](images/IoT4E_mobile_washer_QR.svg "选择洗衣机。")

7.	使用移动设备扫描洗衣机的 QR 代码。现在，洗衣机已注册，并且洗衣机状态会显示在移动设备上。

**后续步骤**
现在，可以使用移动设备来查看警报和控制洗衣机。通过执行以下步骤来尝试查看警报和控制洗衣机：
  - 在您的计算机上，选择洗衣机的问题，如电路板故障或振动剧烈。该问题会向移动设备发送警报。
  - 在移动设备上，单击**开始洗涤**以启动机器。您可以在计算机上看到洗衣机经历每个洗涤周期时的状态变化。
