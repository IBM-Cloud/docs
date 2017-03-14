---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 对 MQA 安装 iOS 应用程序（已弃用）
{: #instrumentios}

要搭配使用 {{site.data.keyword.mqafull}} 和 iOS 应用程序，必须下载 SDK，并使用 Xcode 开发环境，进行一些更改，以对其执行安装操作。
{: shortdesc}

您必须具有 {{site.data.keyword.Bluemix}} 帐户并为执行安装操作的应用程序平台正确安装了开发环境版本，才能对应用程序安装 {{site.data.keyword.mqa}}。

要对 {{site.data.keyword.mqa}} 执行安装操作以使用 Objective-C 或 Swift 应用程序，请完成以下任务：

1. 将所需许可权和已下载的 SDK 添加到 iOS 项目。

	1. 在 Xcode 中创建或打开项目。

	2. 在 Xcode 项目的*常规*选项卡的*链接的框架和库*部分中，选择 `+`，以添加以下依赖关系库：

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. 将适用于 iOS 的 {{site.data.keyword.mqa}} SDK `Q4M.framework` 文件夹拖到导航器树中的**框架**组中。在“选择选项”窗口中，选择*需要时复制项*，**创建组**，并选中项目名称的复选框以作为目标。

	4. 在*构建设置*选项卡的“链接”部分中，将“调试并发布”的*其他链接程序标记*设置为 **-ObjC**。重要信息：请确保选中*所有*选项卡，以便“其他链接程序标记”包含在列表中。

	5. *仅限 Objective-C：*将以下导入语句添加到 `AppDelegate.m` 和 `ViewController.m` 文件：

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *仅限 Swift：*通过完成以下步骤，为适用于 iOS 的 {{site.data.keyword.mqa}} SDK 添加 Objective-C 桥接头：

		1. 右键单击项目根节点，然后选择**新建文件**。

		2. 在 iOS 下的“选择模板”窗口中，单击“源”部分的“头文件”模板。

		3. 将文件命名为 `MyProject-Bridging-Header.h`（其中 *MyProject* 是 Swift 项目的名称），然后选择项目的名称作为目标。例如，将文件命名为 `MyProject-Bridging-Header.h`。

		4. 单击**创建**以在项目的根目录中保存文件。

		5. 在新桥接头文件中，为桥接头文件添加以下导入语句：

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. 在 Xcode 项目导航器中选中项目的情况下，单击**构建设置**并搜索 `Objective-C 桥接头`。

		7. 在 **Swift 编译器 - 常规**下，将 **Objective-C 桥接头**的值设置为桥接头的路径。该路径是项目根目录的相对路径。例如，如果项目 MQASampleApp 位于 `/user/example/MQASampleApp`，那么该路径为 `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`。如果您在项目的根目录中保存文件，那么您可以使用环境变量来设置该路径，方法是输入 `${SRCROOT}/${PROJECT}-Bridging-Header.h`。

		8. 保存并构建应用程序，以验证路径是否正确。

	7. 在 `info.plist` 文件中，验证项目信息中的以下设置：

		* 捆绑版本 - {{site.data.keyword.mqa}} 使用此字段中的值来确定何时将新构建通知发送给测试人员。当您将新构建上传到 {{site.data.keyword.mqa}} 时，请确保增加此号码。“捆绑版本”字段中的字符串限制为数字和句点 (.) 字符。因为此限制是 Xcode 需求，所以大部分应用程序遵循此惯例，不需要更改。
		* 捆绑版本字符串 - 此字段包含版本号的字符串表示。该字符串没有“捆绑版本”字段的限制。

2. 配置新会话以开始执行每个登录。

    1. 在 `AppDelegate` 文件中找到 `didFinishLaunchingWithOptions` 方法：

        * Objective-C：`AppDelegate.m` 文件
        * Swift：`AppDelegate.swift` 文件

	2. 启动 {{site.data.keyword.mqa}} 会话。

		* Objective-C

			1. 在 `applicationDelegate` 方法的某个方法（如 `didFinishLaunchingWithOptions` 方法）中启动新会话。通过在项目导航器中打开与项目具有相同名称的文件夹，可以找到委派。查找 `projectDelegate.m` 文件。

			2. 在 `didFinishLaunchingWithOptions` 方法中，将以下代码添加到具有 `return YES;` 的行的前面：

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. 将 *Your_Application_Key* 变量替换为来自 {{site.data.keyword.mqa}} 的应用程序密钥。
提示：您可以在“应用程序设置”的 {{site.data.keyword.mqa}} Web 窗格中，找到应用程序密钥。

		* Swift

			1. 在 `AppDelegate.swift` 文件中找到 `didFinishLaunchingWithOptions` 方法。

			2. 在该方法中，将以下代码添加到 `return true` 行的前面，其中 *Your_Application_Key* 是应用程序的有效密钥：

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. 定义是使用预生产方式还是生产方式。有关预生产方式和生产方式之间的区别，请参阅 IBM Knowledge Center 中的[预生产方式和生产方式之间的区别 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window}。

		* Objective-C

			1. 找到 `didFinishLaunchingWithOptions` 方法。

			2. 在 didFinishLaunchingWithOptions 方法中，将以下代码行添加到具有 `return YES;` 的行的前面：

			要使用预生产方式，请添加以下代码行：

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			要使用生产方式，请添加以下代码行：

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C 完整示例**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. 在 AppDelegate.swift 文件中，搜索 `didFinishLaunchingWithOptions` 方法。

			2. 将以下行添加到 `didFinishLaunchingWithOptions` 方法的 `return true` 行的前面：

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			代码的示例为：

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Override point for customization after
				   application launch.
				return true
				```
				{: codeblock}

				**Swift 完整示例**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. 运行应用程序，以确保在应用程序启动时 {{site.data.keyword.mqa}} 会随之启动。

4. 继续 [{{site.data.keyword.mqa}} 入门](index.html)页面上的步骤。

# 相关链接
{: #rellinks notoc}

## 相关链接
{: #general notoc}
* [{{site.data.keyword.mqa}} 入门](index.html){:new_window}
