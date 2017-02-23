---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 可视化设备数据
{: #visualizingdata_data}

此样本帮助您从 {{site.data.keyword.iot_full}} 组织中已注册设备可视化实时数据和历史数据。
{:shortdesc}

## 开始之前
{: #byb}

可视化数据之前，必须执行以下操作：

- 向 {{site.data.keyword.iot_short_notm}} 组织注册设备。
- 确保设备是向 {{site.data.keyword.iot_short_notm}} 发送事件。
- 从 github 存储库[下载可视化样本](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip)并解压缩 .zip 文件。
- 从 {{site.data.keyword.Bluemix_notm}} [安装 cf 命令行工具](../../starters/install_cli.html)。

## 在 {{site.data.keyword.Bluemix_notm}} 中运行样本
{: #running_sample}

1. 使用 Node.js SDK 在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序。记录应用程序的应用程序名称和主机名，需要此信息以将应用程序上传到 {{site.data.keyword.Bluemix_notm}}。
2. 通过完成以下步骤，在 {{site.data.keyword.Bluemix_notm}} 仪表板中将 node.JS 应用程序绑定到 {{site.data.keyword.iot_short_notm}} 实例：

  a. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击已创建的 Node.JS 应用程序。

  b. 单击**绑定服务或 API**，然后选择 {{site.data.keyword.iot_short_notm}} 服务并单击**添加**。
3. 使用 cf 命令行工具，将目录切换到解压缩的可视化样本软件包，并运行以下命令以连接到 {{site.data.keyword.Bluemix_notm}}。
```
cf api https://api.ng.bluemix.net
	 ```
4. 接着，使用以下命令登录到 {{site.data.keyword.Bluemix_notm}}：
```
cf login -u <your_bluemix_login_id>
```
如果未使用缺省组织和空间，那么可使用：
```
cf target-o <your_bluemix_org> -s dev
```

5. 编辑 `manifest.yml` 文件，并使用以下格式更新主机和应用程序名称：
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. 通过使用以下命令部署可视化样本：
```
cf push <your_application_name>
```
7. 在浏览器中，输入以下 URL：
```
http://<your_application_name>.mybluemix.net
```

组织中的所有设备会在设备下拉菜单中列出。进行选择时，应该会看到设备将发送到 {{site.data.keyword.iot_short_notm}} 服务的数据的实时可视化。要查看历史数据，请单击**历史数据**按钮。

## 定制样本
{: #customize_sample}

此样本应用程序是在 node.js 框架上编写的独立 Web 应用程序。此样本可视化通过 {{site.data.keyword.iot_short_notm}} 中已注册设备发送的事件。此样本使用以下工具：

- Express：Node.js Web 应用程序框架
- JQuery：UI 和 Ajax 调用
- Rickshaw：图形可视化工具
- Paho：MQTT 客户机

样本应用程序由以下目录构成：

- Public
- CSS：样式表
- Images
- JS：主要 JavaScript 逻辑文件
- Historian：历史可视化的代码
- Realtime：实时可视化的代码
- Uicontroller.js：用于控制用户界面的代码
- Routes：路由逻辑和 Web 应用程序
- Utils：实用程序功能，用于发出 HTTP 调用
- Views：以 Jade 编写的用户界面文件
- Rickshaw 图表库用于绘制实时数据和历史数据的图形。

## 定制实时数据显示
{: #customize_real_time_display}

包含实时数据的图形可视化代码的目录为 `public/ja/realtime`。可以通过编辑 `public/js/historian/realtimeGraph.js` 对图形逻辑进行定制。

可以在 `public/js/historian/realtime.js` 中找到引用 Paho MQTT 库以从 {{site.data.keyword.iot_short_notm}} 预订设备主题和接收设备事件的文件。

设备事件将传递给 `realtimeGraph.js` 文件以绘制图形。

## 定制历史数据显示
{: #customize_historical_display}

包含历史设备数据的图形可视化代码的目录为 `public/js/historian`。可以通过编辑 `public/js/historian/historianGraph.js` 对图形逻辑进行定制。

用于控制 ReST API 调用以收集历史设备数据的文件为 `public/js/historian/historian.js`。

历史数据将传递给 `historianGraph.js` 文件以绘制图形。

Github iot-visualization Wiki 中提供了更详细的开发者指南。
