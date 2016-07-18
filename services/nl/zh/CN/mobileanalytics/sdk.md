---

copyright:
  years: 2015, 2016

---

# 检测应用程序以使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK
{: #mobileanalytics_sdk}
*上次更新时间：2016 年 4 月 27 日*
{: .last-updated}

使用 {{site.data.keyword.mobileanalytics_full}} SDK，您可以检测移动应用程序。
{: shortdesc}

使用 {{site.data.keyword.mobileanalytics_short}}，您可以收集三种类别的数据，每一种需要不同程度的检测：

1.  预定义的数据：这种类别包含适用于所有应用程序的通用使用情况和设备信息。在这种类别中存在设备元数据（操作系统和设备模型）和使用情况数据（活动用户和应用程序会话），可指示应用程序使用的数量、频率和持续时间。当您在应用程序中初始化 {{site.data.keyword.mobileanalytics_short}} SDK 之后，会自动收集预定义的数据。
2. 定制事件：这种类别包含您自行定义且特定于您应用程序的数据。此数据代表您应用程序中发生的事件，如查看页面、点击按钮或应用程序内采购。除了在您的应用程序中初始化 {{site.data.keyword.mobileanalytics_short}} SDK 之外，您还必须对要跟踪的每一个定制事件，添加一行代码。
3. 客户机日志消息：这种类别使得开发人员可以在整个应用程序中添加记录定制消息的代码行，以协助开发和调试。开发人员向每一则日志消息分配严重性/详细程度级别，且后续可以根据已分配的级别对消息进行过滤，或者通过配置应用程序，忽略低于给定日志级别的消息，来保留存储空间。要收集客户机日志数据，您必须在应用程序内初始化 {{site.data.keyword.mobileanalytics_short}} SDK，并对每一则日志消息，添加一行代码。

目前，Android、iOS 和 WatchOS 可以使用 SDK。

## 识别客户端密钥值
{: #analytics-clientkey}

在设置客户端 SDK 之前，先识别您的**客户端密钥**值。初始化客户端 SDK 时，需要客户端密钥。
1. 打开 {{site.data.keyword.mobileanalytics_short}} 服务仪表板。
2. 单击扳手图标，以打开“API 密钥”选项卡。
3. 在“API 密钥”选项卡中，注意客户端密钥值。


## 初始化 Android 应用程序以收集分析
{: #initalize-ma-sdk-android}

初始化应用程序以启用发送日志到 {{site.data.keyword.mobileanalytics_short}} 服务。

1. 通过将下列 `import` 语句添加到项目文件的顶端，导入客户端 SDK：

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. 通过在 Android 应用程序主要活动的 `onCreate` 方法中，或者在适合您项目的位置，添加初始化代码，以在 Android 应用程序中初始化 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK。

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // 确保指向您的区域
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  要使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK，您必须使用 **bluemixRegion** 参数，初始化 `BMSClient`。在初始化程序中，**bluemixRegion** 值指定您使用的是哪一个 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. 使用 Android 应用程序对象并为其提供应用程序名称，来初始化 Analytics。您还需要[**客户端密钥**](#analytics-clientkey)值。
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// 在此代码示例中，Analytics 配置为记录生命周期事件。
	```
  {: codeblock}

	**提示：**应用程序名称用作过滤器，在仪表板中搜索客户机日志。当您跨平台（例如 Android 和 iOS）使用相同的应用程序名称时，您可以在相同的名称下，查看该应用程序的所有日志，而无论日志发自哪个平台。

## 初始化 iOS 应用程序以收集分析
{: #init-ma-sdk-ios}

初始化应用程序以启用发送日志到 {{site.data.keyword.mobileanalytics_short}} 服务。iOS 和 watchOS 可以使用 Swift SDK。

1. 通过将下列 `import` 语句添加到 `AppDelegate.swift` 项目文件的顶端，导入 `BMSCore` 和 `BMSAnalytics` 框架：

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. 要使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK，您必须先使用下列代码，初始化 `BMSClient` 类。

  将初始化代码置于应用程序代表的 `application(_:didFinishLaunchingWithOptions:)` 方法中，或者置于适合您项目的位置。

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    要使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK，您必须使用 **bluemixRegion** 参数，初始化 `BMSClient`。在初始化程序中，**bluemixRegion** 值指定您使用的是哪一个 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. 通过为 Analytics 提供您的移动应用程序名称，对其进行初始化。您还需要[**客户端密钥**](#analytics-clientkey)值。

  应用程序名称用作过滤器，在 {{site.data.keyword.mobileanalytics_short}} 仪表板中搜索客户机日志。通过跨平台（例如 Android 和 iOS）使用相同的应用程序名称，您可以在相同的名称下，查看该应用程序的所有日志，而无论日志发自哪个平台。

  可选 `deviceEvents` 参数会自动收集设备级别事件的分析。

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  您可以使用 `Analytics.recordApplicationDidBecomeActive()` 和 `Analytics.recordApplicationWillResignActive()` 方法，来记录 WatchOS 上的设备事件。
  
  将下列一行添加到 ExtensionDelegate 类的 `applicationDidBecomeActive()` 方法中。

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  将下列一行添加到 ExtensionDelegate 类的 applicationWillResignActive() 方法中：
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## 收集使用情况分析
{: #app-monitoring-gathering-analytics}

  您可以配置 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK，以记录使用情况分析，并将记录的数据发送到 {{site.data.keyword.mobileanalytics_short}} 服务。

  使用下列 API，开始记录和发送使用情况分析：

#### Android
{: #android-usage-api}
	
```
// 禁用记录使用情况分析（例如，节省磁盘空间）
// 缺省情况下会启用记录
Analytics.disable();
	
// 启用记录使用情况分析
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// 将记录的使用情况分析发送到 Mobile Analytics 服务
Analytics.send();
```
	
记录事件的使用情况分析示例：
	
```
// 记录定制图表的定制分析事件，其由 JSON 对象代表：
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// 禁用记录使用情况分析（例如，节省磁盘空间）
// 缺省情况下会启用记录
Analytics.enabled = false

// 启用记录使用情况分析
Analytics.enabled = true

// 将记录的使用情况分析发送到 {{site.data.keyword.mobileanalytics_short}} 服务
Analytics.send()
```

记录事件的使用情况分析示例：

```
// 记录定制图表的定制分析事件
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## 启用、配置和使用记录器
{: #app-monitoring-logger}

  {{site.data.keyword.mobileanalytics_full}} 客户端 SDK 提供了一种日志记录框架，与您可能熟悉的其他日志框架（如 `java.util.logging` 或 `log4j`）类似。此日志记录框架支持每个数据包多个记录器实例，支持不同的日志级别，支持捕获对应用程序崩溃的堆栈跟踪，等等。

  您还可以将记录的数据配置为存储在应用程序运行所在的设备上，并在以后将这些设备日志发送到 {{site.data.keyword.mobileanalytics_short}} 服务。

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  {{site.data.keyword.mobileanalytics_short}} 客户端 SDK 日志记录框架支持以下日志级别，按详细程度从低到高的顺序与其建议的使用准则一起列出：

  * `FATAL` - 用于不可恢复的崩溃或挂起。`FATAL` 级别保留用于记录不可恢复的错误，这些错误对于用户显示为应用程序崩溃
  * `ERROR` - 用于意外异常或意外网络协议错误
  * `WARN` - 用于记录不视为严重错误的使用情况警告，例如使用了不推荐的 API 或网络响应速度慢
  * `INFO` - 用于报告初始化事件以及其他可能重要但不紧急的数据
  * `DEBUG` - 用于报告调试语句，以帮助开发者解决应用程序缺陷

    #### 日志级别方案
    {: #log-level-scenario}

    当记录器级别配置为 `FATAL` 时，记录器会捕获未捕获的异常，但是不会捕获导致崩溃事件的任何日志。您可以设置更详细的记录器级别，以确保同时捕获可能导致 `FATAL` 记录器条目的日志，如 `WARN` 和 `ERROR`。

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### 记录器使用情况示例
{: #sample-logger-usage}

**注：**在使用此日志记录框架之前，请确保已检测应用程序，以使用 [{{site.data.keyword.mobileanalytics_short}} 客户端 SDK](sdk.html)。
 
  以下代码片段显示了样本记录器用法：

#### Android
{: #android-logger-sample}

```
// 配置记录器，将日志保存到设备，以便
// 可以在以后将它们发送到 {{site.data.keyword.mobileanalytics_short}} 服务
// 缺省情况下会禁用；设置为 true 可启用
Logger.storeLogs(true);

// 更改最低日志级别（可选）
// 缺省设置为 Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// 将日志发送至 {{site.data.keyword.mobileanalytics_short}} 服务
Logger.send();
```

记录器方案：

```
// 创建两个记录器实例
// 您可以创建多个日志实例，以组织您的日志
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// 具有不同级别的日志消息
// 功能 1 的调试消息
// 功能 2 的信息消息
logger1.debug("debug message");
// 未记录 logger1.debug 消息，因为 logLevelFilter 设置为 Info
logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// 配置记录器，将日志保存到设备，以便可以在以后将它们发送至 {{site.data.keyword.mobileanalytics_short}} 服务
// 缺省情况下会禁用；设置为 true 可启用
Logger.logStoreEnabled = true

// 更改最低日志级别（可选）
// 缺省设置为 LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// 将日志发送至 {{site.data.keyword.mobileanalytics_short}} 服务
Logger.send()
```

记录器方案：
    
```
// 创建两个记录器实例
// 您可以创建多个日志实例，以组织您的日志
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// 具有不同级别的日志消息
logger1.debug("debug message for feature 1")
// 未记录 logger1.debug 消息，因为 logLevelFilter 设置为 Info
logger2.info("info message for feature 2")
```

**提示**：处于隐私考虑，您可以对在发布方式下构建的应用程序，禁用记录器输出。缺省情况下，记录器类会将日志打印到 Xcode 控制台。在目标的构建设置中，将 `-D RELEASE_BUILD` 标记添加到发布构建配置的**其他 Swift 标记**部分。
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## 跟踪活动用户
{: #trackingusers}
通过将活动用户的用户名传递到 {{site.data.keyword.mobileanalytics_short}}，您可以选择跟踪有多少用户正在积极使用您的应用程序。

#### Android
{: #android-tracking-users}

添加下列代码，以用于用户登录时：

```
Analytics.setUserIdentity("username");
```

添加下列代码，以用于用户注销时：

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

添加下列代码，以用于用户登录时：

```
Analytics.userIdentity = "username"
```

添加下列代码，以用于用户注销时：

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# 相关链接

## API 参考
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
