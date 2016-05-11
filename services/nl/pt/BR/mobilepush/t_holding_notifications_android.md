---

copyright:
 years: 2015, 2016

---

# Participando de notificações para
Android
{: #hold-notifications-android}

Quando seu aplicativo entrar no plano de fundo, você provavelmente desejará que Push
restrinja as notificações enviadas para ele. Para reter notificações, chame o método
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
