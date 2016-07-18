<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld 样本入门
{: #gettingstarted-cordova}

如果想要从新的 Cordova 应用程序开始操作，可以使用 HelloWorld 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 Bluemix 后端。该应用程序已经安装有 SDK。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 Bluemix 中创建移动后端。
<ol>
	<li>在 Bluemix“目录”的“样板”部分中，单击 MobileFirst Services Starter。</li>
    	<li>输入应用程序的名称和主机，并单击**创建**。</li>
    	<li>单击**完成**。</li>
</ol>
2. 从 GitHub 获取项目。您可以选择使用 git clone 命令获取项目。从您的计算机打开终端，然后输入以下命令：
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. 从项目目录运行以下命令，以添加 Android 和 iOS 平台环境：

Android：
```
cordova platform add android
```

iOS：
```
cordova platform add ios
```

4. 使用以下命令添加 Cordova 插件：
```
cordova plugin add ibm-mfp-core
```

5. 为 Android 和/或 iOS 配置 Cordova 应用程序。

 * Android

	 在 Android Studio 中打开项目之前，请先先通过命令行界面 (CLI) 构建并运行 Cordova 应用程序，以免发生构建错误。

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 为避免发生构建错误，请按如下所示配置 Xcode 项目。

	    1. 使用最新版本 Xcode 打开 &lt;app_name&gt;/platforms/ios 目录中的 xcode.proj 文件。

			**重要信息：**如果收到消息，提示您“转换为最新 Swift 语法”，请单击“取消”。

		2. 转至**构建设置 > Swift 编译器 - 代码生成 > Objective-C 桥接头**，然后添加以下路径：

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. 转至**构建设置 > 链接 > Runpath 搜索路径**，然后添加以下 Frameworks 参数：

		```
		@executable_path/Frameworks
		```
		4. 使用 Xcode 构建和运行应用程序。

6. 配置 HelloWorld 样本
<ol>
	<li>切换到克隆该项目的目录</li>
	<li>打开 &lt;your_app_dir&gt;/www/js/index.js 文件，将 &lt;APPLICATION_ROUTE&gt; 和 &lt;APPLICATION_ID&gt; 替换为您的 Bluemix 应用程序标识和路径值。</li>
</ol>

注：请确保您的 &lt;APPLICATION_ROUTE&gt; 安全地使用 https 协议。

```
// Bluemix 凭证
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. 在移动仿真器或设备上运行样本。

   使用以下命令构建 Cordova 应用程序：
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   使用以下命令运行样本应用程序：
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


此时将显示一个视图应用程序，其中含有 **PING BLUEMIX** 按钮。点击该按钮时，应用程序将测试客户机到后端 Bluemix 应用程序的连接。应用程序使用您在 index.js 文件中指定的应用程序路径测试此连接。


![Hello World 应用程序已成功连接到 Bluemix](images/yayconnected.jpg "图 1. Hello World 应用程序已成功连接到 Bluemix")

从移动应用程序成功连接到 Bluemix  后，将显示消息“恭喜！您已建立连接”。
8. 解决任何问题。

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

如果连接失败，那么将显示消息“糟糕，出错了”。此外，还会提供有关该错误的更多信息。
检查以下各项：
 * 验证是否正确地粘贴了路径和 GUID 值。
 * 查看 Xcode 或 Android 调试日志。
 * 在 Bluemix 中检查应用程序的状态。

## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅“设置 Cordova 客户端 SDK”。

# 相关链接

## 样本
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
