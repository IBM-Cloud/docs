---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Inicializando o plug-in Cordova
{: #cordova_enable}

Antes de poder usar o plug-in Push
Notification
Service Cordova, é necessário inicializá-lo transmitindo a rota e o
GUID do aplicativo. Depois de inicializar o plug-in, é possível conectar-se ao app de
servidor criado no painel do Bluemix. O plug-in Cordova é o wrapper dos SDKs de cliente
Android e iOS para permitir que um app Cordova se comunique com serviços Bluemix.

1. Inicialize o BMSClient copiando e colando o fragmento de código a seguir no
arquivo JavaScript principal (em geral, localizado no diretório **www/js**).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modifique o fragmento de código para usar os parâmetros Route e appGUID do
Bluemix. Clique no link **Opções móveis** no Painel do aplicativo
Bluemix para obter a rota e o GUID do aplicativo. Use os valores Rota e GUID do App como
parâmetros no fragmento de código ```BMSClient.initialize```.


	**Observação**: Se você tiver criado um app Cordova usando a
CLI do Cordova, por exemplo, o comando Cordova create app-name, coloque este código
Javascript no arquivo **index.js**, após a função
```app.receivedEvent``` dentro da função o```nDeviceReady:
function()`` para inicializar o cliente BMS.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Próxima etapa. [Registrando
dispositivos](t_cordova_register.html).
