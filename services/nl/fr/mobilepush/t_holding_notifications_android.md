---

Copyright :
  Années : 2015, 2016

---

# Conservation des notifications pour Android
{: #hold-notifications-android}

Lorsque votre application passe en arrière-plan, il peut être judicieux que Push conserve les notifications qui lui sont envoyées. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les notifications push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
