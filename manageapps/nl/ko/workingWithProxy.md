---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 프록시 작업
{: #working_with_proxy}



[Bluemix 데디케이티드](/docs/dedicated/index.html#dedicated),
[Bluemix 로컬](/docs/local/index.html#local)과 같은 일부 환경에서 스테이징과 런타임 중에
애플리케이션의 동작에 영향을 미치는 프록시를 구성할 수 있습니다. 

다음 환경 변수를 사용하여 프록시 관련 작업을 수행하도록 애플리케이션을 구성할 수 있습니다. 
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

*cf se*를 사용하거나 *manifest.yml* 파일을 통해 이와 같은 환경 변수를 설정할 수 있습니다. 애플리케이션에서 스테이징
환경 변수와 프록시 환경 변수를 설정하는 동안 인터넷에서 리소스를 다운로드해야 하는 경우에는
프록시 환경 변수가 구성된 방법에 따라 구성된 프록시를 통해 리소스가 다운로드됩니다. 

예를 들어, nodejs 애플리케이션이 있고 *http_proxy*가 *yourProxyURL*로 설정된 환경에서
실행 중이라고 가정합니다. 또한 npm이 인터넷에서 노드 모듈을 다운로드하도록 허용한다고 가정합니다. 이를 달성하기 위해
*no_proxy*를 *npmjs.org*로 설정할 수 있습니다. 

**참고**: 애플리케이션에서 런타임 동안 프록시를 이용할 수 있습니다. 이는 전적으로 애플리케이션에
따라 다르며 빌드팩과 이들 세 환경 변수의 영향을 받지 않습니다. 

## Java 애플리케이션
{: #java_apps}

[Liberty for Java](/docs/runtimes/liberty/index.html) 애플리케이션과 [java_buildpack](/docs/runtimes/tomcat/index.html) 애플리케이션의 경우 **JAVA_OPTS** 환경 변수를 통해 프록시 설정을 런타임에 전달할 수 있습니다. 예를 들어, 다음 명령을 실행할 수 있습니다. 
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

그런 다음 애플리케이션을 다시 스테이징하십시오. 그러면 애플리케이션에서 런타임 시 지정된 프록시 설정을 사용합니다. Java 프록시 옵션에 대한 자세한 정보는 [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html)의 내용을 참조하십시오. 

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
