---

copyright:
 años: 2015, 2016

---

{:new_window: target="_blank"}

# Inicialización del plug-in de Cordova
{: #cordova_enable}

Para poder utilizar el plug-in de Cordova del Servicio de notificaciones Push, debe inicializarlo
pasando la ruta de la aplicación y el GUID de aplicaciones. Tras inicializar el plug-in, puede conectarse a la aplicación del servidor que ha creado en el panel de control de Bluemix. El plug-in de Cordova es el continente para los
SDK de cliente de iOS y Android para habilitar a una aplicación de Cordova a comunicarse con los servicios de Bluemix.

1. Inicialice el BMSClient copiando y pegando el siguiente fragmento de código en el archivo JavaScript principal (normalmente ubicado en el directorio **www/js**).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modifique el fragmento de código para que utilice los parámetros Ruta y appGUID de Bluemix. Pulse el enlace **Opciones móviles** en el Panel de control de aplicaciones de Bluemix para obtener la ruta de la aplicación y la GUID de la app. Utilice los valores de Ruta y GUID de la app como parámetros en el fragmento de código ```BMSClient.initialize```.


	**Nota**: Si ha creado una app de Cordova utilizando el CLI de Cordova, por ejemplo, el mandato Cordova create app-name, coloque este código Javascript en el archivo **index.js**, después de que la función ```app.receivedEvent``` dentro de la función o```nDeviceReady: function()`` inicialice el cliente BMS.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Siguiente paso. [Registro de dispositivos](t_cordova_register.html).
