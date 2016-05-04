---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 환경 변수 
{: #environment_variables}

*마지막 업데이트 날짜: 2016년 3월 23일*

Java용 Liberty에서 지원하는 환경 변수

<table>
<tr>
<th align="left">이름</th>
<th align="left">설명</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>[앱 관리 유틸리티](../../manageapps/app_mng.html)를 사용으로 설정합니다. </td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>[앱 관리 유틸리티](../../manageapps/app_mng.html)를 설치합니다. </td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>[Liberty 베타 기능](usingBetaFeatures.html)을 사용으로 설정합니다. </td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>[Java 옵션](customizingJRE.html)을 설정합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAGENT</td>
<td>[Dynatrace 에이전트 위치 정보](dynatrace.html#configuring_liberty_app)를 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>[IBM JRE 버전](customizingJRE.html)을 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>[WAR 또는 EAR 파일의 기능](optionsForPushing.html#stand_alone_apps)을 포함하여 다양한 Liberty 런타임 옵션을 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>[OpenJDK 버전](customizingJRE.html)을 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Spring Auto-Reconfiguration 프레임워크를 사용하지 않습니다. 사용 안함으로 설정하려면 값을 enabled: false로 설정하십시오. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>빌드팩의 로깅 레벨을 설정합니다. 가능한 값: <b>DEBUG</b>, <b>INFO</b> (default), <b>WARN</b>, <b>ERROR</b> 또는 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>[JRE 유형](customizingJRE.html)을 선택합니다. </td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>[JVM 인수](customizingJRE.html)를 설정합니다. </td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>프록시 서버 정보를 설정합니다.</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>프록시 서버 정보를 설정합니다.</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>[auto-configuration](autoConfig.html#opting_out) 서비스를 사용 안함으로 설정합니다. </td>
</tr>
</table>

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
