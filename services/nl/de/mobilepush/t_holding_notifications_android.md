---

copyright:
 years: 2015, 2016

---

# Benachrichtigungen für Android blockieren
{: #hold-notifications-android}
*Letzte Aktualisierung: 14. Juni 2016*
{: .last-updated}

Wenn Ihre Anwendung in den Hintergrund wechselt, möchten Sie möglicherweise, dass der Push Notification-Service die Benachrichtigungen aufbewahrt, die an Ihre Anwendung gesendet werden. Zum Blockieren von Benachrichtigungen rufen Sie die Methode 'hold()' in der Methode 'onPause()' der Aktivität auf, die Push-Benachrichtigungen verarbeitet.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
