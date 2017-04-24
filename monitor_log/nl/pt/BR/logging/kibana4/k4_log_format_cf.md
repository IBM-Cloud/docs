---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de log do Kibana para aplicativos Cloud Foundry
{: #kibana_log_format_cf}

É possível configurar o Kibana para exibição, na página *Descobrir*, dos seguintes campos para cada entrada de log:
{:shortdesc}

| Campo | Descrição |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> O horário do evento registrado. <br> O registro de data e hora é definido até o milissegundo. |
| @version | Versão do evento. |
| ALCH_TENANT_ID | ID do espaço do {{site.data.keyword.Bluemix_notm}}. |
| \_id | O ID exclusivo para seu documento de log. |
| \_index | O índice para sua entrada de log. |
| \_type | O tipo de log; por exemplo, *syslog*. |
| app_name | O nome de seu aplicativo {{site.data.keyword.Bluemix_notm}}. |
| application_id | O ID exclusivo de seu aplicativo {{site.data.keyword.Bluemix_notm}}. |
| host | O nome de seu aplicativo que produziu os dados do log. |
| instance_id | O ID da instância de sua instância do aplicativo que produziu os dados do log. |
| nível de log | A severidade do evento registrado. |
| mensagem | A mensagem que é emitida pelo componente. <br> A mensagem varia, dependendo do contexto. |
| message_type | O fluxo para o qual a mensagem de log é gravada. <br> * **OUT** refere-se ao fluxo stdout<br> * **ERR** refere-se ao fluxo stderr. |
| org_id | O ID exclusivo de sua organização do {{site.data.keyword.Bluemix_notm}} |
| org_name | O nome da organização do {{site.data.keyword.Bluemix_notm}} na qual seu app está montado. |
| origem | Componente de onde o evento foi originado. |
| source_id | O componente que produz logs. <br> A lista a seguir descreve os logs de cada componente: <br> * **API**: respostas registradas em chamadas API que solicitam uma mudança no estado do app.<br> * **APP**: respostas registradas do seu app. <br> * **CELL**: respostas registradas da célula Diego que indicam quando um aplicativo é iniciado, interrompido ou travado<br> * **LGR**: respostas registradas do loggregator que indicam problemas com o processo de criação de log.<br> * **RTR**: respostas registradas do Roteador quando ele roteia solicitações de HTTP para seu app. <br> * **SSH**: respostas registradas da célula Diego quando um usuário acessa um contêiner de app usando o comando `cf ssh`. <br> * **STG**: respostas registradas da célula Diego ou do Droplet Execution Agent quando seu app é montado ou remontado.  |
| space_name | O nome do espaço do {{site.data.keyword.Bluemix_notm}} no qual seu app é montado. |
| time stamp | O horário do evento registrado. O registro de data e hora é definido até o milissegundo. |




