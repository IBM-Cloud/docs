---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Environment variables
{: #environment_variables}

Environment variables supported by Liberty for Java.

<table>
<tr>
<th align="left">Name</th>
<th align="left">Description</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Enable [App Management utilities](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Install [App Management utilities](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Enable [Liberty beta features/](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Set [Java options](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configure the [Dynatrace agent location information](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configure the [IBM JRE version](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configure a variety of Liberty runtime options including [features for WAR or EAR files](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configure the [OpenJDK version](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Disable the Spring Auto-Reconfiguration framework. To disable, set value to enabled: false. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Set logging level of the buildpack. Possible values: <b>DEBUG</b>, <b>INFO</b> (default), <b>WARN</b>, <b>ERROR</b>, or <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Select the [JRE type](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Set the [JVM arguments](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Override service configuration](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Set proxy server information</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Set proxy server information</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Disable service [auto-configuration.](autoConfig.html#opting_out)</td>
</tr>
</table>

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
