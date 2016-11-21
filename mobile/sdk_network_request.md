---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-17"

---
# Making a network request
{: #sdk-network-request}

You can also use the `BMSCore` SDK to make network requests to any resource.

## Android
{: #request-android}

For Android, you can use the `Request` class to make network requests.

1. Make sure you have [imported the Client SDK and initialized it](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) in your Android application. 
	
2. Make a network request.

	```
	public void makeGetCall() {
		Thread thread = new Thread(new Runnable() {
			@Override
			public void run() {
				try  {
					Request request = new Request("http://httpbin.org/get", "GET");
					request.send(null, null);
				} catch (Exception e) {
					// Handle Failure here.
				}
			}
		});
		thread.start();
	}
	```
	{: codeblock}

## iOS
{: #bmsurl-ios}

For iOS, you can use `BMSURLSession` to make network requests by creating data tasks and upload tasks to send and receive data. Follow these steps to create and send a data task by using a completion handler to parse the response.

For more information about update tasks, see the `BMSCore` SDK [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core).

1. Make sure you have [imported the Client SDK and initialized it](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) in your iOS application.

2. Create a data task by using a completion handler to parse the response.

#### Swift 3.0
{: ios-swift3-network-requests}

```
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.setValue("value", forHTTPHeaderField: "key")

let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in

    if let httpResponse = response as? HTTPURLResponse {
        print("Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        print("Response data: \(responseString)")
    }
    if let error = error {
        print("Error: \(error)")
    }
}.resume()
```
{: codeblock}

#### Swift 2.2
{: ios-swift23-network-requests}

```
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.setValue("value", forHTTPHeaderField: "key")

let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in

    if let httpResponse = response as? NSHTTPURLResponse {
        print("Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        print("Response data: \(responseString)")
    }
    if let error = error {
        print("Error: \(error)")
    }
}.resume()
```
{: codeblock}
