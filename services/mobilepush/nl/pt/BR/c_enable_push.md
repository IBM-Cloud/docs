---

copyright:
 years: 2015, 2016

---

# Ativando Notificações
{: #c_enable_push-notifications}
Última atualização: 16 de agosto de 2016
{: .last-updated}

É possível ativar aplicativos para receber e enviar notificações push a seus dispositivos.

Esta seção descreve como ativar seus aplicativos móveis para receber notificações push, como criar notificações básicas, obter e
inicializar o SDK ou plug-in e como registrar seu dispositivo para receber notificações push. Também é possível ativar seus aplicativos móveis para receber
notificações push usando a [REST API](t_restapi.html).

Nota: para registros de dispositivo com push, o serviço {{site.data.keyword.mobilepushshort}} mantém uma referência exclusiva a tokens emitidos de provedores de notificação -
APNs para Apple ou GCM para Google. Os tokens podem ser invalidados pelo provedor de notificação de serviço {{site.data.keyword.mobilepushshort}} por vários motivos. 

Por exemplo, durante a desinstalação de um app no dispositivo. Neste cenário, quando houver a tentativa de entregar uma notificação com base na resposta dos provedores de que o dispositivo está invalidado, o serviço {{site.data.keyword.mobilepushshort}} removerá os registros do dispositivo. Isso,
por sua vez, restringiria tentativas subsequentes de enviar a notificação a esses dispositivos invalidados.
