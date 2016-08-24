---

copyright:
 years: 2015, 2016

---

# Ativando Notificações
{: #c_enable_push-notifications}
*Última atualização: 14 de junho de 2016*
{: .last-updated}

É possível ativar aplicativos para receber e enviar notificações push a seus dispositivos.

Esta seção descreve como ativar seus aplicativos móveis para receber notificações push, como criar notificações básicas, obter e
inicializar o SDK ou plug-in e como registrar seu dispositivo para receber notificações push. Também é possível ativar seus aplicativos móveis para receber
notificações push usando a [REST API](t_restapi.html).

Nota: para registros de dispositivo com push, o serviço de Notificação push mantém uma referência exclusiva a tokens emitidos dos provedores
de notificação - APNS para Apple ou GCM para Google. Os tokens podem ser invalidados pelo provedor de notificação do serviço de Notificação push
por vários motivos. 

Por exemplo, durante a desinstalação do aplicativo no dispositivo. Em tal cenário, quando se tenta entregar uma notificação com base na resposta dos provedores de que o dispositivo está invalidado, o serviço de Notificação push removerá os registros do dispositivo. Isso,
por sua vez, restringiria tentativas subsequentes de enviar a notificação a esses dispositivos invalidados.
