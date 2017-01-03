---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Participando de notificações para
Android
{: #hold-notifications-android}
Última atualização: 06 de dezembro de 2016
{: .last-updated}

Quando seu aplicativo entra em segundo plano, é possível que você queira que o serviço {{site.data.keyword.mobilepushshort}} retenha as notificações enviadas para seu aplicativo. Para reter notificações, chame o método hold() no método onPause() da atividade que está manipulando o {{site.data.keyword.mobilepushshort}}.

```
	@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	} 
```
	{: codeblock}
