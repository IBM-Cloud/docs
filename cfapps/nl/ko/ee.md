---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 시나리오: 엔드-투-엔드 개발
{: #ee}

*마지막 업데이트 날짜: 2016년 4월 18일*

앱을 빌드, 실행 및 배치할 때는
{{site.data.keyword.Bluemix}} 사용자 인터페이스,
플랫폼 및 도구 선택을 사용할 수 있습니다. 이 엔드 투 엔드 개발 시나리오에 따라 시작하십시오.
{:shortdesc}

## 등록
{: #ee_start}

시작하기 전에 우선 [https://console.ng.bluemix.net/](https://console.ng.bluemix.net/)에서 IBM ID를 등록해야 합니다. 그 다음에 {{site.data.keyword.Bluemix_notm}}에 로그인하고
30일 무료 평가판 사용을 시작하십시오. {{site.data.keyword.Bluemix_notm}}에서는
무료 평가판에 대해 2GB의 런타임 메모리와 10개의 서비스 인스턴스 사용을 허용합니다. 

## {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를
사용한 웹 앱 작성
{: #ee_appui}

등록한 후 {{site.data.keyword.Bluemix_notm}}
사용자 인터페이스를 사용하여 첫 번째 앱의 빌드를 시작합니다. 

{{site.data.keyword.Bluemix_notm}}에서
앱은 조직 및 영역과 연관됩니다. 조직은 다중 협업자에 의해 소유되고 사용됩니다. 
처음에는 사용자 이름에 따라 이름 지정된 기본 조직을 갖게 되며 사용자가 유일한 협업자입니다. 이 조직 내에서 영역도 확보합니다.
영역은 앱을 실행하기 위한 환경입니다. 예를 들어,
개발 환경으로 개발 영역을, 테스트 환경으로 테스트 영역을,
프로덕션 환경으로 프로덕션 영역을 확보합니다. 
또한 각 환경은 지역에 속합니다. 
{{site.data.keyword.Bluemix_notm}}에서는
네트워크 대기 시간의 감소, 데이터 개인정보 보호정책 및 가용성 증진을 위해
애플리케이션을 특정 지리적 지역에 배치할 수 있습니다.
세부사항은 지역을 참조하십시오.

이 시나리오에서는 Node.js를 사용하여 웹 앱을 개발하고자 합니다.
현재 미국에 거주하고 있으며 대부분의 앱 사용자도 미국에 있다고 가정합니다. 
네트워크 대기 시간 감소의 장점을 이용할 수 있도록, 사용자 기반에 근접한 앱을 빌드하고 실행하기로 결정합니다. {{site.data.keyword.Bluemix_notm}}에 로그인한 후 오른쪽 상단에서 계정 이름을 클릭하고 **미국 남부** 지역을 선택하십시오. 그리고 다음 단계에 따라 앱을 작성하십시오.

  1. 더하기 단추를 클릭하십시오.
  2. **계산**>**CF 애플리케이션**>**SDK for Node.js**를 선택하십시오.
  3. 앱의 고유 이름(예: TestNode)을 입력하고 **작성**을 클릭하십시오. 앱 이름은 전체 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다. 
  
이제 **코딩 시작** 지시사항이 표시됩니다.
지시사항에 따라 TestNode의 스타터 코드를 다운로드하고 이를 수정 및 배치할 수 있습니다.

앱에는 기본적으로 1개의 인스턴스 및 512MB 메모리 할당량이 지정됩니다. 
메모리를 늘리거나 인스턴스를 더 추가함으로써 앱의 가용성을
높일 수 있습니다(예: 인스턴스당 1GB의 메모리가 있는 3개의 인스턴스). 앱 인스턴스 및 메모리 할당량을 지정하려면 **앱 개요 보기**를 클릭하십시오. 예를 들어, 인스턴스에 대해 3을 입력하고 메모리 할당량에 대해 1GB를 입력한 후에 **저장**을 클릭하십시오.
파일, 로그 및 환경 변수를 보고 문제점을 해결할 수도 있습니다. 

## {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를
사용한 서비스 바인딩
{: #ee_bindui}

앱을 작성한 후에는 앱으로 데이터베이스에 연결하고자 할 수 있습니다. 
이러한 방식으로 데이터베이스 조회 언어를 사용하여 앱 데이터를 저장하고 관찰할 수 있습니다. 이 시나리오에서는 {{site.data.keyword.Bluemix_notm}}에서 제공하는
{{site.data.keyword.cloudant}} 서비스를 사용하기로 결정합니다. 

애플리케이션 내에서 서비스를 사용하려면 서비스 인스턴스를 작성하고
애플리케이션을 서비스 인스턴스에 바인딩해야 합니다. 이를 위해서는 다음 단계를 수행하십시오. 
  1. 앱 개요 페이지에서 **서비스 또는 API 추가**를 클릭하십시오.
  2. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 {{site.data.keyword.cloudant}} 서비스를 선택하십시오.
  3. 서비스 인스턴스의 고유 이름을 입력하거나
{{site.data.keyword.Bluemix_notm}}에서
생성한 기본 이름을 사용하고 **작성**을 클릭하십시오. 
  4. 애플리케이션 다시 스테이징 창이 표시됩니다. 앱을 다시 스테이징하려면 **다시 스테이징**을 클릭하십시오. 
  
이제 앱이 {{site.data.keyword.cloudant}} 서비스에 바인딩되었습니다.
VCAP_SERVICES 환경 변수의 서비스 인스턴스와 통신하기 위한 애플리케이션의 모든 필수 데이터를 찾을 수 있습니다. 예를 들어,
{{site.data.keyword.Bluemix_notm}}는 동일한 가상 머신에서 여러 애플리케이션을
호스팅하므로 애플리케이션이 동일한 HTTP 포트 번호를 사용하여 수신 요청을 받을 수 없습니다. 충돌을 피하기 위해 각 애플리케이션에
고유 포트 번호가 지정됩니다. 이 포트 번호는 VCAP_APP_PORT 변수 하에서 사용 가능합니다.

자세한 정보를 보려면 앱 개요 페이지의 **환경 변수**를 클릭하여 VCAP_SERVICES의 전체 목록을 참조하십시오.
```
{
   "cloudantNoSQLDB": [

      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Shared",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**참고:** 이 환경 변수는 앱이 바인딩된 각 서비스 인스턴스마다 하나의 항목이 있는 JSON 오브젝트의 직렬화입니다. 각 서비스 인스턴스가 제공하는 데이터의 양 및 유형은
서비스에 따라 정해집니다. 앱이 서비스를 사용하지 않는 경우 VCAP_SERVICES는 비어 있는 JSON 오브젝트입니다. 
이 환경 변수는 앱에 서비스를 추가할 때만 사용됩니다. 

## cf cli를 사용하여 앱 빌드
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}}는
앱에서 코딩을 시작할 수 있도록 다수의 도구(예: cf 명령행 인터페이스 및 Eclipse 도구)를 제공합니다. cf 명령행 인터페이스를 선택하여 앱 TestNode에서 코딩을 시작할 수 있습니다.

  1. 우선 앱의 코드를 다운로드하고 개발하십시오. 
  
    1. 앱의 코딩 시작 페이지로 이동하십시오. 
**스타터 코드 다운로드** 단추를 클릭하여 앱 코드를 다운로드하십시오. 
    2. 다운로드한 파일을 디렉토리(예: `C:\test`)로 추출하십시오. 
    3. 로컬 통합 개발 환경에서 코드를 개발하십시오. 
	
  2. **cf** 명령행 인터페이스(CLI)를 설치하십시오. 
  
    1. 운영 체제에 맞는 cf 명령행 도구 설치 프로그램을 다운로드하십시오.
    2. 도구 마법사에 따라 설치를 완료하십시오. 
    3. **cf -v** 명령을 사용하여 cf 명령행 인터페이스의 버전을 확인하십시오. 예:
	
	```
	cf -v
	```
	
    **요구사항:** 항상 cf 명령행 도구의 최신 버전을 사용해야 합니다.
  3. **cf** 명령행 인터페이스를 설치한 후에는 **cf api** 명령을
사용하여 작업할 {{site.data.keyword.Bluemix_notm}} 지역을
지정해야 합니다.
**cf** 명령행 인터페이스는 *https://api.Bluemix_URL*을 사용합니다. 여기서, *Bluemix_URL*은
지역의 URL입니다. 미국 남부 지역의 URL은 {{Domain}}입니다. 다음 명령을 입력하여
{{site.data.keyword.Bluemix_notm}}에 연결하십시오.
  
  ```
  cf api https://api.ng.bluemix.net
	 ```
  
  기타 {{site.data.keyword.Bluemix_notm}} 지역에 연결하는 방법에 대한 자세한 정보는
{{site.data.keyword.Bluemix_notm}} 지역을 참조하십시오. {{site.data.keyword.Bluemix_notm}} 지역을 지정한 후에
사용자가 지정한 위치 정보가 저장됩니다.
  
  4. 그런 다음, cf login 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 있습니다.
  
  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```
  
  5. {{site.data.keyword.Bluemix_notm}}에 로그인한 후에는
{{site.data.keyword.Bluemix_notm}}로 다시 앱을 배치할 준비가 됩니다.
앱 디렉토리 `C:\test`에서 다음 명령을 입력하십시오. 
  
  ```
  cf push TestNode```
  
  **cf push** 명령에 대한 자세한 정보는 앱 업로드를 참조하십시오.
  
  6. 이제 브라우저에서 다음 앱 URL을 입력하여 앱에 액세스할 수 있습니다.```
  http://TestNode.mybluemix.net
  ```

또한 Eclipse 도구와 같은 다른 앱 빌드 도구를 선택할 수도 있습니다. 자세한 정보는
{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 앱의 코딩 시작 페이지를 참조하십시오.

## cf cli를 사용하여 서비스 바인딩
{: #ee_cfbind}

{{site.data.keyword.Bluemix_notm}}에서는
이 시나리오의 앞쪽에서 설명한 대로 Bluemix 사용자 인터페이스를 사용하여 서비스를 추가할 수 있습니다. 그러나
**cf** 명령행 인터페이스를 사용하여 서비스를 바인딩할 수도 있습니다. cf 명령행 인터페이스를 사용하여
{{site.data.keyword.cloudant}} 서비스를 앱 TestNode에 추가하고자 한다고 가정합니다.

앱 내에서 {{site.data.keyword.cloudant}} 서비스를 사용하려면,
Cloudant 서비스 인스턴스를 작성하고 앱을 서비스 인스턴스에 바인딩한 후에 서비스 인스턴스를 사용해야 합니다.
동일한 프로시저가 기타 모든 서비스에 적용됩니다. 

  1. Cloudant NoSQL DB 서비스 인스턴스를 작성하십시오.
  
  cf create-service 명령을 사용하여 서비스의 새 인스턴스를 작성하십시오. 예:
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100```
  
  cf services 명령을 사용하여 작성한 서비스 인스턴스의 목록을 볼 수도 있습니다.
  
  ```
  cf services```
  
  서비스 인스턴스를 작성한 후에는 임의의 애플리케이션을 바인딩하고 사용하는 데 사용할 수 있습니다.
  
  2. 서비스 인스턴스를 앱에 바인딩하십시오. 
  
  서비스 인스턴스를 사용하려면 애플리케이션을 바인딩해야 합니다. 사용자가 작성한 애플리케이션 이름 및 서비스 인스턴스를 지정하고
cf bind-service 명령을 사용하여 서비스 인스턴스를 애플리케이션에 바인딩하십시오.
  
  ```
  cf bind-service TestNode cloudant100```
  
  서비스 인스턴스를 애플리케이션에 바인딩하면 {{site.data.keyword.Bluemix_notm}}가
서비스와 통신할 수 있으며 새 애플리케이션이 해당 서비스 인스턴스와 통신하도록 지정할 수 있습니다. 다른 서비스의 경우,
{{site.data.keyword.Bluemix_notm}}가 바인딩 동안 애플리케이션 및 서비스 인스턴스를
다르게 처리할 수 있습니다. 예를 들어, 일부 서비스는
서비스 인스턴스와 통신하는 각 애플리케이션에 대해 새 테넌트를 작성할 수 있습니다. 서비스는
애플리케이션과 서비스 사이의 통신을 위해 반드시 애플리케이션에 전달되어야 하는
신임 정보 등의 정보를 사용하여 {{site.data.keyword.Bluemix_notm}}에 다시 응답합니다. 

  **참고:** 애플리케이션이 서비스 인스턴스에 바인딩될 때 실행 중이면 애플리케이션이 다시 시작될 때까지
VCAP_SERVICES 환경 변수가 업데이트되지 않습니다. 애플리케이션을 다시 시작하려면 cf restart 명령을 사용하십시오.
  
  3. 서비스 인스턴스를 사용하십시오.
  
  이 시나리오에서는 VCAP_SERVICES 환경 변수에 {{site.data.keyword.cloudant}}의 이 인스턴스에 연결하기 위해
애플리케이션이 사용할 수 있는 다음 항목과 같은 정보가 포함됩니다.
  
  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  예를 들어, Node.js 앱이 다음과 같이 이 정보에 액세스할 수 있습니다.
```
  if (process.env.VCAP_SERVICES) {

        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
"username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **참고:** 샘플 코드에서 표시하듯이, {{site.data.keyword.cloudant}} 서비스 인스턴스에 연결하기 위해 VCAP_SERVICES 환경 변수가 존재하는지 여부를
우선 확인할 수 있습니다. 존재하는 경우, 애플리케이션이 cloudant 변수의 특성을 사용하여 데이터베이스에 액세스할 수 있습니다. 그러나
VCAP_SERVICES 환경 변수가 존재하지 않는 경우에는 제공된 기본값으로 로컬 {{site.data.keyword.cloudant}} 서비스 인스턴스가 사용됩니다.
  
  4. 서비스 인스턴스와 상호작용하십시오.
  
  신임 정보를 사용하여 서비스 인스턴스와 상호작용할 수 있습니다. 취할 수 있는 조치에는 읽기, 쓰기 및 업데이트가 포함됩니다. 다음 예는 JSON 오브젝트를 {{site.data.keyword.cloudant}} 서비스 인스턴스에 삽입하는 방법을 예시합니다.
```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **선택사항:** 서비스 인스턴스를 바인드 해제하거나 삭제하십시오.
  
  서비스 인스턴스가 더 이상 사용되지 않거나 일부 공간을 사용 가능하게 하고자 하는 경우
서비스 인스턴스를 바인드 해제하거나 삭제하고자 할 수 있습니다. 앱에서 서비스 인스턴스를 바인드 해제하려면 **cf unbind-service command** 명령을 사용하고,
서비스 인스턴스를 삭제하려면 **cf delete-service** 명령을 사용하십시오.

  서비스에 대한 자세한 정보는 서비스의 내용을 참조하십시오. {{site.data.keyword.Bluemix_notm}} 환경에서
애플리케이션을 관리하는 데 사용할 수 있는 **cf** 옵션에 대한 자세한 정보를 보려면
**cf** 명령행 인터페이스에서 **cf --help**를 실행하십시오.

  **참고:** 서비스 인스턴스를 삭제하기 전에 더 이상 필요하지 않은지
확인하십시오. 서비스 인스턴스를 삭제하면 해당 서비스 인스턴스와 연관된 모든 데이터가 지워집니다. 삭제된 서비스와 바인딩된 모든 애플리케이션은
애플리케이션이 다시 시작될 때까지 VCAP_SERVICES 환경 변수를 업데이트할 수 없습니다.

## 앱 비용 계산
{: #ee_billing}

30일 무료 평가판이 만료되었지만
{{site.data.keyword.Bluemix_notm}}를 계속 사용하고자 합니다.
{{site.data.keyword.Bluemix_notm}}를
계속 사용하려면 종량과금제 계정 또는 구독 계정에 대한 신용카드 정보를 추가해야 합니다.
단,
{{site.data.keyword.Bluemix_notm}}에서는
지불 계정으로 변환한 후에도
대부분의 런타임 프레임워크 및 서비스에 대해서는 무료 사용량을 계속 제공합니다. 사용한 양이 무료 사용량을
초과하지 않으면 {{site.data.keyword.Bluemix_notm}}에 의해 비용이 부과되지 않습니다.

{{site.data.keyword.Bluemix_notm}}에서는
앱 비용을 볼 수 있도록 추정기 및 계산기를 제공합니다. 다음과 같은 방법으로 TestNode의 비용을 볼 수 있습니다.

  * 대시보드에서 TestNode를 클릭하십시오. 그리고 개요 페이지에서 **이 앱의 비용 추정**을 클릭하여 **SDK for Node.js** 런타임 및 지원의 가격 및 앱의 월별 총액을 보십시오.
  
  * 또는 가격 책정 시트 페이지에서 앱의 서비스 및 런타임의 월별 사용량을 입력하십시오. 예: 각 인스턴스마다 1GB의 메모리가 있는 **SDK for Node.js**의 3개 인스턴스. 월별 가격이 계산되어 표시됩니다. 

또한 런타임 및 서비스의 가격을 계속 추가하고 무료 사용량을 제외하는
방법을 통해 앱 비용을 수동으로 계산할 수도 있습니다.
자세한 정보는 수동으로 비용 계산을 참조하십시오.

## 앱 제거
{: #ee_removing}

앱을 계속 빌드함에 따라 할당량이 한계에 접근할 수 있습니다. 그러나 더 이상 필요하지 않은 일부 앱이
여전히 할당량을 차지하고 있을 수 있습니다. {{site.data.keyword.Bluemix_notm}}에서
공간을 사용 가능하게 하기 위해 언제든지 쉽게 앱을 삭제할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 앱 개요 페이지로 이동한 다음
**메뉴** 아이콘을 클릭하고 더 이상 사용하지 않는 앱을 삭제하십시오. 또한 **cf delete** 명령을
사용하여 앱을 삭제할 수도 있습니다.
