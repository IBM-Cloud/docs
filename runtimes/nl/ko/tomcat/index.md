---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*마지막 업데이트 날짜: 2016년 3월 19일*

{{site.data.keyword.Bluemix}}의 Tomcat 런타임은 java_buildpack을 통해 제공됩니다.
{: shortdesc}

{{site.data.keyword.Bluemix}}에서 Tomcat 런타임을 사용하려면 java_buildpack을 -b 옵션으로 지정해야 합니다. 예: 
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Tomcat 런타임에 대한 자세한 정보는
[java-buildpack readme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md)를 참조하십시오.

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Tomcat 스타터 애플리케이션을 제공합니다. Tomcat 스타터 애플리케이션은 사용할 수 있는 템플리트를 제공하는 단순한 Tomcat 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 Bluemix 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 런타임 버전
{: #runtime_versions}

JBP_CONFIG_TOMCAT 환경 변수를 사용하여 앱에서 사용할 Tomcat 버전을 변경할 수 있습니다.
JBP_CONFIG_OPEN_JDK_JRE 환경 변수를 사용하여 앱에서 사용할 Java 버전을 변경할 수 있습니다.
두 환경 변수 모두 애플리케이션의 Manifest 파일에서 지정할 수 있습니다. 예:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
현재 기본 Tomcat 버전은 8.0.30입니다. 현재 기본 Java 버전은 1.8.0_65입니다.
자세한 정보는 [java-buildpack 릴리스](https://github.com/cloudfoundry/java-buildpack/releases)를 참조하십시오.

# 관련 링크
## 일반
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
