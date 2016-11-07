---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用移动应用程序
{: #iot4e_using_mobile}
*上次更新时间：2016 年 9 月 19 日*
{: .last-updated}

开始使用 {{site.data.keyword.iotelectronics_full}} 移动应用程序，以了解您可以如何接收警报、发送命令并检查互联家电的状态。
{:shortdesc}

## 开始之前

开始使用移动应用程序之前，必须完成以下任务：
  - 在 {{site.data.keyword.Bluemix_notm}} 组织中部署 {{site.data.keyword.iotelectronics}} Starter 的实例。部署入门模板的实例可自动部署入门模板的组件应用程序和服务。
  - 通过配置 {{site.data.keyword.amafull}}，[启用移动通信和安全性](iotelectronics_config_mca.html)。

## 移动应用程序入门
要开始使用移动应用程序，请完成以下任务：
1. [下载移动应用程序](#iot4e_downloadmobile)至移动设备。
2. [将移动应用程序连接到 {{site.data.keyword.iotelectronics}} 环境](#iot4e_connecting_mobile)，并注册家电。


 ### 下载移动应用程序
 {: #iot4e_downloadmobile}
要获取移动应用程序，请在您电话上，从 Apple App Store 下载并安装移动应用程序。在电话上，打开 App Store，并搜索“ibm iot”。选择 **IBM IoT for Electronics** 并安装。

 或者，您也可以使用 [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8)，将其安装到电话上。


### 连接移动应用程序
{: #iot4e_connecting_mobile}

要将移动应用程序连接到环境并注册家电，请执行以下任务：

1. 打开 {{site.data.keyword.itoelectronics}} Starter 应用程序。有关指示信息，请参阅[打开 Starter 应用程序](iot4ecreatingappliances.html#iot4e_openAppMain)。

2. 选择**远程控制互联家电**。

    ![{{site.data.keyword.iotelectronics}} Starter 体验](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} Starter 体验")

3. 通过滚动到标签为**接下来，选择或添加新的模拟洗衣机**的部分，并单击 + 图标来创建一台或多台洗衣机。此时将创建新的洗衣机。

    ![添加洗衣机](images/IoT4E_add_washer.png "添加洗衣机")

4.	滚动到连接 QR 代码，并使用移动设备对其进行扫描。连接 QR 代码位于标签为**要将应用程序连接到环境，您需要扫描此 QR 代码**的部分。

  ![连接 QR 代码。](images/iot4e_mobile_connect_QR.png "{{site.data.keyword.iotelectronics}} 连接 QR 代码")

5. 在移动设备上，输入登录凭证。用户标识和密码可为任意长度。请牢记登录凭证以用于未来会话。现在您的移动设备已注册到 {{site.data.keyword.iotelectronics}} 环境，您可随时注册单个家电。

6. 在计算机上，滚动到模拟洗衣机，并对其进行单击以显示其数据和家电 QR 代码。

  ![选择洗衣机。](images/IoT4E_mobile_washer_QR.png "选择洗衣机。")

7.	使用移动设备扫描洗衣机的 QR 代码。现在，洗衣机已注册，并且洗衣机状态会显示在移动电话上。

#### 后续工作
现在，可以使用移动设备来查看警报和控制洗衣机。通过执行以下步骤来尝试查看警报和控制洗衣机：
  - 在计算机上，选择洗衣机的问题，如电路板故障或强烈振动。该问题会向移动电话发送警报。
  - 在移动设备上，单击**开始洗涤**以启动机器。您可以在计算机上看到洗衣机经历每个洗涤周期时的状态变化。
