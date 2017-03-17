---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando webhooks 
{: #tag_based_notifications}
Última atualização: 23 de janeiro de 2017
{: .last-updated}


Com o serviço {{site.data.keyword.mobilepushshort}}, é possível optar por receber alertas
sobre informações que foram mudadas. As mudanças nas informações corporativas criam eventos, para os quais é
possível ser notificado registrando-os como eventos webhook. Esses eventos webhook acionam um alerta. 

Webhooks são retornos de chamada definidos pelo usuário que são acionados por um evento, como
registrar-se em um dispositivo ou inscrever-se nas tags. No serviço {{site.data.keyword.mobilepushshort}},
é possível registrar-se para os eventos webhook a seguir: 

- **onDeviceRegister**: um evento webhook é acionado para dispositivos registrados
para push.
- **onDeviceUpdate**: um evento webhook é acionado quando informações sobre um
dispositivo registrado são atualizadas.
- **onDeviceUnregister**: um evento webhook é acionado quando um
dispositivo tem o registro cancelado. 
- **onSubscribe**: um evento webhook é acionado quando um usuário se inscreve em
uma tag.
- **onUnsubscribe**: um evento webhook é acionado quando um usuário remove a
assinatura de uma tag.
- **onNotificationSend**: um evento webhook é acionado para uma notificação que foi
despachada.
- **onNotificationFailure**: um evento webhook é acionado para falhas de notificação.


**Nota**: a notificação é despachada em lotes. Um despacho de mensagem pode ter
múltiplos eventos webhooks, que podem incluir falhas e sucesso. 
Os eventos webhook têm o mesmo messageID que a mensagem despachada. 

Para obter mais informações sobre webhooks, veja a [API de REST de notificações push da IBM ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}.
