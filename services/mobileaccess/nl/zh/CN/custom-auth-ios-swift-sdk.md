---

copyright:
  years: 2016
lastupdated: "2016-10-09"
---

# 针对 {{site.data.keyword.amashort}} iOS (Swift SDK) 应用程序配置定制认证
{: #custom-ios}

将要使用定制认证的 iOS 应用程序配置为使用 {{site.data.keyword.amafull}} 客户端 SDK，并将该应用程序连接到 {{site.data.keyword.Bluemix}}。新发行的 {{site.data.keyword.amashort}} Swift SDK 为现有 Mobile Client Access Objective-C SDK 提供的功能增添了新功能，同时也改进了现有功能。

**注：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用 Objective-C SDK，以支持此新的 Swift SDK。

## 开始之前
{: #before-you-begin}

您必须具有受配置为使用定制身份提供者的 {{site.data.keyword.amashort}} 服务实例保护的资源。您的移动应用程序还必须安装 {{site.data.keyword.amashort}} 客户端 SDK。有关更多信息，请参阅以下信息：
 * [{{site.data.keyword.amashort}} 入门](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [设置 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [使用定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [创建定制身份提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 进行定制认证](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 配置 {{site.data.keyword.amashort}} 进行定制认证
 {: #custom-auth-ios-configmca}

 1. 打开服务仪表板。
 
 1. 单击**移动选项**，然后记录**路径** (*applicationRoute*) 和**应用程序 GUID/TenantId** (*serviceTenantID*)。初始化 SDK 并将请求发送到后端应用程序时需要这些值。

 1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。

 1. 单击**定制**磁贴。

 1. 在**域名**中，指定您的定制认证域。

 1. 在 **URL** 中，指定您的 applicationRoute。

 1. 单击**保存**。




### 初始化客户端 SDK
{: #custom-ios-sdk-initialize}

通过传递 `applicationGUID` (tenantId) 参数来初始化 SDK。通常会将初始化代码放置在应用程序代表的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

1. 将所需框架导入要使用 {{site.data.keyword.amashort}} 客户端 SDK 的类中。

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```

1. 初始化 {{site.data.keyword.amashort}} 客户机 SDK，将授权管理器更改为 `MCAAuthorizationManager`，并定义和注册认证代表。

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {
let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //the regionName should be one of the following BMSClient.Region constants: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
 }
 ```

在代码中：

* 将 `<applicationBluemixRegion>` 替换为托管 {{site.data.keyword.Bluemix_notm}} 应用程序的区域。要查看 {{site.data.keyword.Bluemix_notm}} 区域，请单击菜单栏中的“头像”图标 ![“头像”图标](images/face.jpg "“头像”图标")，以打开**帐户和支持**窗口小部件。
显示的区域值应为以下某个值：**美国南部**、**英国**或**悉尼**，并对应于代码中需要的常量：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。
* 将“`<yourProtectedRealm>`”替换为您在 {{site.data.keyword.amashort}}“仪表板”的**定制**磁贴中定义的**域名**值。 
* 将“`<serviceTenantID>`”替换为从**移动选项**检索到的 **tenantId** 值。请参阅[配置 Mobile Client Access 以进行定制认证](#custom-auth-ios-configmca)。

### 初始化客户端 SDK
{: #custom-ios-sdk-initialize}
   
  
## 测试认证
{: #custom-ios-testing}

初始化客户端 SDK 并注册定制认证代表后，可以开始对移动后端应用程序发起请求。


### 开始之前
{: #custom-ios-testing-before}

 您必须具有使用 {{site.data.keyword.mobilefirstbp}} 样板创建的应用程序，并且在 `/protected` 端点具有受 {{site.data.keyword.amashort}} 保护的资源。

1. 通过在浏览器中打开 `{applicationRoute}/protected`，向移动后端应用程序的受保护端点发送请求。将 `{applicationRoute}` 替换为从**移动选项**中检索到的值（请参阅[配置 Mobile Client Access 进行定制认证](#custom-auth-ios-configmca)）。例如，`http://my-mobile-backend.mybluemix.net/protected`。

 使用 {{site.data.keyword.mobilefirstbp}} 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问。因此，浏览器中会显示 `Unauthorized` 消息。

1. 使用 iOS 应用程序对同一端点发起请求。初始化 `BMSClient` 并注册定制认证代表后，添加以下代码：

 

	```Swift

	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

	request.send(completionHandler: callBack)
	 ```

1. 请求成功后，将在 Xcode 控制台中看到以下输出：

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
