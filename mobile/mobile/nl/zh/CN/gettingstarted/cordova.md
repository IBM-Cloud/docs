# HelloWorld 样本入门
{: #gettingstarted-cordova}

如果想要从新的 Cordova 应用程序开始操作，可以使用 HelloWorld 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 Bluemix 后端。该应用程序已经安装有 SDK。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 Bluemix 中创建移动后端。
<ol>
	<li>在 Bluemix“目录”的“样板”部分中，单击 MobileFirst Services Starter。</li>
    	<li>输入应用程序的名称和主机，并单击**创建**。</li>
    	<li>单击**完成**。
</li>
</ol>
2. 从 GitHub 获取项目。您可以选择使用 git clone 命令获取项目。从您的计算机打开终端，然后输入以下命令：```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
开始之前，下载 Gradle.zip 文件，然后通过将下载的压缩文件解压到所选目录中来安装 Gradle。首次导入样本时，Android Studio 可能会要求 GRADLE HOME。将该路径设置为解压缩的 Gradle.zip 文件中的 bin 目录。build.gradle 文件会通过拉入所需的依赖关系来自动构建项目。

3. 初始化项目。要初始化 SDK，请在 BMSClient.getInstance().initialize() 函数的 try 块中将 &lt;APPLICATION_ROUTE&gt; 和 &lt;APPLICATION_ID&gt; 替换为您的应用程序路径和 GUID：```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. 在开发环境中运行样本。从 Android Studio 工具栏，单击播放按钮，并选择模拟器。在模拟器中，单击**对 Bluemix 执行 Ping 操作**。样本应用程序会将 Get 请求发送到 Bluemix 中 Node.js 运行时上的受保护资源。如果请求成功，那么会验证连接，且会更新模拟器中的文本。注：Node.js 运行时代码在 MobileFirst Services Starter 样板中提供。如果后端应用程序不是使用 MobileFirst Services Starter 样板创建的，那么该应用程序将不会成功连接。


![Hello World 应用程序已成功连接到 Bluemix](images/yayconnected.jpg "图 1. Hello World 应用程序已成功连接到 Bluemix")

在 Android Studio 中从移动应用程序成功连接到 Bluemix 后，将显示消息“恭喜！您已建立连接”。
5. 解决任何问题。

![Hello World 应用程序未连接到 Bluemix](images/bummer_android.jpg "图 2. Hello World 应用程序未连接到 Bluemix")

连接失败时，将显示消息“糟糕，出错了”。此外，还会提供有关该错误的更多信息。请检查以下各项：
 * 验证是否正确地粘贴了路径和 GUID 值。
 * 您还可以检查调试日志以获取更多信息。

## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅“设置 Android 客户端 SDK”。
