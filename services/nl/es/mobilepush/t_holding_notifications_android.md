---

copyright:
 years: 2015, 2016

---

# Retención de notificaciones para Android
{: #hold-notifications-android}
*Última actualización: 14 de junio de 2016*
{: .last-updated}

Cuando su aplicación entre en segundo plano, probablemente querrá enviar por push el servicio de notificación para retener notificaciones que se envían a la aplicación. Para retener notificaciones, invoque el método hold() en el método onPause() de la actividad que maneja las notificaciones push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```
