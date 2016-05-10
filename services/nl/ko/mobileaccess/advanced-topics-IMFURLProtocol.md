---
copyright:
  years: 2015, 2016
---
# iOS 애플리케이션에서 IMFURLProtocol 사용
{: #imfurl}
보호된 자원에 대한 요청을 일부 써드파티 코드가 전송하는 경우와 같은 고급 수준의 경우 요청을 보호된 자원으로
전송하는 데 `IMFResourceRequest` 클래스를 사용하지 못할 수 있습니다. 가능한 솔루션은
`IMFURLProtocol` API를 표준 `NSURLRequest (NSMutableURLRequest)` 호출과 함께 사용하는 것입니다. 

## `IMFURLProtocol` Pod 설치
{: #imfurl-pod}

CocoaPods를 사용하여 `IMFURLProtocol` Pod를 설치할 수 있습니다. 그런 다음 iOS 프로젝트에서
`IMFURLProtocol.h`를 참조할 수 있습니다. 

## IMFURLProtocol API를 사용하여 요청 전송
{: #imfurl-send}

1. 요청 전송에 사용할 클래스에서 `IMFURLProtocol.h` 파일을 가져오십시오. 
2. `NSURLConnection` 클래스에 위임자로 전달되는 클래스에서 `NSURLConnectionDataDelegate`
API를 구현하십시오. 
3. `IMFURLProtocol:registerIMFURLProtocol` 메소드를 사용하여 `IMFURLProtocol`의 인스턴스를 등록하십시오. 
4. `IMFURLProtocol:registerProtectedResourceWithPath` 메소드를 사용하여 보호된 자원 경로를 등록하십시오. 
5. `NSMutableURLRequest`를 작성하고 자원에 대한 일반 요청에 필요한 해당 특성을 설정하십시오. 
6. 이전 단계에서 작성한 요청과 위임을 사용하여 `NSURLConnection`을 설정하고
`NSURLConnection:start`를 사용하여 전송하십시오. 
7. 응답은 `NSURLConnectionDataDelegate`에서 처리합니다. 

## 샘플 코드
{: #imfurl-sample}

이 예는 `IMFURLProtocol`을 등록하고 표준 요청을 보호된 자원으로 전송하는 방법을 보여줍니다. 

### 1단계: 프로토콜 구현 추가 및 응답 처리
{: #imfurl-sample1}
```Swift
import Foundation

class ViewController : UIViewController, NSURLConnectionDataDelegate {


	func connection(connection: NSURLConnection, didReceiveResponse response: NSURLResponse) {


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

### 2단계: IMFURLProtocol 클래스 등록 및 보호된 자원 경로 정의
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
