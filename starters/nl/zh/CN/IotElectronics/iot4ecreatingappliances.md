---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# 使用入门模板应用程序
*上次更新时间：2016 年 9 月 15 日*
{: .last-updated}

在 {{site.data.keyword.iotelectronics_full}} Starter 应用程序中创建模拟家电。体验企业制造商可以如何监视连接到 {{site.data.keyword.iot_short_notm}} 的家电。手动与模拟家电进行交互以触发警报、通知和操作。
{:shortdesc}


## 打开入门模板应用程序
{: #iot4e_openAppMain}

由于打开入门模板应用程序的方法会根据使用的 {{site.data.keyword.Bluemix_notm}} 控制台的版本不同而略有变化，因此您应该阅读相应版本的指示信息。

您可以通过查找以下选项来确定使用的版本：
  - [新 {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp)。如果使用的是“新 {{site.data.keyword.Bluemix_notm}} 体验”，那么**尝试新 Bluemix** *不会*显示在标题部分中。
  - [典型 {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp_c)。如果使用的是“典型 {{site.data.keyword.Bluemix_notm}} 体验”，那么**尝试新 Bluemix** 会显示在标题部分中。  

**提示：**要切换到“经典 {{site.data.keyword.Bluemix_notm}} 体验”，请单击标题部分中的用户名，然后向下滚动并单击**切换到典型**。要切换到“新 {{site.data.keyword.Bluemix_notm}} 体验”，请单击标题部分中的**尝试新 Bluemix**。

### 在“新 {{site.data.keyword.Bluemix_notm}} 体验”中打开入门模板应用程序。
{: #iot4e_openApp}
1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板中，通过单击 {{site.data.keyword.iotelectronics}} Starter 应用程序磁贴来启动该入门模板应用程序。

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验。](images/IoT4E_bm_dashboard.png "仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验")

2. 等待标题中显示*您的应用程序正在运行*状态信息，然后单击**查看应用程序**，以显示入门模板应用程序。  

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验。](images/IoT4E_view_app.png "仪表板中的 {{site.data.keyword.iotelectronics}} - 新体验")

### 在“典型 {{site.data.keyword.Bluemix_notm}} 体验”中打开入门模板应用程序。
{: #iot4e_openApp_c}

1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板中，通过单击 {{site.data.keyword.iotelectronics}} Starter 应用程序磁贴来启动该入门模板应用程序。

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 典型。](images/IoT4E_bm_dashboard_c.png "仪表板中的 {{site.data.keyword.iotelectronics}} - 典型体验")

2. 等待“应用程序运行状况”部分中显示*您的应用程序正在运行*状态信息，然后在主窗口中，单击应用程序名称旁边的**路径** URL，以显示入门模板应用程序。  

    ![仪表板中的 {{site.data.keyword.iotelectronics}} - 典型。](images/IoT4E_view_app_c.png "仪表板中的 {{site.data.keyword.iotelectronics}}")

## 创建模拟家电
{: #iot4eCreateAppliances}

在入门模板应用程序中，能以家电制造商或消费者身份创建并控制模拟家电。这些模拟家电的状态和事件数据会存储并可在 {{site.data.keyword.iot_full}} 中进行查看。

1. 选择以下某个选项：
    - **连接并管理模拟家电**，以家电制造商身份创建模拟家电。
    - **远程控制互联家电**，以家电所有者身份创建模拟家电，并通过[样本移动应用程序](iotelectronics_config_mobile.html)进行连接。

    ![{{site.data.keyword.iotelectronics}} Starter 体验](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} Starter 体验")

2. 滚动到标签为**接下来，选择或添加新的模拟洗衣机**的部分，并单击 + 图标。此时将创建新的洗衣机。

    ![添加洗衣机。](images/IoT4E_add_washer.png "添加洗衣机")

3. 要查看洗衣机详细信息、发出命令和生成故障，请单击洗衣机。

  ![洗衣机状态详细信息。](images/IoT4E_washer_control.png "洗衣机状态详细信息")


# 相关链接
{: #rellinks}

## API 文档
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## 组件
{: #general}

* [{{site.data.keyword.iotelectronics}} 文档](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}} 文档](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}} 文档](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}} 文档](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## 样本
{: #samples}
* [样本移动应用程序](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
