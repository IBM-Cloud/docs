---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# 设置 iOS Swift SDK
{: #getting-started-ios}

使用 {{site.data.keyword.appid_short}} 客户端 SDK 构建 Swift 应用程序，初始化该 SDK，认证用户，然后对受保护和不受保护的资源发起请求。
{:shortdesc}


## 开始之前
{: #before-you-begin}

您需要以下信息：
  * {{site.data.keyword.appid_short_notm}} 的实例。
  * 您的租户标识。
    * 在服务仪表板的**服务凭证**选项卡中，单击**查看凭证**。您的租户标识会显示在 **TenantID** 字段中。此值用于初始化应用程序。
  * 您所在的 {{site.data.keyword.Bluemix_notm}} 区域。您可以通过查看 UI 来找到您所在的区域。此值用于初始化应用程序。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 区域及对应的 SDK 值</caption>
    <tr>
      <th> Bluemix 区域</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美国南部</td>
      <td> AppID.REGION_US_SOUTH</td>
    </tr>
    <tr>
      <td> 悉尼</td>
      <td> AppID.REGION_SYDNEY</td>
    </tr>
    <tr>
      <td> 英国</td>
      <td> AppID.REGION_UK</td>
    </tr>
  </table>

  * Xcode 项目（V8.1 或更高版本）。
  * CocoaPods（V1.1.0 或更高版本）。


## 安装 {{site.data.keyword.appid_short_notm}} 客户端 SDK
{: #install-appid-sdk}

{{site.data.keyword.appid_short_notm}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 Swift 和 Objective-C Cocoa 项目的依赖项管理器。CocoaPods 会下载工件，并将其提供给项目使用。

1. 创建 Xcode 项目或打开现有项目。
2. 在项目的目录中打开或创建 Podfile。
3. 在项目的目标下，添加“BluemixAppID”pod 的依赖项。确保 `use_frameworks!` 命令也位于目标下。

  例如：


  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. 要下载 `BluemixAppID` 依赖项，请运行以下命令：

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. 打开 Xcode 项目并启用密钥链共享。在**项目设置**下，单击**功能** > **密钥链共享**。
7. 在**项目设置** > **信息** > **URL 类型**下，添加 URL 类型。使用以下值填充**标识**文本框和 **URL 方案**文本框：$(PRODUCT_BUNDLE_IDENTIFIER)


## 初始化 {{site.data.keyword.appid_short_notm}} 客户端 SDK
{: #initialize-client-sdk}

1. 将以下 import 语句添加到 `AppDelegate.swift` 文件中：

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 通过将租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Swift 应用程序中，通常会将初始化代码放置在 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法中，但这不是强制性的。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {:pre}

  * 将 tenantId 替换为 App ID 服务的租户标识。
  * 将 AppID.REGION_UK 替换为您所在的 {{site.data.keyword.appid_short_notm}} 区域。

3. 将以下代码添加到 AppDelegate 文件中。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## 使用登录窗口小部件认证用户
{: #authenticate-login}

初始化 {{site.data.keyword.appid_short_notm}} 客户端 SDK 后，可以通过运行登录窗口小部件来对用户进行认证。登录窗口小部件缺省配置使用 Facebook 和/或 Google 作为认证选项。如果仅配置了其中一项，那么登录窗口小部件不会启动，并且用户会重定向到已配置的 IDP 认证屏幕。



1. 将以下 import 语句添加到要在其中使用 SDK 的文件中。

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 运行以下命令来启动该窗口小部件。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## 访问用户属性
{: #accessing}

获取访问令牌时，还可获取对用户保护的属性端点的访问权。使用以下 API 方法可获取访问权：

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性：

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {:pre}


### 匿名登录
{: #anonymous notoc}

通过 {{site.data.keyword.appid_short_notm}}，您可以匿名登录；请参阅[匿名身份](/docs/services/appid/user-profile.html#anonymous)。

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {:pre}

### 渐进式认证
{: #progressive notoc}

持有匿名访问令牌时，用户可以通过将令牌传递到 loginWidget.launch 方法来成为已识别用户：

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

匿名登录后，会执行渐进式认证，即便在未传递访问令牌的情况下调用了登录窗口小部件时也是如此，因为服务使用的是最后一次收到的令牌。如果要清除存储的令牌，请运行以下命令：

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## 后续步骤
{: #next-steps}

初始设置身份提供者时，{{site.data.keyword.appid_short_notm}} 提供了缺省配置。缺省配置只能用于开发方式。在发布应用程序之前，请将缺省 [Facebook](/docs/services/appid/identity-providers.html#facebook) 和 [Google](/docs/services/appid/identity-providers.html#google) 配置更新为您自己的凭证。
