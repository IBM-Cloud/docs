---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 环境变量
{: #environment_variables}

Liberty for Java 支持的环境变量。

<table>
<tr>
<th align="left">名称</th>
<th align="left">描述</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>启用[应用程序管理实用程序](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>安装[应用程序管理实用程序](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>启用 [Liberty Beta 功能](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>设置 [Java 选项](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>配置 [Dynatrace 代理程序位置信息](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>配置 [IBM JRE 版本](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>配置各种 Liberty 运行时选项，包括[用于 WAR 或 EAR 文件的功能](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>配置 [OpenJDK 版本](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION</td>
<td>禁用 Spring 自动重新配置框架。要禁用，请将值设置为 enabled: false。</td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>设置 buildpack 的日志记录级别。可能的值：<b>DEBUG</b>、<b>INFO</b>（缺省值）、<b>WARN</b>、<b>ERROR</b> 或 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>选择 [JRE 类型](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>设置 [JVM 自变量](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[覆盖服务配置](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>设置代理服务器信息</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>设置代理服务器信息</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>禁用服务[自动配置](autoConfig.html#opting_out)。</td>
</tr>
</table>

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
