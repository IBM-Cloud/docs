---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variabili di ambiente
{: #environment_variables}

Variabili di ambiente supportate da Liberty for Java.

<table>
<tr>
<th align="left">Nome</th>
<th align="left">Descrizione</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Abilita i [programmi di utilità di Gestione applicazioni](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Installa i [programmi di utilità di Gestione applicazioni](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Abilita le [funzioni beta Liberty/](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Configura le [opzioni Java](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configura le [informazioni di ubicazione dell'agent Dynatrace](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configura la [versione IBM JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configura varie opzioni di runtime Liberty incluse le [funzioni per i file WAR o EAR](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configura la [versione di OpenJDK](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Disabilita lo Spring Auto-Reconfiguration Framework. Per disabilitare, imposta il valore su enabled: false. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Imposta il livello di registrazione del pacchetto di build. Valori possibili: <b>DEBUG</b>, <b>INFO</b> (predefinito), <b>WARN</b>, <b>ERROR</b> o <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Selezione il [tipo JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Imposta gli [argomenti JVM](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Sovrascrivi congiurazione del servizio](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Imposta le informazioni del server proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Imposta le informazioni del server proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Disabilita il servizio di [configurazione automatica.](autoConfig.html#opting_out)</td>
</tr>
</table>

# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
