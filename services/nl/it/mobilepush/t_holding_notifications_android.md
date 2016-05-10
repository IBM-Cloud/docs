---

copyright:
 years: 2015, 2016

---

# Notifiche messe in pausa per Android
{: #hold-notifications-android}

Quando la tua applicazione va in background, probabilmente vuoi che Push metta in pausa le notifiche inviate alla
                            tua applicazione. Per mettere in pausa le notifiche, richiama il metodo hold() nel metodo onPause() dell'attività che sta gestendo le notifiche di push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
