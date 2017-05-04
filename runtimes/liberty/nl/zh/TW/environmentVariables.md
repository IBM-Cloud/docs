---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 環境變數
{: #environment_variables}

Liberty for Java 支援的環境變數。

<table>
<tr>
<th align="left">名稱</th>
<th align="left">說明</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>啟用[應用程式管理公用程式](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>安裝[應用程式管理公用程式](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>啟用 [Liberty 測試版特性](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>設定 [Java 選項](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>配置 [Dynatrace 代理程式位置資訊](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>配置 [IBM JRE 版本](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>配置各種 Liberty 運行環境選項，包括 [WAR 檔或 EAR 檔的特性](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>配置 [OpenJDK 版本](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>停用 Spring Auto-Reconfiguration 架構。若要停用，請將值設為 enabled: false。</td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>設定建置套件的記載層次。可能值：<b>DEBUG</b>、<b>INFO</b>（預設值）、<b>WARN</b>、<b>ERROR</b> 或 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>選取 [JRE 類型](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>設定 [JVM 引數](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[置換服務配置](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>設定 Proxy 伺服器資訊</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>設定 Proxy 伺服器資訊</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>停用服務[自動配置](autoConfig.html#opting_out)。</td>
</tr>
</table>

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty 運行環境](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
