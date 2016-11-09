---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# Sending requests with IMFURLProtocol
{: #imfurl}

In some cases, you might not be able to use the `IMFResourceRequest` class for sending requests to resources protected by {{site.data.keyword.amafull}}, such as when a request to a protected resource is sent by some third-party code. A possible solution is use the `IMFURLProtocol` API, along with the standard `NSURLRequest (NSMutableURLRequest)` call.

**Note:** The  `IMFURLProtocol` API is available only from the  {{site.data.keyword.amashort}} Objective-C SDK.

## Installing the `IMFURLProtocol` pod
{: #imfurl-pod}

Use CocoaPods to install the `IMFURLProtocol` pod. 

Edit the Podfile file and add the following line and run:
```Bash
pod 'IMFURLProtocol'
```

Then, reference `IMFURLProtocol.h` from your iOS project.

## Sending requests with the `IMFURLProtocol` API
{: #imfurl-send}

1. Import the `IMFURLProtocol.h` file in the class you are using to send the request.
2. Implement the `NSURLConnectionDataDelegate` API in a class that is passed as a delegate to the `NSURLConnection` class.
3. Register an instance of `IMFURLProtocol` with the `IMFURLProtocol:registerIMFURLProtocol` method.
4. Register the protected resource path with the `IMFURLProtocol:registerProtectedResourceWithPath` method.
5. Create a `NSMutableURLRequest` and set its properties as required for a regular request to a resource.
6. Set up `NSURLConnection` with the request and delegate that were created in previous steps and send it using `NSURLConnection:start`.
7. The response is processed by a `NSURLConnectionDataDelegate`.

## Sample code
{: #imfurl-sample}

This example shows how to register `IMFURLProtocol` and send a standard request to protected resource.

### Step 1: Add protocol implementation and process the response
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

### Step 2: Register the IMFURLProtocol class and define a path to protected resource
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
