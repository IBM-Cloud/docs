---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 베타 기능 사용
{: #using_beta_features}

*마지막 업데이트 날짜: 2016년 3월 23일*

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
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

Bluemix에서 Liberty 베타 기능을 사용하려면 다음을 수행해야 합니다.

1. 다음 예에서와 같이 server.xml 파일에서 활성화된 하나 이상의 베타 기능을 사용하여 [서버 디렉토리 또는 패키지된 서버를 배치하십시오](optionsForPushing.html).
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  IBM_LIBERTY_BETA 환경 변수를 **true**로 설정하십시오. 이 변수는 애플리케이션의 베타 기능을 설치하고 활성화하도록 Liberty 빌드팩에 지시합니다. 다음 예를 참조하십시오. 
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
{: #codeblock}

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
