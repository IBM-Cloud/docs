---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置移动连接和安全性
{: #iot4e_configureMCA}

*上次更新时间：2016 年 9 月 19 日*
{: .last-updated}

通过配置 {{site.data.keyword.amafull}}，启用移动通信和安全性。需要此任务来使用样本移动应用程序，并且此任务只需执行一次。
{:shortdesc}

## 开始之前

开始之前，必须完成以下任务：
  - 在 {{site.data.keyword.Bluemix_notm}} 组织中部署 {{site.data.keyword.iotelectronics}} Starter 的实例。部署入门模板的实例会自动部署组件应用程序和服务，包括 {{site.data.keyword.amafull}}。

  - 由于配置过程会根据使用的 {{site.data.keyword.Bluemix_notm}} 控制台的版本不同而略有变化，因此您应该阅读相应版本的指示信息。

  您可以通过查找以下选项来确定使用的版本：
    - [新 {{site.data.keyword.Bluemix_notm}}](#configMCAnew)。如果使用的是“新 {{site.data.keyword.Bluemix_notm}} 体验”，那么**转至典型体验**选项会显示在仪表板的标题部分中。
    - [典型 {{site.data.keyword.Bluemix_notm}}](#configMCAclassic)。如果使用的是“典型 {{site.data.keyword.Bluemix_notm}} 体验”，**尝试新 Bluemix** 选项会显示在标题部分中。

## 在“新 {{site.data.keyword.Bluemix_notm}} 体验”中配置 {{site.data.keyword.amashort}}
{: #configMCAnew}

  1. 如果刚刚部署了 {{site.data.keyword.iotelectronics}} Starter，那么将显示该入门模板应用程序的“入门”选项卡，您应该继续执行这些指示信息的后续步骤。如果未显示该入门模板应用程序，请打开 {{site.data.keyword.Bluemix_notm}} 仪表板，通过单击 {{site.data.keyword.iotelectronics}} Starter 应用程序磁贴来启动该入门模板应用程序。

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验](images/IoT4E_bm_dashboard.png "仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验")

  2. 在**连接**选项卡上，单击以打开 {{site.data.keyword.amashort}} 服务。

    ![如何查找 {{site.data.keyword.amashort}}。](images/IoT4E_Connections.png "{{site.data.keyword.iotelectronics}} 连接")

  3. 在**设置认证**页面上，通过单击**移动选项**来找到 {{site.data.keyword.iotelectronics}} Starter 应用程序的 URL。复制位于**路径**字段中的 URL。

    ![{{site.data.keyword.amashort}} 移动选项](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} 移动选项")  

  4. 在 ****设置认证的定制部分**页面中，单击**配置**。

       ![配置 {{site.data.keyword.amashort}}。](images/MCA_config_pg.png "{{site.data.keyword.amashort}} 设置认证页面")  

  5. 输入以下认证凭证，然后单击**保存**：
    - **域名**：输入 **myRealm**。
    - **定制身份提供者 URL**：以下列格式输入先前复制的 URL，以标识您的 {{site.data.keyword.iotelectronics}} Starter 应用程序：**https://<*myIoT4eStarterApp*>.mybluemix.net**
    - **您的 Web 应用程序重定向 URI**：使此字段保留空白。

      ![{{site.data.keyword.amashort}} 定制认证项。](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} 定制认证项")  

  6. 通过单击位于标题部分中的入门模板应用程序的名称，返回到 {{site.data.keyword.iotelectronics}} Starter 控制台的“连接”选项卡。

   ![{{site.data.keyword.amashort}} 面包屑。](images/MCA_breadcrumb.png "{{site.data.keyword.amashort}} 面包屑")

## 在“典型 {{site.data.keyword.Bluemix_notm}} 体验”中配置 {{site.data.keyword.amashort}}
{: #configMCAclassic}

1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板中，通过单击 {{site.data.keyword.iotelectronics}} Starter 应用程序磁贴来启动该入门模板应用程序。

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 典型。](images/IoT4E_bm_dashboard_c.png "仪表板中的 {{site.data.keyword.iotelectronics}} - 典型体验")

2. 在您的 {{site.data.keyword.iotelectronics}} 实例中，单击以打开 {{site.data.keyword.amashort}} 服务。   

  ![如何查找 {{site.data.keyword.amashort}}。](images/IoT4E_Connections_c.png "{{site.data.keyword.iotelectronics}} 连接")

2. 在**设置认证**页面上，通过单击**移动选项**来找到 {{site.data.keyword.iotelectronics}} Starter 应用程序的 URL。复制位于**路径**字段中的 URL。

  ![{{site.data.keyword.amashort}} 移动选项](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} 移动选项")  

3. 在 ****设置认证的定制部分**页面中，单击**配置**。

 ![配置 {{site.data.keyword.amashort}}。](images/MCA_config_pg.png "{{site.data.keyword.amashort}} 设置认证页面")  

4. 输入以下认证凭证，然后单击**保存**：
   - **域名**：输入 **myRealm**。
   - **定制身份提供者 URL**：以下列格式输入先前复制的 URL，以标识您的 {{site.data.keyword.iotelectronics}} Starter 应用程序：**https://<*myIoT4eStarterApp*>.mybluemix.net**
   - **您的 Web 应用程序重定向 URI**：使此字段保留空白。

    ![{{site.data.keyword.amashort}} 定制认证项。](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} 定制认证项")  

5. 返回到 {{site.data.keyword.iotelectronics}} Starter 控制台的“连接”选项卡，如下所示：
  1. 通过单击标题部分中**返回到仪表板**选项旁边的双箭头以显示菜单。
  2. 单击**概述**以返回到入门模板控制台。  

    ![{{site.data.keyword.amashort}} 面包屑。](images/MCA_breadcrumb_c.png "{{site.data.keyword.amashort}} 面包屑")
