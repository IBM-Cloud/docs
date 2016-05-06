---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Umgebungsvariablen
{: #environment_variables}

*Letzte Aktualisierung: 23. März 2016*

Von Liberty for Java unterstützte Umgebungsvariablen

<table>
<tr>
<th align="left">Name</th>
<th align="left">Beschreibung</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Zum Aktivieren von [App-Management-Dienstprogrammen](../../manageapps/app_mng.html).</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Zum Installieren von [App-Management-Dienstprogrammen](../../manageapps/app_mng.html).</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Zum Aktivieren von [Liberty-Beta-Features/](usingBetaFeatures.html).</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Zum Festlegen von [Java-Optionen](customizingJRE.html).</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAGENT</td>
<td>Zum Konfigurieren der [Informationen zur Position des Dynatrace-Agenten](dynatrace.html#configuring_liberty_app).</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Zum Konfigurieren der [IBM JRE-Version](customizingJRE.html).</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Zum Konfigurieren verschiedener Liberty-Laufzeitoptionen, wie z. B. [Features für WAR- oder EAR-Dateien](optionsForPushing.html#stand_alone_apps).</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Zum Konfigurieren der [OpenJDK-Version](customizingJRE.html)</td>.
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Zum Inaktivieren der automatischen Neukonfiguration durch das Framework Spring. Zum Inaktivieren legen Sie den Wert auf 'enabled: false' fest. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Zum Festlegen der Protokollierungsebene des Buildpacks. Mögliche Werte: <b>DEBUG</b>, <b>INFO</b> (Standardwert), <b>WARN</b>, <b>ERROR</b> oder <b>FATAL</b>.</td>
</tr>

<tr>
<td>JVM</td>
<td>Zum Auswählen des [JRE-Typs](customizingJRE.html).</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Zum Festlegen der [JVM-Argumente](customizingJRE.html).</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Zum Festlegen der Proxy-Server-Informationen.</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Zum Festlegen der Proxy-Server-Informationen.</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Zum Inaktivieren des Service [auto-configuration](autoConfig.html#opting_out).</td>
</tr>
</table>

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
