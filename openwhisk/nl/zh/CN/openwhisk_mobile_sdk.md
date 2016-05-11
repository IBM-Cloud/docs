---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 {{site.data.keyword.openwhisk_short}} 移动 SDK
{: #openwhisk_mobile_sdk}
*上次更新时间：2016 年 3 月 28 日*

{{site.data.keyword.openwhisk}} 提供了用于 iOS 和 watchOS 2 设备的移动 SDK，支持移动应用程序轻松触发远程触发器以及调用远程操作。Android 版本当前不可用；Android 开发者可直接使用 {{site.data.keyword.openwhisk}} REST API。
{: shortdesc}

移动 SDK 是用 Swift 2.2 编写的，支持 iOS 9 及更高发行版。

## 向应用程序添加 SDK
{: #openwhisk_add_sdk}
可以使用 CocoaPods、Carthage 或从源代码目录安装移动 SDK。

### 使用 CocoaPods 安装 

{{site.data.keyword.openwhisk_short}} 移动 SDK 可通过 CocoaPods 进行公共分发。假定 CocoaPods 已安装，请将以下行放到入门模板应用程序项目目录中名为“Podfile”的文件中。 

```
source 'https://github.com/openwhisk/openwhisk-podspecs.git'

use_frameworks!

target 'MyApp' do
     platform :ios, '9.0'
     pod 'OpenWhisk'
end

target 'MyApp WatchKit Extension' do
     platform :watchos, '2.0'
     pod 'OpenWhisk-Watch'
end
```
{: codeblock}

在命令行中，输入“pod install”。这将安装用于具有 watchOS 2 扩展的 iOS 应用程序的 SDK。使用 CocoaPods 为应用程序创建的工作空间文件在 Xcode 中打开项目。

### 使用 Carthage 安装

在应用程序的项目目录中创建文件并命名为“Cartfile”。在 Cartfile 中放入以下行：
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Or latest version
```
{: codeblock}

在命令行中，输入“carthage update --platform ios”。Carthage 会下载并构建 SDK，在应用程序的项目目录中创建名为 Carthage 的目录，然后将 OpenWhisk.framework 文件放入 Carthage/build/iOS 中。将 OpenWhisk.framework 添加到 Xcode 项目中的嵌入框架。

### 通过源代码安装

源代码在 https://github.com/openwhisk//openwhisk-client-swift.git 中提供。使用 Xcode 中的 OpenWhisk.xcodeproj 文件打开项目。该项目包含“OpenWhisk”和“OpenWhiskWatch”这两个方案，分别用于 iOS 和 WathOS2。针对需要的目标构建项目，然后将生成的框架添加到应用程序（通常位于 ~/Library/Developer/Xcode/DerivedData/your app name 中）。

## 安装入门模板应用程序示例
{: #openwhisk_install_sdkstart}

可以使用 {{site.data.keyword.openwhisk_short}} CLI 来下载用于嵌入 {{site.data.keyword.openwhisk_short}} SDK 框架的示例代码。  

要安装入门模板应用程序示例，请输入以下命令：
```
wsk sdk install iOS
```
这将下载包含入门模板应用程序的 zip 文件。在项目目录中有一个 Podfile。通过终端运行“pod install”以安装 SDK。
{: pre}

## SDK 入门
{: #openwhisk_sdk_getstart}

要快速入门和熟悉运用，请使用 {{site.data.keyword.openwhisk_short}} API 凭证创建 WhiskCredentials 对象，然后通过该对象创建 {{site.data.keyword.openwhisk_short}} 实例。

例如，在 Swift 2.1 中，使用以下示例代码来创建凭证对象：

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

在上面的示例中，传入的是从 {{site.data.keyword.openwhisk_short}} 中获取的 `myKey` 和 `myToken`。可以使用以下 CLI 命令来检索密钥和令牌：

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

冒号前后的字符串分别为密钥和令牌。

## 调用 {{site.data.keyword.openwhisk_short}} 操作
{: #openwhisk_sdk_invoke}


要调用远程操作，可以使用操作名称来调用 `invokeAction`。可以指定该操作所属的名称空间，或者使其保留为空以接受缺省名称空间。使用字典来根据需要将参数传递到该操作。

例如：

```
// In this example, we are invoking an action to print a message to the OpenWhisk Console
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Error invoking action \(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }

    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

在上面的示例中，您使用缺省名称空间调用了 `helloConsole` 操作。

## 触发 {{site.data.keyword.openwhisk_short}} 触发器
{: #openwhisk_sdk_fire}

要触发远程触发器，可以调用 `fireTrigger` 方法。使用字典来根据需要传入参数。

```
// In this example we are firing a trigger when our location has changed by a certain amount

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
        }
    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

在上面的示例中，触发的是名为 `locationChanged` 的触发器。

## 使用返回结果的操作
{: #openwhisk_sdk_actionresult}

如果操作会返回结果，请在 invokeAction 调用中将 hasResult 设置为 true。这将在 reply 字典中返回操作的结果，例如：

```
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //do something
            print("Error invoking action \(error.localizedDescription)")

        } else {
var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

缺省情况下，SDK 只会返回激活标识，以及所调用操作生成的任何结果。要获取整个响应对象的元数据（包括 HTTP 响应状态码），请使用以下设置：

```
whisk.verboseReplies = true
```
{: codeblock}

## 配置 SDK
{: #openwhisk_sdk_configure}

可以通过 baseURL 参数将 SDK 配置为使用 {{site.data.keyword.openwhisk_short}} 的不同安装。例如：

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

在此示例中，使用的是在 localhost:8080 上运行的安装。如果未指定 baseUrl，那么移动 SDK 将使用在 https://openwhisk.ng.bluemix.net 上运行的实例。

可以传入定制 NSURLSession，以便在需要特殊网络处理的情况下使用。例如，您自己可能有使用自签名证书的 {{site.data.keyword.openwhisk_short}} 安装：

```
// create a network delegate that trusts everything
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// create an NSURLSession that uses the trusting delegate
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// set the SDK to use this urlSession instead of the default shared one
whisk.urlSession = session
```
{: codeblock}

### 支持限定名

所有操作和触发器都具有由名称空间、包以及操作名称或触发器名称组成的标准名称。SDK 调用操作或触发触发器时，可以接受这些标准名称作为参数。SDK 还提供了接受类似 `/mynamespace/mypackage/nameOfActionOrTrigger` 的标准名称的函数。限定名字符串支持所有 {{site.data.keyword.openwhisk_short}} 用户具有的名称空间和包的未指定缺省值，因此以下解析规则适用：

- qName = "foo" results in namespace = default, package = default, action/trrigger = "foo"
- qName = "mypackage/foo" results in namespace = default, package = mypackage, action/trigger = "foo"
- qName = "/mynamespace/foo" results in namespace = mynamespace, package = default, action/trigger = "foo"
- qName = "/mynamespace/mypackage/foo results in namespace = mynamespace, package = mypackage, action/trigger = "foo"

其他所有组合都会发出 WhiskError.QualifiedName 错误。因此，使用限定名时，必须将调用包装在“`do/try/catch`”构造中。

### SDK 按钮

为了方便起见，SDK 包含 `WhiskButton`，用于扩展 `UIButton` 以允许其调用操作。要使用 `WhiskButton`，请遵循以下示例：

```
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Call this when you detect a press event, e.g. in an IBAction, to invoke the action
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})

// or alternatively you can set up a "self contained" button that listens for press events on itself and invokes an action

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // use qualified name API which requires do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
{: codeblock}
