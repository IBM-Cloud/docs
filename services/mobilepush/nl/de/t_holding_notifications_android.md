---

copyright:
 years: 2015, 2016

---

# Benachrichtigungen für Android blockieren
{: #hold-notifications-android}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Wenn Ihre Anwendung in den Hintergrund wechselt, ist es gegebenenfalls wünschenswert, dass der {{site.data.keyword.mobilepushshort}}-Service die Benachrichtigungen aufbewahrt, die an Ihre Anwendung gesendet werden. Rufen Sie zum Blockieren von Benachrichtigungen die Methode 'hold()' in der Methode 'onPause()' der Aktivität auf, die Push-Benachrichtigungen verarbeitet. 

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
