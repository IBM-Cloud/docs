---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# 使用 IMFURLProtocol 发送请求
{: #imfurl}

在某些用例中，您可能无法使用 `IMFResourceRequest` 类向受 {{site.data.keyword.amafull}} 保护的资源发送请求；例如，对受保护资源的请求是通过一些第三方代码发送时。可能的解决方案是使用 `IMFURLProtocol` API 以及标准 `NSURLRequest (NSMutableURLRequest)` 调用。

**注：**只有通过 {{site.data.keyword.amashort}} Objective-C SDK，才能使用 `IMFURLProtocol` API。

## 安装 `IMFURLProtocol` pod
{: #imfurl-pod}

使用 CocoaPods 来安装 `IMFURLProtocol` pod。 

编辑 Podfile 文件，添加以下行并运行：
```Bash
pod 'IMFURLProtocol'
```

然后，从 iOS 项目中引用 `IMFURLProtocol.h`。

## 使用 `IMFURLProtocol` API 发送请求
{: #imfurl-send}

1. 将 `IMFURLProtocol.h` 文件导入要用于发送请求的类中。
2. 在作为代表传递到 `NSURLConnection` 类的类中实现 `NSURLConnectionDataDelegate` API。
3. 使用 `IMFURLProtocol:registerIMFURLProtocol` 方法注册 `IMFURLProtocol` 的实例。
4. 使用 `IMFURLProtocol:registerProtectedResourceWithPath` 方法注册受保护资源路径。
5. 创建 `NSMutableURLRequest`，并根据针对资源的常规请求的需要来设置其属性。
6. 通过先前步骤中创建的请求和代表来设置 `NSURLConnection`，并使用 `NSURLConnection:start` 发送 NSURLConnection。
7. 响应由 `NSURLConnectionDataDelegate` 进行处理。

## 样本代码
{: #imfurl-sample}

此示例显示了如何注册 `IMFURLProtocol`，以及如何向受保护资源发送标准请求。

### 步骤 1：添加协议实施并处理响应
{: #imfurl-sample1}
```Swift
import Foundation

class ViewController : UIViewController, NSURLConnectionDataDelegate {func connection(connection: NSURLConnection,
								didReceiveResponse response: NSURLResponse) {println("\(response.description)")
	}

	func connection(connection: NSURLConnection, didReceiveData data: NSData) {
		var text = NSString(data: data, encoding: NSUTF8StringEncoding)
		println("\(text)")
	}

	func connection(connection: NSURLConnection, didFailWithError error: NSError) {
		println("\(error.description)")
	}
}
```

### 步骤 2：注册 IMFURLProtocol 类，并定义受保护资源的路径
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)// Send a standard request
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
