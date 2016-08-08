---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用移动应用程序
{: #iot4e_using_mobile}
*上次更新时间：2016 年 6 月 14 日*
{: .last-updated}

开始使用 {{site.data.keyword.iotelectronics_full}} 移动应用程序，以了解您可以如何接收警报、发送命令并检查互联家电的状态。
{:shortdesc}

完成以下任务：
1. [下载移动应用程序](#iot4e_downloadmobile)。
2. [配置 {{site.data.keyword.amafull}}](#iot4e_configureMCA)。
3. [将移动设备连接到 {{site.data.keyword.iotelectronics}} 环境](#iot4e_connecting_mobile)。
4. [在移动设备上注册和控制家电](#iot4e_adding_appliance)。


 ## 下载移动应用程序
 {: #iot4e_downloadmobile}
要获取移动应用程序，请在您电话上，从 Apple App Store 下载并安装移动应用程序。在电话上，打开 App Store，并搜索“ibm iot”。选择 **IBM IoT for Electronics** 并安装。

 或者，您也可以使用 [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8)，将其安装到电话上。

## 配置 {{site.data.keyword.amashort}}
{: #iot4e_configureMCA}

您必须配置 {{site.data.keyword.amafull}}，才能连接移动应用程序。  

  1. 在 {{site.data.keyword.iotelectronics}} 的**连接**选项卡上，打开 {{site.data.keyword.amashort}} 应用程序。（您还可以从 {{site.data.keyword.Bluemix_notm}} 仪表板访问应用程序。）  

    ![如何查找 {{site.data.keyword.amashort}}。](images/IoT4E_Connections.svg "{{site.data.keyword.iotelectronics}} 连接")

  2. 在**定制**部分中，单击**配置**。

   ![配置 {{site.data.keyword.amashort}}。](images/MCA_config_pg.svg "{{site.data.keyword.amashort}} 设置认证页面")  

  3. 输入以下认证凭证：
    - **域名**：输入 **myRealm**。
    - **URL**：以下列格式输入 URL，以识别 {{site.data.keyword.iotelectronics}} Starter 应用程序：**https://<*myIoT4eStarterApp*>.mybluemix.net**  

      **提示：**请确保在 URL 中使用安全的 `https://` 前缀。通过单击**移动选项**，您可以查找入门模板应用程序的 URL。


  ![{{site.data.keyword.amashort}} 定制认证项。](images/MCA_config_pg2.svg "{{site.data.keyword.amashort}} 定制认证项")  

  4. 保存。

## 将移动应用程序连接到 {{site.data.keyword.iotelectronics}} 环境
{: #iot4e_connecting_mobile}

要查看移动应用程序上的模拟设备，您必须将移动应用程序连接到 {{site.data.keyword.iotelectronics}} Bluemix 环境。

要连接移动应用程序，请执行以下步骤：

  1. 在计算机上，启动 {{site.data.keyword.iotelectronics}} 应用程序并单击**查看应用程序**，以显示入门模板应用程序。  

  ![“查看应用程序”突出显示的 {{site.data.keyword.iotelectronics}}“入门”页面。](images/IoT4E_getting_started.svg "{{site.data.keyword.iotelectronics}} 具有“查看应用程序”的“入门”页面")  
  2. 选择**远程控制互联家电**。

  ![选择 {{site.data.keyword.iotelectronics}} 消费者应用程序体验。](images/IoT4E_consumer_app.svg "{{site.data.keyword.iotelectronics}} 消费者应用程序体验")

  3. 创建一台或多台洗衣机。在创建洗衣机之前，移动应用程序无法连接。

  4.	滚动到连接 QR 代码，并使用移动设备对其进行扫描。连接 QR 代码位于标签为`要将应用程序连接到环境，您需要扫描此 QR 代码`的部分。

  ![扫描 {{site.data.keyword.iotelectronics}} 连接 QR 代码。](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} 连接 QR 代码")

  5. 输入登录凭证。用户标识和密码可为任意长度。请牢记登录凭证以用于未来会话。  

## 在移动设备上注册和控制家电
{: #iot4e_adding_appliance}

要查看家电状态并接收通知，您必须使用移动应用程序注册家电。

要注册家电，请完成以下步骤：

  1. 在计算机上，滚动到模拟洗衣机，并对其进行单击以显示其数据和家电 QR 代码。

  ![选择洗衣机。](images/IoT4E_mobile_washer_QR.svg "选择洗衣机。")

  2.	使用移动设备扫描洗衣机的 QR 代码，以在移动电话上注册洗衣机。您将在移动电话上看到洗衣机状态。

  3. 在计算机上，选择洗衣机的问题，如电路板故障或强烈振动。该问题会向移动电话发送警报。
