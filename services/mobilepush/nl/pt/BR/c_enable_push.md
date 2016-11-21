---

copyright:
 years: 2015, 2016

---

# Ativando notificações push
{: #c_enable_push-notifications}
Última atualização: 17 de outubro de 2016
{: .last-updated}

É possível ativar aplicativos para receber notificações push para os seus dispositivos.

Esta seção descreve como ativar os seus aplicativos clientes - aplicativos móveis e de navegador da web, bem como os Apps Chrome e Extensões para receber notificações push, como criar
notificações de configuração básica, obter e inicializar o SDK ou o plug-in e como registrar o seu dispositivo ou navegador para receber notificações push. Também é possível
ativar seus aplicativos móveis e de navegador da web para receber notificações push usando
a [API REST](t_restapi.html).

Nota: para registros de dispositivo, navegador, Apps Chrome e Extensões, o serviço {{site.data.keyword.mobilepushshort}} mantém uma referência
exclusiva para tokens emitidos a partir de provedores de notificação - APNs para Apple ou GCM para Google. Os tokens podem ser invalidados pelo provedor de notificação de serviço {{site.data.keyword.mobilepushshort}} por vários motivos. 

Por exemplo, durante a desinstalação de um app no dispositivo. Nesse cenário, quando a entrega de uma notificação for tentada com base na resposta dos provedores de que o dispositivo está invalidado, o serviço {{site.data.keyword.mobilepushshort}} removerá os registros do dispositivo ou do navegador da web. Isso,
por sua vez, restringiria tentativas subsequentes de enviar a notificação a esses dispositivos invalidados.
