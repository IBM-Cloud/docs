---

copyright:
  years: 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Oracle JRE 사용
{: #using_oraacle_jre}

선택한 경우 Oracle JRE로 Bluemix에서 Liberty 애플리케이션을 실행할 수 있습니다. 해당 작업을 수행하려면 다음을 수행해야 합니다.
* 빌드팩이 다운로드할 수 있는 소스 위치에서 JRE를 호스트합니다.
* 호스트 JRE의 위치를 제공하는 `index.yml` 파일을 호스팅합니다.
* 해당 JRE를 사용하도록 사용자의 애플리케이션을 구성합니다.

## JRE 및 index.yml 호스트
{: #hosting_jre}

Oracle JRE 파일은 웹 서버에서 호스트되어야 하며, Liberty 빌드팩이 해당 서버에서 이를 다운로드할 수 있어야 합니다. 사용 가능한 서버 기능을 사용하여 Bluemix 자체에서 이 파일을 호스트하거나, 일부 공용 사용 가능 위치에서 호스트할 수 있습니다. 서버는 JRE 파일에 대한 세부사항을 지정하는 `index.yml` 파일로 구성되어야 합니다. 다음 단계를 완료하여 JRE 및 `index.yml` 파일을 호스팅하십시오.
  1. Oracle JRE를 가져오십시오. JRE는 Unix 64비트 OS용 버전이고 `tar.gz` 파일이어야 합니다.
  2. Liberty 빌드팩이 다운로드할 수 있는 소스 위치에서 JRE 파일을 호스트하십시오. 
  3. 호스팅 위치에 `index.yml` 파일을 제공하는지 확인하십시오. `index.yml` 파일에는 Oracle JRE의 버전 ID(뒤에 콜론이 붙음)와 해당 JRE 파일 위치의 완전한 URL로 구성된 항목이 포함되어야 합니다. `index.yml`의 형식은 다음과 같습니다.
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * 예:
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## 앱 구성
{: #configure_app}

두 개의 환경 변수가 Liberty 애플리케이션에 설정되어야 합니다. *JBP_CONFIG_OPENJDK*가 `index.yml` 파일의 위치를 지정하도록 설정되고, *JVM* 환경 변수가 *openjdk*로 설정되어야 대체 JRE를 사용하도록 빌드팩을 구성할 수 있습니다.

JBP_CONFIG_OPENJDK 변수의 경우 값은 다음과 같습니다.
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

이를 설정하기 위해 다음과 같은 명령을 실행할 수 있습니다.
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

참고로, *repository_root* URL은 `index.yml`을 포함하지 않지만 해당 위치 바로 이전에 중지됩니다.

JVM 환경 변수를 설정하려면 다음과 같은 명령을 실행합니다.
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**참고**: 환경 변수를 설정한 후 애플리케이션을 다시 스테이징해야 합니다.

## 확인
{: #confirmation}

예상되는 JRE를 사용 중인지 확인하려면 스테이징 로그에서 다음과 유사한 메시지를 확인하십시오.
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
