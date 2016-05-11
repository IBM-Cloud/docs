---

copyright:
 years: 2015, 2016

---

# 安装 Cordova 推送插件
{: #cordova_install}

安装和使用客户机推送插件来进一步开发 Cordova 应用程序。这还会安装 Cordova 核心插件，该插件会初始化与 Bluemix 的连接。

### 开始之前

1. 下载最新版本的 Android Studio SDK 和 Xcode。
1. 设置仿真器。对于 Android Studio，请使用支持 Google Play API 的仿真器。
1. 安装 Git 命令行工具。对于 Windows，请确保选择**从 Windows 命令提示符运行 Git** 选项。有关如何下载并安装此工具的信息，请参阅 [Git](https://git-scm.com/downloads)。

1. 安装 Node.js 和 Node 软件包管理器 (NPM) 工具。NPM 命令行工具与 Node.js 捆绑在一起。有关如何下载并安装 Node.js 的信息，请参阅 [Node.js](https://nodejs.org/en/download/)。
1. 在命令行中，使用 **npm install -g cordova** 命令来安装 Cordova 命令行工具。必须有该工具才能使用 Cordova 推送插件。有关如何安装 Cordova 和设置 Cordova 应用程序的信息，请参阅 [Cordova Apache](https://cordova.apache.org/#getstarted)。

	**注**：要查看 Cordova 推送插件自述文件，请转至 [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)。


## 安装 Cordova 推送插件
1. 切换到要在其中创建 Cordova 应用程序的文件夹，然后运行以下命令来创建 Cordova 应用程序。如果已有 Cordova 应用程序，请转至步骤 3。


	cordova create your_app_name
	cd your_app_name
	```
1. 可选：编辑 **config.xml** 文件，然后将 <name> 元素中的应用程序名称更改为所选名称，而不使用缺省 HelloCordova 名称。

	**注**：确保指定正确的捆绑软件标识。否则，将在 Xcode 中显示以下错误消息：
	* 对可执行文件进行签名的权利无效。
	* 应用程序的“代码签名权利”文件中指定的权利与供应概要文件中指定的权利不同。

	要解决此问题，请在 Xcode 或 Cordova 应用程序 **config.xml** 文件中指定正确的捆绑软件标识。

1. 将支持的最低版本 API 或部署目标声明添加到 Cordova 应用程序的 config.xml 文件中。minSdkVersion 值必须高于 15。targetSdkVersion 值必须始终反映出 Google 上可用的最新版本 Android SDK。
	* **Android** - 使用编辑器打开 config.xml 文件，然后使用最低的目标 SDK 版本更新
```<platform name="android">``` 元素：

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - 使用部署目标声明更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. 在 Cordova 命令行界面 (CLI) 中，使用以下命令添加平台：iOS 和/或 Android。

	```
	cordova platform add ios
	cordova platform add android
	```
1. 在 Cordova 应用程序根目录中，输入以下命令来安装 Cordova 推送插件：**cordova plugin add ibm-mfp-push**。

	您会看到类似于以下内容的信息，具体取决于您添加的平台：

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. 在 *your-app-root-folder* 中，使用以下命令来验证 Cordova 核心和推送插件是否成功安装：**cordova plugin list**。

	您会看到类似于以下内容的信息，具体取决于您添加的平台：

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. （仅限 iOS）- 配置 iOS 开发环境。
	a. 使用 Xcode 打开 *your-app-name***/platforms/ios** 目录中的 your-app-name.xcodeproj 文件。

	b. 添加桥接头。转至**构建设置 > Swift 编译器 - 代码生成 > Objective-C 桥接头**，然后添加以下路径：*your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. 添加 Frameworks 参数。转至**构建设置 > 链接 > Runpath 搜索路径**，然后添加以下参数：
	```
	@executable_path/Frameworks
	```
	d. 取消注释桥接头中的以下推送导入语句。转至 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. 使用 Xcode 构建并运行应用程序。
1. （仅限 Android）- 使用以下命令来构建 Android 项目：
**cordova build android**。

	**注**：在 Android Studio 中打开项目之前，必须先通过 Cordova CLI 构建 Cordova 应用程序。否则，将遇到构建错误。

1. 后续步骤：[初始化 Cordova 插件](t_cordova_initalize.html)。
