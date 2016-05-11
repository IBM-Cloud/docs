---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 조치 작성 및 호출
{: #openwhisk_actions}

*마지막 업데이트 날짜: 2016년 3월 22일*

조치는 {{site.data.keyword.openwhisk}} 플랫폼에서 실행되는 Stateless 코드 스니펫입니다. 조치는 JavaScript 함수, Swift 함수 또는 Docker 컨테이너에 패키지화된 사용자 정의 실행 가능 프로그램일 수 있습니다. 예를 들어, 이미지에서 얼굴을 발견하거나 일련의 API 호출을 집계하거나 트윗을 게시하기 위해 조치를 사용할 수 있습니다.
{:shortdesc}

조치는 명시적으로 호출되거나 이벤트에 대한 응답으로 실행될 수 있습니다. 어느 경우에나 조치 실행의 결과는 고유 활성화 ID에 의해 식별된 활성화 레코드입니다. 조치에 대한 입력 및 조치의 결과는 키-값 쌍의 사전입니다. 이 때, 키는 문자열이며 값은 유효한 JSON 값입니다.

조치는 다른 조치에 대한 호출 또는 정의된 조치 순서로 구성될 수 있습니다.

## JavaScript 조치 작성
{: #openwhisk_create_action_js}

다음 절에서는 JavaScript에서 조치에 대해 작업하는 방법을 안내합니다. 단순 조치의 작성 및 호출부터 시작하여 조치에 매개변수 추가, 매개변수를 사용하는 해당 조치 호출, 기본 매개변수 설정 및 해당 호출, 비동기 조치 작성에 대해 설명하며 최종적으로 조치 시퀀스로 작업하는 방법에 대해 설명합니다.


### 단순 JavaScript 조치 작성 및 호출
{: #openwhisk_single_action_js}

다음 단계 및 예를 검토하여 첫 번째 JavaScript 조치를 작성하십시오.

1. 다음 컨텐츠를 사용하여 JavaScript 파일을 작성하십시오. 이 예에서 파일 이름은 'hello.js'입니다.
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  JavaScript 파일은 추가 기능을 포함할 수 있습니다. 그러나 편의상 `main`을 호출하는 함수는 조치에 대한 시작점을 제공하기 위해 존재해야 합니다.

2. 다음 JavaScript 함수에서 조치를 작성하십시오. 이 예에서 조치를 'hello'라고 합니다.

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  {: screen}

3. 작성한 조치 나열:
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  방금 작성한 `hello` 조치를 볼 수 있습니다.

4. 조치를 작성한 후에 'invoke' 명령을 사용하여 {{site.data.keyword.openwhisk_short}}의 클라우드 내에서 이를 실행할 수 있습니다. 명령에 플래그를 지정하여 *블로킹* 호출 또는 *비블로킹* 호출을 사용하여 조치를 호출할 수 있습니다. 블로킹 호출은 조치가 실행을 완료하고 결과를 리턴할 때까지 대기합니다. 이 예에서는 블로킹 매개변수인 `-blocking`을 사용합니다.

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  명령은 두 가지 중요한 정보 조각을 출력합니다.
  * 활성화 ID(`44794bd6aab74415b4e42a308d880e5b`)
  * 호출 결과

  이 경우의 결과는 JavaScript 함수에 의해 리턴되는 `Hello world` 문자열입니다. 활성화 ID는 나중에 로그 또는 활성화의 결과를 검색하는 데 사용될 수 있습니다.  

5. 지금 당장 조치 결과가 필요하지 않은 경우, `--blocking` 플래그를 생략하여 비블로킹 호출을 작성할 수 있습니다. 나중에 활성화 ID를 사용하여 결과를 얻을 수 있습니다. 다음 예를 참조하십시오.

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

6. 활성화 ID를 기록하는 것을 잊은 경우, 가장 최신에서 가장 오래된 순서로 정렬된 활성화 목록을 얻을 수 있습니다. 다음 명령을 실행하여 활성화 목록을 얻으십시오.

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  {: screen}

### 조치에 매개변수 전달
{: #openwhisk_adding_parameters_js}

매개변수는 호출될 때 조치에 전달될 수 있습니다.

1. 조치에 매개변수를 사용하십시오. 예를 들어, 다음 컨텐츠로 'hello.js' 파일을 업데이트하십시오.
  
  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  입력 매개변수가 JSON 오브젝트 매개변수로 `main` 함수에 전달됩니다. 이 예에서 `name` 및 `place` 매개변수가 `params` 오브젝트에서 검색됩니다.

2. `name` 및 `place` 매개변수값을 전달하면서 `hello` 조치를 업데이트하고 조치를 호출하십시오. 다음 예를 참조하십시오.
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  `--param` 옵션을 사용하여 매개변수 이름 및 값을 지정하고 `--result` 옵션을 사용하여 호출 결과만 표시하는 방법에 주의하십시오.

### 기본 매개변수 설정
{: #openwhisk_binding_actions}

다중으로 이름 지정된 매개변수를 사용하여 조치를 호출할 수 있습니다. 이전 예에서 `hello` 조치를 호출하려면 두 개의 매개변수, 즉, 개인의 *name* 및 출신 *place*가 필요합니다.

모든 매개변수를 매번 조치에 전달하기보다 특정 매개변수를 바인딩할 수 있습니다. 다음은 조치가 "Vermont"라는 위치를 기본값으로 사용하도록 *place* 매개변수를 바인딩하는 예입니다.
 
1. `--param` 옵션을 사용하여 매개변수값을 바인딩하도록 조치를 업데이트하십시오.

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. 이번에는 `name` 매개변수만 전달하여 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  조치를 호출할 때 장소 매개변수를 지정할 필요가 없습니다. 호출 시에 매개변수값을 지정하여 바인딩된 매개변수를 겹쳐쓸 수 있습니다.

3. `name` 및 `place` 값을 둘 다 전달하여 조치를 호출하십시오. 나중에 조치에 바인딩된 값을 겹쳐씁니다.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### 비동기 조치 작성
{: #openwhisk_asynchrony_js}

콜백 함수에서 계속 실행되는 JavaScript 함수는 `main` 함수가 리턴한 후에 활성화 결과를 리턴해야 하는 경우가 있습니다. 조치에서 `whisk.async()` 및 `whisk.done()` 함수를 사용하여 이를 달성할 수 있습니다.

1. `asyncAction.js`라는 파일에 다음 컨텐츠를 저장하십시오.

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  `main` 함수가 즉시 리턴하고 `whisk.async()`가 이 활성화가 계속 실행되어야 함을 표시하는 값을 리턴합니다.

  이 경우에 `setTimeout()` JavaScript 함수는 콜백 함수를 호출하기 전에 20초 동안 대기하며 `whisk.done()`에 대한 호출이 활성화가 완료되었음을 표시합니다.

2. 다음 명령을 실행하여 조치를 작성하고 호출하십시오.

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

  비동기 조치의 블로킹 호출이 수행되었습니다.

3. 활성화 완료에 걸린 시간을 보려면 활성화 로그를 페치하십시오.

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  활성화 레코드에서 `start` 및 `end` 시간소인을 비교하여 이 활성화 완료에 20초 약간 넘게 소요되었음을 알 수 있습니다.


### 외부 API를 호출하기 위해 조치 사용
{: #openwhisk_apicall_action}

지금까지는 예에 자체 포함된 JavaScript 함수가 있었습니다. 외부 API를 호출하는 조치도 작성할 수 있습니다.

이 예에서는 Yahoo 날씨 서비스를 호출하여 특정 위치에서의 현재 상태를 얻습니다. 

1. `weather.js`라는 파일에 다음 컨텐츠를 저장하십시오.
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  예에서 조치가 JavaScript `request` 라이브러리를 사용하여 Yahoo Weather API에 대한 HTTP 요청을 작성하고 JSON 결과에서 필드를 추출합니다. [참조](./openwhisk_reference.html#runtime_ref_runtime_environment)에서는 사용자의 조치에서 사용할 수 있는 Node.js 패키지에 대해 자세히 설명합니다.
  
  또한 이 예에서는 비동기 조치에 대한 필요성을 표시합니다. 함수가 리턴할 때 이 조치의 결과를 아직 사용할 수 없음을 표시하기 위해 조치에서 `whisk.async()`를 리턴합니다. 대신 HTTP 호출이 완료되어 인수로 `whisk.done()` 함수에 전달된 후에 `request` 콜백에서 결과를 사용할 수 있습니다.

2. 다음 명령을 실행하여 조치를 작성하고 호출하십시오.
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### 조치 시퀀스 작성
{: #openwhisk_create_action_sequence}

일련의 조치를 연결하는 조치를 작성할 수 있습니다.

첫 번째 시퀀스를 작성하는 데 사용할 수 있는 `/whisk.system/util` 패키지에서 여러 유틸리티 조치가 제공됩니다. [패키지](./openwhisk_packages.html) 절에서 패키지에 대한 자세한 정보를 볼 수 있습니다.

1. `/whisk.system/util` 패키지의 조치를 표시합니다.
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  이 예에서는 `cat` 및 `sort` 조치를 사용할 것입니다.

2. 한 조치의 결과가 다음 조치에 인수로 전달되도록 조치 시퀀스를 작성하십시오.
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  이 조치 시퀀스는 텍스트의 일부 행을 배열로 변환하여 해당 행을 정렬합니다.

3. 조치 시퀀스를 호출하기 전에 텍스트 몇 행이 있는 'haiku.txt'를 작성하십시오.

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. 조치 호출:
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  결과에서 행이 정렬된 것을 볼 수 있습니다.

**참고**: 다중으로 이름 지정된 매개변수를 사용하여 조치 시퀀스를 호출하는 방법에 대한 정보는 [기본 매개변수 설정](./openwhisk_actions.html##openwhisk_binding_actions)을 참조하십시오.

## Swift 조치 작성
{: #openwhisk_actions_swift}

Swift 조치 작성 프로세스는 JavaScript 조치 작성 프로세스와 유사합니다. 다음 절에서는 단일 Swift 조치를 작성 및 호출하여 해당 조치에 매개변수를 추가하는 방법에 대해 안내합니다.

또한 온라인 [Swift 샌드박스](https://swiftlang.ng.bluemix.net)를 사용하여 시스템에 Xcode를 설치할 필요 없이 Swift 코드를 테스트할 수 있습니다.

### 조치 작성 및 호출
{: #openwhisk_actions_invoke_swift}

조치는 단순히 최상위 레벨의 Swift 함수입니다. 예를 들어, 다음 컨텐츠를 사용하여 `hello.swift`라는 파일을 작성하십시오.

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

JavaScript 조치와 같이 Swift 조치도 항상 사전을 이용하여 사전을 생성합니다.

다음과 같이 이 함수에서 `helloSwift`라는 {{site.data.keyword.openwhisk_short}} 조치를 작성할 수 있습니다.

```
wsk action create helloSwift hello.swift
```
{: pre}

명령행 및 `.swift` 소스 파일을 사용할 때 (JavaScript 조치와 반대로) Swift 조치를 작성함을 지정할 필요가 없습니다. 도구가 파일 확장자에서 이를 판별합니다.

조치 호출은 JavaScript 호출과 마찬가지로 Swift 호출에 대해서도 동일합니다.

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**주의:** Swift 조치는 Linux 환경에서 실행됩니다. Swift on Linux는 아직
개발 중이며 {{site.data.keyword.openwhisk_short}}에서는 일반적으로 사용 가능한 가장 최신 릴리스를
사용합니다. 이러한 최신 릴리스가 항상 안정적인 것은 아닙니다. 또한 {{site.data.keyword.openwhisk_short}}와
함께 사용되는 Swift의 버전이 XCode on MacOS의 안정적인 릴리스의 Swift 버전과 일치하지 않을 수 있습니다.

## Docker 조치 작성
{: #openwhisk_actions_docker}

{{site.data.keyword.openwhisk_short}} Docker 조치를 사용하면 사용자의 조치를 어떤 언어로든 작성할 수 있습니다.

사용자의 코드가 실행 가능 2진으로 컴파일되어 Docker 이미지에 임베드됩니다. 2진 프로그램은 `stdin`에서 입력을 가져와서 `stdout`을 통해 응답함으로써 시스템과 상호작용합니다.

전제조건으로, Docker 허브 계정이 있어야 합니다. 무료 Docker ID 및 계정을 설정하려면 [Docker 허브](https://hub.docker.com){: new_window}로 이동하십시오.

다음 지시사항에서는 사용자 ID가 "janesmith"이며 비밀번호가 "janes_password"라고 가정합니다. CLI가 이미 설정되었다고 가정하면 {{site.data.keyword.openwhisk_short}}에 의해 사용될 사용자 정의 2진을 설정하기 위해 세 단계가 필요합니다. 그런 다음 업로드된 Docker 이미지가 조치로 사용될 수 있습니다.

1. Docker 스켈레톤을 다운로드하십시오. 다음과 같이 CLI를 사용하여 다운로드할 수 있습니다.

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  The Docker skeleton is now installed at the current directory.
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  스켈레톤은 사용자 정의 2진 형식으로 사용자의 코드를 삽입할 수 있는 Docker 컨테이너 템플리트입니다.

2. Docker 스켈레톤에 사용자 정의 2진을 설정하십시오. 스켈레톤은 사용할 수 있는 C 프로그램을 이미 포함하고 있습니다.

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  필요에 따라 이 파일을 수정할 수 있습니다.

3. Docker 이미지를 빌드하고 제공된 스크립트를 사용하여 이를 업로드하십시오. 먼저 `docker login`을 실행하여 인증한 다음 선택된 이미지 이름을 사용하여 스크립트를 실행하십시오.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  example.c 파일의 일부가 Docker 이미지 빌드 프로세스의 일부로 컴파일되므로 시스템에서 C 컴파일이 필요하지 않습니다.

4. 제공된 JavaScript 파일이 아니라 Docker 이미지에서 조치를 작성하려면 `--docker`를 추가하고 JavaScript 파일 이름을 Docker 이미지 이름으로 대체하십시오.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


[참조](./openwhisk_reference.html#openwhisk_ref_docker) 절에서 Docker 조치 작성에 대한 자세한 정보를 찾을 수 있습니다.


## 조치 출력 감시
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}} 조치는 다양한 이벤트에 대한 응답으로 또는 조치 시퀀스의 일부로 기타 사용자에 의해 호출될 수 있습니다. 그런 경우, 호출을 모니터하는 것이 유용합니다.

{{site.data.keyword.openwhisk_short}} CLI를 사용하여 조치가 호출될 때 조치의 출력을 감시할 수 있습니다.

1. 쉘에서 다음 명령 실행:
  ```
  wsk activation poll
  ```
  {: pre}

  이 명령은 활성화부터 계속해서 로그를 검사하는 폴링 루프를 시작합니다.

2. 다른 창으로 전환하여 조치 호출:

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```
  {: screen}

3. 폴링 창에서 활성화 로그 관찰:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  이와 유사하게 폴링 유틸리티를 실행할 때 {{site.data.keyword.openwhisk_short}}에서 사용자를 위해 실행 중인 모든 조치에 대한 실시간 로그를 볼 수 있습니다.

## 조치 삭제
{: #openwhisk_delete_action}

사용하지 않는 조치를 삭제하여 정리할 수 있습니다.

1. 다음 명령을 실행하여 조치 삭제:
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```
  {: screen}

2. 조치가 더 이상 조치 목록에 표시되지 않는지 확인하십시오.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
