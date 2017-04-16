---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# 使用 IMFURLProtocol 傳送要求
{: #imfurl}

在部分情況下，您可能無法使用 `IMFResourceRequest` 類別將要求傳送給 {{site.data.keyword.amafull}} 所保護的資源；例如，透過某個協力廠商程式碼傳送對受保護資源的要求時。可能的解決方案是使用 `IMFURLProtocol` API，以及標準 `NSURLRequest (NSMutableURLRequest)` 呼叫。

**附註：**`IMFURLProtocol` API 只能從 {{site.data.keyword.amashort}} Objective-C SDK 取得。

## 安裝 `IMFURLProtocol` pod
{: #imfurl-pod}

請使用 CocoaPods 來安裝 `IMFURLProtocol` pod。 

編輯 Podfile 檔，然後新增下行並執行：
```Bash
pod 'IMFURLProtocol'
```

然後，從 iOS 專案中參照 `IMFURLProtocol.h`。

## 使用 `IMFURLProtocol` API 傳送要求
{: #imfurl-send}

1. 在用來傳送要求的類別中，匯入 `IMFURLProtocol.h` 檔案。
2. 在作為 `NSURLConnection` 類別的委派而傳遞的類別中，實作 `NSURLConnectionDataDelegate` API。
3. 使用 `IMFURLProtocol:registerIMFURLProtocol` 方法，登錄 `IMFURLProtocol` 實例。
4. 使用 `IMFURLProtocol:registerProtectedResourceWithPath` 方法，登錄受保護資源的路徑。
5. 建立 `NSMutableURLRequest`，並視需要為資源的一般要求設定其內容。
6. 使用先前步驟中所建立的要求及委派來設定 `NSURLConnection`，並使用 `NSURLConnection:start` 進行傳送。
7. 回應是透過 `NSURLConnectionDataDelegate` 進行處理。

## 範例程式碼
{: #imfurl-sample}

此範例顯示如何登錄 `IMFURLProtocol`，以及如何向受保護的資源傳送標準要求。

### 步驟 1：新增通訊協定實作並處理回應
{: #imfurl-sample1}
```Swift
import Foundation

class ViewController : UIViewController, NSURLConnectionDataDelegate {

	func connection(connection: NSURLConnection,
								didReceiveResponse response: NSURLResponse) {

		println("\(response.description)")
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

### 步驟 2：登錄 IMFURLProtocol 類別並定義受保護資源的路徑
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)

	// Send a standard request
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
