---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato de log do Kibana para Hub de Mensagens
{: #kibana_log_format_messagehub}

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
