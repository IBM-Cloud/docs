---

copyright:
 years: 2015, 2016

---

# Push-Benachrichtigungen in Android-Geräten empfangen
{: #android_receive}

Rufen Sie die Methode **MFPPush.listen()** auf, um das Objekt 'notificationListener' für Push zu registrieren. Diese Methode wird in der Regel über die Methode **onResume()** der Aktivität aufgerufen, die Push-Benachrichtigungen verarbeitet.

1. Rufen Sie die Methode **listen()** auf, um das Objekt 'notificationListener' für Push zu registrieren. Diese Methode wird in der Regel über die Methode **onResume()** der Aktivität aufgerufen, die Push-Benachrichtigungen verarbeitet.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Erstellen Sie einen Build für das Projekt und führen Sie ihn in dem Gerät oder im Emulator aus. Wenn die Methode
onSuccess() für den Antwortlistener in der Methode register() aufgerufen wird, wird bestätigt, dass das Gerät erfolgreich für Push Notifications Service registriert wurde. An diesem Punkt können Sie gemäß der in 'Einfache Push-Benachrichtigungen senden' beschriebenen Anleitung eine Nachricht senden.
3. Überprüfen Sie, ob die Geräte Ihre Benachrichtigung empfangen haben. Wenn die Anwendung im Vordergrund
ausgeführt wird, wird die Benachrichtigung von **MFPPushNotificationListener** verarbeitet. Wenn die Anwendung im Hintergrund ausgeführt wird, wird eine Nachricht in der Benachrichtigungsleiste angezeigt.
