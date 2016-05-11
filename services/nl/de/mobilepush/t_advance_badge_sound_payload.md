---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Audio, Nutzdaten und iOS Badge konfigurieren

{: #badge-sound-payload}

Konfigurieren Sie ein iOS Badge, Audio und zusätzliche JSON-Nutzdaten.

1. Navigieren Sie im Dashboard für Push-Benachrichtigungen zur Registerkarte **Benachrichtigungen**.
2. Konfigurieren Sie im Abschnitt **Optionale Felder** die folgenden Komponenten für
Push-Benachrichtigungen: 
	a. **iOS Badge**: Für iOS-Geräte die Nummer, die als Badge für das App-Symbol angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen,
legen Sie für diese Eigenschaft den Wert 0 fest.

	b. **Sound File**: Geben Sie eine Zeichenfolge ein, die auf die Audiodatei in Ihrer mobilen App verweist. Geben Sie den Zeichenfolgenamen der zu verwendenden Audiodatei in den Nutzdaten an.


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
**Zusätzliche Nutzdaten** - Diese Nutzdaten können ein beliebiges Schlüssel/Wert-Paar sein; es muss sich jedoch um ein JSON-Objekt handeln, das Sie mit der Push-Benachrichtigung senden möchten.

	```
	{"key":"value", "key2":"value2"}
	```
