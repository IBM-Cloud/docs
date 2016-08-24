---

copyright:
 years: 2015, 2016

---

# Conservation des notifications pour Android
{: #hold-notifications-android}
*Dernière mise à jour : 14 juin 2016*
{: .last-updated}

Quand votre application passe en arrière-plan, vous pouvez vouloir que le service Notifications Push conserve les notifications qui sont envoyées à cette application. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les notifications push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
