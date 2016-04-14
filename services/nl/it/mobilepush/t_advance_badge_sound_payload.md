---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configurazione di badge, audio e payload e badge iOS

{: #badge-sound-payload}

Configura un badge, l'audio e del payload JSON aggiuntivo iOS.

1. Nel dashboard Push Notifications, vai alla scheda **Notifications**.
2. Vai alla sezione **Optional Fields** per configurare le seguenti funzioni di notifica di
                    push. badge ios, audio e payload aggiuntivo.

	a. **Badge iOS** - per i dispositivi iOS, il numero da visualizzare come badge dell'icona applicazione. Se questa proprietà
                            non è presente, il badge non viene modificato. Per rimuovere il badge, imposta
                            il valore di questa proprietà su 0.

	b. **File audio** - immetti una stringa per puntare al file audio nella tua applicazione mobile. Nel payload, specifica
                            il nome stringa del file audio da utilizzare.


	Android

	```
	"settings": {
	     "gcm" : {
	     "sound":"tt.wav",
	  }
	 }  
	```

	iOS

	```
	"settings": {
	     "apns" : {
	      "badge": 10,
	      "sound": "tt.wav",
	  }
	}
	``` 		
**Payload aggiuntivo** - questo payload può essere qualsiasi coppia chiave-valore e deve essere un
                            oggetto JSON che vuoi inviare con la notifica di push.

	```
	{"chiave":"valore", "chiave2":"valore2"}
	```
