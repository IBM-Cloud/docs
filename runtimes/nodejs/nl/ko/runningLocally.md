---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 로컬에서 Node.js 애플리케이션 실행을 위한 힌트
{: #hints}

로컬과 Bluemix 모두에서 Node.js 애플리케이션 실행을 용이하게 하려면 이 정보를 사용하십시오.
{: shortdesc}

다음 예에서는 **js** 파일의 소스 파트를 보여줍니다. 
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

애플리케이션이 Bluemix에서 실행 중인 경우 이 코드를 사용하여 PORT 환경 변수에 Bluemix 내부에서 사용되고 앱이 수신 연결을 청취하는 포트 값을 포함합니다. 애플리케이션이 로컬로 실행 중인 경우에는 PORT가 정의되지 않으므로 **3000**을 포트 번호로 사용합니다. 이런 방식으로 작성하면 애플리케이션을 테스트 목적으로 로컬에서 실행하고 Bluemix에서는 추가 변경 없이 실행할 수 있습니다. 
