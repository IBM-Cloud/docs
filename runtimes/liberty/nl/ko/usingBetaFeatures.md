---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 베타 기능 사용
{: #using_beta_features}

Liberty 베타 기능은 향후 Liberty 릴리스에 포함될 수 있는 새로운 기능과 프로그래밍 모델을 미리 사용해 볼 수 있도록 합니다. Bluemix에 배치된 애플리케이션에서도 대부분의 베타 기능을 사용할 수 있습니다. 

**중요**: 베타 기능은 개발과 테스트 용도로만 제공되며 운영 환경에서는 사용할 수 없습니다. 이용 약관 전문을 보려면 [베타 라이센스 계약](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)을 참조하십시오.

Bluemix에서 사용 가능한 Liberty 베타 기능
<table>
<tr>
<th align="left">기능</th>
<th align="left">기능</th>
<th align="left">기능</th>
<th align="left">기능</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
<td>osgiBundle-1.0</td>
</tr>
</table>

Bluemix에서 Liberty 베타 기능을 사용하려면 다음을 수행해야 합니다.

1. 다음 예에서와 같이 server.xml 파일에서 활성화된 하나 이상의 베타 기능을 사용하여 [서버 디렉토리 또는 패키지된 서버를 배치하십시오](optionsForPushing.html).

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>bluemixLogCollector-1.1</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  **IBM_LIBERTY_BETA** 환경 변수를 **true**로 설정하십시오. 이 변수는 애플리케이션의 베타 기능을 설치하고 활성화하도록 Liberty 빌드팩에 지시합니다. 예: 
  * cf 명령행 도구 사용:

```
$ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * 또는 manifest.yml 파일 사용:

```
env:
          IBM_LIBERTY_BETA: "true"
```

3. **JBP_CONFIG_LIBERTY** 환경 변수를 **"version: +"**로 설정하십시오. 이 변수는 베타 기능을 지원하는 [Liberty 월별 런타임](buildpackDefaults.html#liberty_versions)을 사용으로 설정합니다. 예: 
  * cf 명령행 도구 사용:

```
$ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * 또는 manifest.yml 파일 사용:

```
env:
          JBP_CONFIG_LIBERTY: "version: +"
```

기존 애플리케이션에서 베타 기능을 사용으로 설정하는 경우에는 환경 변수를 설정한 후에 애플리케이션을 다시 스테이징할 것을 기억하십시오.

{: #codeblock}

# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
