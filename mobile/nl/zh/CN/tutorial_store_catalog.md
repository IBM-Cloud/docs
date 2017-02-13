---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# 教程 - Store Catalog UI Starter
{: #tutorial_store_catalog}

{{site.data.keyword.Bluemix}} Store Catalog UI Starter 提供可定制的基础销售应用程序结构，并为您提供每个 {{site.data.keyword.Bluemix_notm}} Mobile Services 的集成点。


## 需求
{: #tutorial_requirements}

* [Bluemix ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net "外部链接图标") 帐户


## 入门
{: #tutorial_gs}

要快速入门和熟悉运用 Store Catalog UI Starter，请遵循以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建 Mobile 仪表板项目。

   1. 从 Mobile 仪表板的**入门**页面中，单击**创建项目**。

      或者，您可以在**项目**页面上单击**创建项目**。

   2. 选择 **UI 入门模板**（如果尚未选择的话）。

   3. 选择 **Store Catalog** 并单击**创建项目**。

   4. 输入项目名称并单击**创建**。

2. 可选：添加 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**项目概述**页面上，针对 **{{site.data.keyword.mobilepushshort}}** 单击**添加**。

      或者，您可以在 **{{site.data.keyword.mobilepushshort}}** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。

   3. 对于 iOS，[配置 Apple PushNotification Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_ios.html "外部链接图标"){: new_window}。

   4. 对于 Android，[配置 Google 云消息传递 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_android.html "外部链接图标"){: new_window}。

3. 可选：添加其他功能。

   1. 在**项目概述**页面上，针对相应功能单击**添加**。

   2. 输入服务名称并单击**创建**。

   3. 遵循服务所随附的指示信息以对其进行设置。

4. 设计应用程序。

   1. 在导航菜单中选择 **UI 构建器**，以定制应用程序的设计。
   
		**提示：**要查看“UI 构建器”的快速概述，请在选择“UI 构建器”后，在导航中选择**显示如何工作**。

   2. 在导航中选择**设计**选项卡。

      有工作空间用于设计您的应用程序，以及模拟视图用于查看应用程序的外观。

   3. （可选）选择**创建屏幕**，以添加新屏幕。对新屏幕进行命名，以使其易于在应用程序中引用。此时将在与主屏幕相同的级别创建新屏幕，而无论在树中选择的项目为何。您可以从以下屏幕类型中进行选择：
      * 菜单
      * 列表
      * 映射
      * 定制
      * 图表	   

   4. 您可以通过在界面的**布局**部分中，选择*菜单*文本框，并替换**要显示的数据**字段中的内容，来更改应用程序的菜单标题。在模拟设备部分查看更新。

      通过选择每一个更新并更新信息，来更新设计项（如果必要的话）。这些项以树形式显示。您可以通过将菜单项拖移到新位置，来更改菜单项的顺序和位置。菜单项的任何子代也会随父代一起移动。在**要显示的数据**字段中显示的树项中的文本信息会引用数据源电子表格中的内容。*请勿在**设计**视图中更改这些项，因为它们会由**数据**视图中识别的“数据源”中的内容覆盖。*

		在树中识别为*表单*的项是独立的，可以内嵌修改。它不会引用数据源的信息。

   5. 在导航中选择**数据**，以查看应用程序使用的数据。在模板中存在默认信息；但是，您可以通过选择**创建新的**来更改数据源。您可以引用多个数据源，以便为您使用的每个数据源提供名称。您可以从以下数据源选项中进行选择：
      * Cloud
      * Local
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google Drive

      如果表中的内容位于本地，那么您还可以使用按钮并选择表中的内容，来对其进行导入、导出或修改。

	  注意：如果您导入的数据与默认数据的结构不匹配，请开启*替换模式*滑块。如果某个 .csv 文件的列比入门模板所随附的数据少，就属于这种情况。
	  
   6. 选择**导航**以在应用程序中定制导航操作。这是可选的，因为许多屏幕的导航操作都会基于屏幕的关系自动创建。您可以先在菜单项目列表中选择您要*从中*导航的屏幕或字段，来更改目标屏幕。然后，在“目标”屏幕字段中，选择您要其导航*到*的屏幕。 

   7. 在导航中选择**用户访问权**，以修改项目的访问需求。您可以使用开关来开启和关闭用户访问权。当开启用户访问权时，您可以设置不活动用户超时和访问应用程序的用户凭证。

   8. 在导航菜单中选择**设置**，以修改项目的整体信息和颜色。如果您添加到项目的服务需要的话，您可在此屏幕中输入 Google API 密钥。您也通过此屏幕添加在 Apple Store 或 Google Play Store 中注册的唯一捆绑软件标识。

      如果您想要向项目添加 IBM MobileFirst Foundation SDK，请开启此开关。

   9. 如果您在*设置*屏幕中开启此开关以向项目添加 IBM MobileFirst Platform Foundation，那么导航中会显示 **Foundation** 选项。选择 **Foundation** 并完成 IBM MobileFirst Platform Foundation 特定的必要信息。

   10. 在导航菜单中选择**发布**，以输入创建移动应用程序所需的最终信息。您可以输入适用于 iOS 的捆绑软件标识和适用于 Android 的应用程序标识。

       如果您在创建 iOS 应用程序，那么您必须从 Apple 供应门户网站，获取捆绑软件标识、*.p12* 文件形式的分发证书和 *.mobileprovision* 文件形式的供应概要文件。这三项应该在您将应用程序发布到 Apple Store 的同时，在您计划使用的相同计算机上创建。分发证书和供应概要文件必须以捆绑软件标识为基础。 	

5. 下载项目。

   1. 单击**代码**并选择首选平台或编程语言。

   2. 对于 Android，您可以在生成代码后从以下选项中进行选择：

      * 下载代码

      * 下载 APK

      * 使用 QR 码下载

   3. 对于 iOS，您可以在生成代码后选择以下选项：

      * 下载代码

6. 在设备或模拟器上运行应用程序。


## 接下来执行的操作
{: #tutorial_next}

[立即使用！![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "外部链接图标"){: new_window}


### UI 入门模板教程
{: #tutorials_UI}

* [教程 - Store Catalog](tutorial_store_catalog.html)


### 代码入门模板教程
{: #tutorials_Code}

* [教程 - 基本](tutorial.html)
* [教程 - Cloudant Sync](tutorial_cloudant_synd.html)
* [教程 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [教程 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [教程 - Watson Language](tutorial_watson_language.html)
* [教程 - Weather](tutorial_weather.html)

