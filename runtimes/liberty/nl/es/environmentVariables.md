---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variables de entorno
{: #environment_variables}

Variables de entorno admitidas por Liberty para Java.

<table>
<tr>
<th align="left">Nombre</th>
<th align="left">Descripción</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Habilitar [Utilidades de App Management](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Instalar [Utilidades de App Management](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Habilitar [funciones beta de Liberty/](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Establecer [Opciones de Java](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configurar la [información sobre ubicación del agente de Dynatrace](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configurar la [versión de IBM JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configurar una variedad de opciones de tiempo de ejecución de Liberty incluidas las [características para archivos WAR o EAR](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configurar la [versión de OpenJDK](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Inhabilitar la infraestructura Spring Auto-Reconfiguration. Para inhabilitarla, establezca el valor en enabled: false. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Establecer nivel de registro del paquete de compilación. Valores posibles: <b>DEBUG</b>, <b>INFO</b> (valor predeterminado), <b>WARN</b>, <b>ERROR</b>, o <b>MUY GRAVE</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Seleccionar el [Tipo de JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Establecer los [argumentos de JVM](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Sustituir configuración de servicio](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Establecer la información del servidor proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Establecer la información del servidor proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Inhabilitar el servicio de [autoconfiguración.](autoConfig.html#opting_out)</td>
</tr>
</table>

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
