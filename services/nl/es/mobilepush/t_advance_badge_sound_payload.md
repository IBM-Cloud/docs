---

copyright:
 años: 2015, 2016

---

{:new_window: target="_blank"}
# Configure un identificador, sonido y carga útil e identificador iOS

{: #badge-sound-payload}

Configure un identificador de iOS, un sonido y la carga útil adicional de JSON.

1. En el panel de control Notificaciones Push, vaya al
                        separador **Notificaciones**.
2. Vaya a la sección **Campos opcionales** para configurar las
                    siguientes características de notificaciones push. Identificador de iOS, sonido y carga útil adicional.

	a. **Identificador iOS**: Para dispositivos iOS, el número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el
                            identificador no se modificará. Para eliminar el identificador, establezca el valor de esta
                            propiedad en 0.

	b. **Archivo de sonido**: Escriba una serie que apunte al archivo de sonido de la app móvil. En la carga útil, especifique el nombre de serie del
                            archivo de sonido a utilizar.


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
**Carga útil adicional**: Esta carga útil puede ser cualquier
                            par de valores de claves y debe ser un objeto JSON que desee enviar con la
                            notificación push.

	```
	{"key":"value", "key2":"value2"}
	```
