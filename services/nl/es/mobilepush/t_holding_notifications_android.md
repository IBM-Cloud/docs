---

copyright:
 años: 2015, 2016

---

# Retención de notificaciones para Android
{: #hold-notifications-android}

Cuando su aplicación entre en segundo plano, probablemente querrá enviar por push para
                            contener notificaciones de volver que se envían a la aplicación. Para retener notificaciones, invoque el método hold() en el método onPause() de la actividad que maneja las notificaciones push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
