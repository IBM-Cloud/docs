---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Formatos de log do Kibana
{: #kibana_formats}

É possível configurar o Kibana para ser exibido nos diferentes campos da página *Descobrir* para cada entrada de log.
{:shortdesc}



## Formato de log do Kibana para aplicativos Cloud Foundry
{: #kibana_log_format_cf}

É possível configurar o Kibana para exibição, na página *Descobrir*, dos seguintes campos para cada entrada de log:

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
| message_type | O fluxo para o qual a mensagem de log é gravada. <br> * **OUT** refere-se ao fluxo stdout <br> * **ERR** refere-se ao fluxo stderr. |
| org_id | O ID exclusivo de sua organização do {{site.data.keyword.Bluemix_notm}} |
| org_name | O nome da organização do {{site.data.keyword.Bluemix_notm}} na qual seu app está montado. |
| origem | Componente de onde o evento foi originado. |
| source_id | O componente que produz logs. <br> A lista a seguir descreve os logs de cada componente: <br> * **API**: respostas registradas em chamadas API que solicitam uma mudança no estado do app. <br> * **APP**: respostas registradas do seu app. <br> * **CELL**: respostas registradas da célula Diego que indicam quando um aplicativo é iniciado, interrompido ou travado <br> * **LGR**: respostas registradas do loggregator que indicam problemas com o processo de criação de log. <br> * **RTR**: respostas registradas do Roteador quando ele roteia solicitações de HTTP para seu app. <br> * **SSH**: respostas registradas da célula Diego quando um usuário acessa um contêiner de app usando o comando `cf ssh`. <br> * **STG**: respostas registradas da célula Diego ou do Droplet Execution Agent quando seu app é montado ou remontado. |
| space_name | O nome do espaço do {{site.data.keyword.Bluemix_notm}} no qual seu app é montado. |
| time stamp | O horário do evento registrado. O registro de data e hora é definido até o milissegundo. |
{: caption="Tabela 1. Campos para apps CF" caption-side="top"}



## Formato de log do Kibana para contêineres do Docker
{: #kibana_log_format_containers}

É possível configurar o Kibana para exibição, na página *Descobrir*, dos seguintes campos para cada entrada de log:

| Campo | Descrição |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> O horário do evento registrado. <br> O registro de data e hora é definido até o milissegundo. |
| @version | Versão do evento. |
| ALCH_TENANT_ID | ID do espaço do {{site.data.keyword.Bluemix_notm}}. |
| \_id | O ID exclusivo para seu documento de log. |
| \_index | O índice para sua entrada de log. |
| \_type | O tipo de log; por exemplo, *logs*. |
| group_id | ID do Grupo <br> * Para um contêiner único, o valor é
**0000**. <br> * Para um grupo de contêiner, o valor é o GUID do grupo.  |
| host | O nome do host no qual o contêiner é executado. |
| instância | GUID da instância para um contêiner único. Lista de IDs de instâncias para um grupo de
contêiner.|
| Posição do Log | Mensagem curta. |
| mensagem | Mensagem integral. |
| path | Caminho e nome de log no qual o log está localizado dentro do contêiner. |
| fluxo | Especifica o tipo de log: stdout, stderr |
| tempo | A data e a hora de quando o evento ocorreu. O registro de data e hora é definido até o milissegundo.|
| time stamp | A data e a hora do evento registrado. O registro de data e hora é definido até o milissegundo. |
{: caption="Tabela 1. Campos para contêineres do Docker" caption-side="top"}


## Formato de log do Kibana para Hub de Mensagens
{: #kibana_log_format_messagehub}

É possível configurar o Kibana para exibição, na página *Descobrir*, dos seguintes campos para cada entrada de log:

| Campo | Descrição |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> O horário do evento registrado. <br> O registro de data e hora é definido até o milissegundo. |
| @version | Versão do evento. |
| ALCH_TENANT_ID | ID do espaço do {{site.data.keyword.Bluemix_notm}}. |
| \_id | O ID exclusivo para seu documento de log. |
| \_index | O índice para sua entrada de log. |
| \_type | O tipo de log; por exemplo, *syslog*. |
| nível de log | A severidade do evento registrado, por exemplo, **Informações**. |
| Módulo | Esse campo é configurado como **MessageHub**. |
{: caption="Tabela 1. Campos para eventos de Hub de mensagens" caption-side="top"}

Exemplo de uma entrada de log:

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
