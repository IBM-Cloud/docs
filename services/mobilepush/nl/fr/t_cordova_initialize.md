---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}

# Initialisation du plug-in Cordova
{: #cordova_enable}

Pour pouvoir utiliser le plug-in Cordova du service Push Notifications, vous devez l'initialiser en transmettant la route de l'application et
l'identificateur global unique de l'application. Une fois le plug-in initialisé, vous pouvez vous connecter à l'application serveur que vous avez créée dans le tableau de bord Bluemix. Le plug-in Cordova est l'encapsuleur pour les logiciels SDK de client Android et iOS qui permettent à une application Cordova de communiquer avec les services Bluemix.

1. Initialisez le client BMS en copiant et en collant le fragment de code suivant dans votre fichier JavaScript principal (généralement situé sous le répertoire **www/js**).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modifiez le fragment de code pour qu'il utilise vos paramètres de route et d'identificateur global unique Bluemix. Cliquez sur le lien **Options pour application mobile** dans le tableau de bord de votre application Bluemix pour obtenir la route et l'identificateur global unique de l'application. Utilisez les valeurs Route et Identificateur global unique de l'application comme paramètres dans votre fragment de code ```BMSClient.initialize```.


	**Remarque** : Si vous avez créé une appli Cordova à l'aide de l'interface CLI Cordova, par exemple, la commande Cordova create app-name, placez ce code Javascript dans le fichier **index.js**, après la fonction ```app.receivedEvent``` dans la fonction o```nDeviceReady: function()``, afin d'initialiser le client BMS.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Etape suivante. [Enregistrement des périphériques](t_cordova_register.html).
