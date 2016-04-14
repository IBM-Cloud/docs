---

copyright:
 years: 2015, 2016

---

# Benachrichtigungen für Android blockieren
{: #hold-notifications-android}

Wenn Ihre Anwendung in den Hintergrund wechselt, möchten Sie möglicherweise, dass Push Benachrichtigungen blockiert, die an Ihre Anwendung gesendet werden. Zum Blockieren von Benachrichtigungen rufen Sie die Methode 'hold()' in der Methode 'onPause()' der Aktivität auf, die Push-Benachrichtigungen verarbeitet.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
