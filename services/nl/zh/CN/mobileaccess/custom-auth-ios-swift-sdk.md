---

copyright:
  years: 2016

---

# 针对 iOS (Swift SDK) 配置 {{site.data.keyword.amashort}} 客户端 SDK
{: #custom-ios}

将要使用定制认证的 iOS 应用程序配置为使用 {{site.data.keyword.amashort}} 客户端 SDK，并将该应用程序连接到 {{site.data.keyword.Bluemix}}。

## 开始之前
{: #before-you-begin}

您必须具有受配置为使用定制身份提供者的 {{site.data.keyword.amashort}} 服务实例保护的资源。您的移动应用程序还必须安装 {{site.data.keyword.amashort}} 客户端 SDK。有关更多信息，请参阅以下信息：
 * [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [设置 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [使用定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [创建定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 进行定制认证](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 配置 {{site.data.keyword.amashort}} 进行定制认证
 {: #custom-auth-ios-configmca}

 1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。

 1. 单击**移动选项**，然后记录**路径** (*applicationRoute*) 和**应用程序 GUID** (*applicationGUID*)。初始化 SDK 时需要这些值。

 1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

 1. 单击**定制**磁贴。

 1. 在**域名**中，指定您的定制认证域。

 1. 在 **URL** 中，指定您的 applicationRoute。

 1. 单击 **保存**。

## 针对 iOS 配置 {{site.data.keyword.amashort}} 客户端 SDK
 {: #custom-auth-ios-sdk}

### 安装 CocoaPods
 {: #custom-auth-cocoapods}

 {{site.data.keyword.amashort}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 iOS 项目的依赖关系管理器。CocoaPods 会自动从存储库下载工件，并将其提供给 iOS 应用程序。

 1. 打开终端并运行 `pod --version` 命令。如果已经安装了 CocoaPods，那么将显示版本号。可以跳至本教程的下一部分。

 1. 通过运行 `sudo gem install cocoapods` 来安装 CocoaPods。如果需要其他指导信息，请参阅 [CocoaPods Web 站点](https://cocoapods.org/)。

 1. 关闭 XCode。

 1. 打开终端并运行 `cd` 进入项目目录。

 1.  运行 `pod init`。

### 使用 CocoaPods 安装客户端 SDK
{: #custom-ios-sdk-cocoapods}

使用 CocoaPods 依赖关系管理器来安装 {{site.data.keyword.amashort}} 客户端 SDK。

1. 打开终端，并浏览到 iOS 项目的根目录。

1. 编辑 `Podfile` 并添加以下行。

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **提示：**您可以将 `use_frameworks!` 添加到 Xcode 目标中，而不是置于 Podfile 中。

1. 在命令行中，运行 `pod install`。
CocoaPods 会安装添加的依赖关系。这将显示进度和添加的组件。

 **重要信息**：您现在必须使用 CocoaPods 生成的 xcworkspace 文件来打开项目。通常该文件的名称为 `{your-project-name}.xcworkspace`。  

1. 在命令行中运行 `open {your-project-name}.xcworkspace` 以打开 iOS 项目工作空间。

### 初始化客户端 SDK
{: #custom-ios-sdk-initialize}

通过传递 `applicationRoute` 和 `applicationGUID` 参数来初始化 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的

1. 获取应用程序参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。单击**移动选项**。**路径**和**应用程序 GUID** 字段中将显示 `applicationRoute` 和 `applicationGUID` 值。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. 初始化 {{site.data.keyword.amashort}} 客户端 SDK，将授权管理器更改为 MCAAuthorizationManager，然后定义认证代表并将其注册。将 `<applicationRoute>` 和 `<applicationGUID>` 替换为从 {{site.data.keyword.Bluemix_notm}} 仪表板中的**移动选项**获取的**路径**和**应用程序 GUID** 值。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<your protected resource's realm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## 测试认证
{: #custom-ios-testing}

初始化客户端 SDK 并注册定制认证代表后，可以开始对移动后端发起请求。

### 开始之前
{: #custom-ios-testing-before}

 必须具有使用 {{site.data.keyword.mobilefirstbp}} 样板创建的应用程序，并且在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。

1. 通过在浏览器中打开 `{applicationRoute}/protected`（例如，`http://my-mobile-backend.mybluemix.net/protected`），向移动后端的受保护端点发送请求。使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。

1. 使用 iOS 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册定制认证代表后，添加以下代码：

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	请求成功后，将在 Xcode 控制台中看到以下输出：

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. 通过添加以下代码，您还可以添加注销功能：

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 如果您在用户登录之后调用此代码，那么用户将注销。用户在尝试重新登录时，必须重新回答服务器发出的质询。

 您可以选择是否将 `callBack` 传递给注销功能。您还可以传递 `nil`。
