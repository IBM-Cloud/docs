---

copyright:
 years: 2015, 2016

---

# 创建 Push 服务实例
{: #create-push-instance}

要开始使用 {{site.data.keyword.IBM}} {{site.data.keyword.mobilepushshort}}，首先应创建 {{site.data.keyword.Bluemix}} 应用程序；例如，Node.js 应用程序。然后，创建 Push 服务 {{site.data.keyword.mobilepushfull}} 的实例，该实例需要绑定到此 Bluemix 应用程序。此外，也可以转至 Bluemix“目录”的“样板”部分，然后单击 MobileFirst Services Starter 来执行此操作。

**注**：如果已配置组织来管理您的环境，请选择要在其中为移动应用程序创建运行时和服务的组织。


1. 如果没有 Bluemix 应用程序，那么需要创建 Bluemix 应用程序；例如，Node.js 应用程序。要创建 Bluemix 应用程序，请转至 Bluemix“仪表板”，然后单击**创建应用程序**。
	
	**注**：如果已有应用程序，请转至步骤 7 来添加服务。![创建服务实例](images/create_service_instance1.jpg "创建服务实例")

1. 在**选择应用程序模板**中，单击 **WEB**。

3. 在**选择起点**区域中，选择 **SDK for Node.js**，然后单击**继续**。![起点](images/create_service_nodejs2.jpg) 

4. 在**空间**下拉菜单中，选择组织空间。

	![
Select organization space](images/create_a_service3.jpg)
1. 在**名称**中，输入应用程序的名称。在“主机”中，输入主机的名称。

1. 在**所选套餐**下拉菜单中，选择套餐，然后单击**创建**按钮。等待应用程序编译打包。

1. 单击**概述**链接。![添加服务](images/create_service_add4.jpg)
1. 单击**添加服务**。这将显示“目录”屏幕。

1. 选择 **IBM Push Notifications：**，然后从**空间**下拉菜单中，选择您的组织。

	![组织空间下拉菜单](images/create_service_org.jpg)
1. 在**服务名称**中，输入 Push Notification Service 名称。

1. 在**所选套餐**中，选择套餐，然后单击**创建**按钮。

1. 单击**是**，以重新编译打包应用程序。

	![IBM Push Notification Service](images/create_service_notification5.jpg)

1. 单击**推送通知**，以显示“推送通知”仪表板。
