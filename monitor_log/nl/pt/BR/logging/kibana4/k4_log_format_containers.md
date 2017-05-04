---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de log do Kibana para contêineres do Docker
{: #kibana_log_format_containers}

É possível configurar o Kibana para exibição, na página *Descobrir*, dos seguintes campos
para cada entrada de log:
{:shortdesc}

| Campo | Descrição |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> O horário do evento registrado. <br> O registro de data e hora é definido até o milissegundo. |
| @version | Versão do evento. |
| ALCH_TENANT_ID | ID do espaço do {{site.data.keyword.Bluemix_notm}}. |
| \_id | O ID exclusivo para seu documento de log. |
| \_index | O índice para sua entrada de log. |
| \_type | O tipo de log; por exemplo, *logs*. |
| group_id | ID do Grupo <br> * Para um contêiner único, o valor é
**0000**.<br> * Para um grupo de contêiner, o valor é o GUID do grupo.  |
| host | O nome do host no qual o contêiner é executado. |
| instância | GUID da instância para um contêiner único. Lista de IDs de instâncias para um grupo de
contêiner. |
| Posição do Log | Mensagem curta. |
|  | Mensagem integral. |
| path | Caminho e nome de log no qual o log está localizado dentro do contêiner. |
| fluxo | Especifica o tipo de log: stdout, stderr |
| tempo | A data e a hora de quando o evento ocorreu. O registro de data e hora é definido até o milissegundo.|
| time stamp | A data e a hora do evento registrado. O registro de data e hora é definido até o milissegundo. |



