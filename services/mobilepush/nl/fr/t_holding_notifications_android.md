---

copyright:
 years: 2015, 2016

---

# Conservation des notifications pour Android
{: #hold-notifications-android}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Quand votre application passe en arrière-plan, vous pouvez vouloir que le service {{site.data.keyword.mobilepushshort}} conserve les notifications qui sont envoyées à cette application. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les
notifications de type {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
