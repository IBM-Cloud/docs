---

copyright:
 years: 2015, 2016

---

# Participando de notificações para
Android
{: #hold-notifications-android}
*Última atualização: 14 de junho de 2016*
{: .last-updated}

Quando seu aplicativo entra em segundo plano, é possível que queira que o serviço de Notificação push retenha as notificações enviadas ao seu aplicativo. Para reter notificações, chame o método
hold() no método onPause() da atividade que está manipulando as notificações push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
