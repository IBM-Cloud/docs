---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variáveis de ambiente
{: #environment_variables}

Variáveis de ambiente suportadas pelo Liberty for Java.

<table>
<tr>
<th align="left">Nome</th>
<th align="left">Descrição</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Ative os [utilitários de gerenciamento de app](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Instale os [utilitários de gerenciamento de app](/docs/manageapps/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Ative os [recursos beta do Liberty](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Configure as [opções Java](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configure as [informações de local do agente Dynatrace](dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configure a [versão do IBM JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configure uma variedade de opções de tempo de execução do Liberty incluindo [recursos para arquivos WAR ou EAR](optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configure a [versão do OpenJDK](customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Desative a estrutura de Reconfiguração automática Spring. Para desativar, configure o valor para ativado: falso. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Configure o nível de criação de log do buildpack. Valores possíveis: <b>DEBUG</b>, <b>INFO</b> (padrão), <b>WARN</b>, <b>ERROR</b> ou <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Selecione o [tipo de JRE](customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Configure os [argumentos da JVM](customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Substituir a configuração de serviço](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Configure informações do servidor proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Configure informações do servidor proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Desative a [configuração automática](autoConfig.html#opting_out) do serviço.</td>
</tr>
</table>

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
