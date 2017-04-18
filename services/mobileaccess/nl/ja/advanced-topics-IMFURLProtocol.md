---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# IMFURLProtocol を使用した要求送信
{: #imfurl}

場合によっては、 {{site.data.keyword.amafull}} によって保護されたリソースに要求を送信するために `IMFResourceRequest` クラスを使用できないことがあります (例えば、何らかのサード・パーティー・コードによって保護リソースに要求が送信される場合など)。考えられる解決策の 1 つは、標準 `NSURLRequest (NSMutableURLRequest)` 呼び出しと一緒に `IMFURLProtocol` API を使用することです。

**注:** `IMFURLProtocol` API は、{{site.data.keyword.amashort}} Objective-C SDK からのみ使用可能です。

## `IMFURLProtocol` pod のインストール
{: #imfurl-pod}

CocoaPods を使用して `IMFURLProtocol` pod をインストールします。 

Podfile ファイルを編集して以下の行を追加し、実行します。
```Bash
pod 'IMFURLProtocol'
```

次に、iOS プロジェクトから `IMFURLProtocol.h` を参照します。

## `IMFURLProtocol` API を使用した要求送信
{: #imfurl-send}

1. 要求を送信するために使用するクラスに `IMFURLProtocol.h` ファイルをインポートします。
2. `NSURLConnection` クラスに代行として渡されるクラスに `NSURLConnectionDataDelegate` API を実装します。
3. `IMFURLProtocol:registerIMFURLProtocol` メソッドを使用して、`IMFURLProtocol` のインスタンスを登録します。
4. `IMFURLProtocol:registerProtectedResourceWithPath` メソッドを使用して、保護リソース・パスを登録します。
5. `NSMutableURLRequest` を作成し、リソースへの通常の要求に必要なプロパティーを設定します。
6. 前のステップで作成された要求および代行を使用して `NSURLConnection` をセットアップし、それを `NSURLConnection:start` を使用して送信します。
7. 応答は `NSURLConnectionDataDelegate` によって処理されます。

## サンプル・コード
{: #imfurl-sample}

この例は、`IMFURLProtocol` を登録し、標準的な要求を保護リソースに送信する方法を示します。

### ステップ 1: プロトコル実装を追加し、応答を処理する
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

### ステップ 2: IMFURLProtocol クラスを登録し、保護リソースへのパスを定義する
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
