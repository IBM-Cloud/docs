---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Node.js 빌드팩

Bluemix는 여러 버전의 Node.js 빌드팩을 제공합니다.
{: shortdesc}
* IBM 작성 **sdk-for-nodejs** 빌드팩은 Bluemix의 Node.js 애플리케이션에 사용되는 기본 빌드팩입니다. 
* **nodejs_buildpack**은 Cloud Foundry 커뮤니티에서 제공하는 커뮤니티 빌드팩입니다. 

**sdk-for-nodejs** 빌드팩은 Bluemix의 **nodejs_buildpack**에 우선합니다. 애플리케이션에 **sdk-for-nodejs** 대신 **nodejs_buildpack**을 사용하려면 사용자 빌드팩을 지정해야 합니다. 예를 들어 **cf push** 명령에서 -b 옵션을 사용하여 지정하십시오. 

일반적으로 현재 **sdk-for-nodejs** 빌드팩과 이전 레벨 버전이 사용 가능합니다. 사용 가능한 모든 빌드팩을 보려면 **cf buildpacks** 명령을 사용하십시오. 예: 

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
