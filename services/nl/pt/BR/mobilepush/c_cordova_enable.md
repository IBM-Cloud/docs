---

copyright:
 years: 2015, 2016

---

# Ativando aplicativos Cordova para receber
notificações push
{: #cordova_enable}

Cordova é uma plataforma para criar aplicativos híbridos
com JavaScript, CSS e HTML. O {{site.data.keyword.mobilepushshort}} suporta o
desenvolvimento de aplicativos iOS e Android baseados em Cordova.

Ative aplicativos Cordova para
receber notificações push e enviar notificações push para
seus dispositivos.




## Instalando o plug-in Push do Cordova
{: #cordova_install}

Instale e use o plug-in Push do cliente para
desenvolver ainda mais seus aplicativos Cordova. Isso
também instala o plug-in Núcleo do Cordova, que inicializa sua
conexão com o Bluemix.

### Antes de começar

1. Faça download das versões mais recentes do Android Studio SDK e Xcode.
1. Configure o emulador. Para Android Studio, use um emulador que suporte a API do Google.
1. Instale a ferramenta de linha de comandos Git. Para Windows, certifique-se de
selecionar a opção **Executar Git no prompt de comandos do Windows**. Para
obter informações sobre como fazer download e instalar essa ferramenta, consulte
[Git](https://git-scm.com/downloads).

1. Instale o Node.js e a ferramenta Node Package Manager (NPM). A ferramenta de
linha de comandos NPM é empacotada com o Node.js. Para obter informações sobre como fazer download e instalar o Node.js, consulte
[Node.js](https://nodejs.org/en/download/).
1. Na linha de comandos, instale as ferramentas de linha de comandos Cordova
usando o comando **npm install -g cordova**. Isso é
necessário para usar o plug-in Push do Cordova. Para obter informações sobre como
instalar o Cordova e configurar o app Cordova, consulte
[Cordova Apache](https://cordova.apache.org/#getstarted).

 **Nota**: Para visualizar o arquivo leia-me do plug-in Push do
Cordova, acesse [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)

1. Mude para a pasta na qual deseja criar seu app Cordova e
execute o comando a seguir para criar um aplicativo Cordova. Se
você tiver um app Cordova existente, vá para a etapa 3.

 ```
cordova create your_app_name
	cd your_app_name
```
1. Opcional: (Opcional) Edite o arquivo **config.xml** e mude o
nome do aplicativo no elemento <name> para um da sua escolha, em vez do nome
HelloCordova padrão.

	**Nota**: Certifique-se de especificar o ID do pacote
configurável correto. Se você não fizer isso, as mensagens de erro a seguir serão
exibidas no Xcode.
	* O executável foi assinado com autorizações inválidas.
	* As autorizações especificadas no arquivo de autorizações de assinatura de
código do aplicativo não correspondem às especificadas no seu perfil de fornecimento.

	Para corrigir esse problema, especifique o ID do pacote configurável correto no
Xcode ou no arquivo **config.xml** do seu app Cordova.

1. Inclua a API mínima suportada ou a declaração de destino de
implementação no arquivo config.xml do seu aplicativo Cordova. O valor minSdkVersion deve
ser maior que 15. O valor targetSdkVersion deve sempre refletir o SDK mais recente do
Android que esta disponível no Google.
	* **Android** - com seu editor, abra o arquivo config.xml e atualize o elemento
   ```<platform name="android">``` com as versões mínima e de destino do SDK:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - Atualize o elemento <platform name="ios">
com uma declaração de destino de implementação:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Na interface da linha de comandos (CLI) do Cordova, inclua suas plataformas: iOS,
Android, ou ambas, usando os comandos a seguir.

	```
	cordova platform add ios@3.9.0
	cordova platform add android
	```
1. No diretório raiz do aplicativo Cordova, insira o comando a seguir para
instalar o plug-in Push do Cordova: **cordova plugin add ibm-mfp-push**.

	Dependendo das plataformas incluídas, você vê algo semelhante ao
seguinte:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Em *your-app-root-folder*, verifique se o plug-in Principal e Push
do Cordova foram instalados com sucesso usando o comando a seguir: **cordova plugin list**.

	Dependendo das plataformas incluídas, você vê algo semelhante ao
seguinte:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (Somente iOS) - Configure seu ambiente de desenvolvimento iOS.
	a. Abra o arquivo your-app-name.xcodeproj no diretório *your-app-name***/platforms/ios** com Xcode.

	b. Inclua o Cabeçalho de ponte. Acesse **Configurações de compilação >
Compilador Swift - Geração de código > Cabeçalho de ponte Objective-C** e inclua o
caminho a seguir: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Inclua o parâmetro Frameworks. Acesse **Configurações de compilação > Link > Caminhos da procura Runpath** e inclua o parâmetro a seguir:
	```
	@executable_path/Frameworks
	```
	d. Remova o comentário das instruções de importação Push a seguir em seu cabeçalho de ponte. Acesse *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Compile e execute seu aplicativo com Xcode.
1. (Somente Android)- Compile seu projeto Android usando o comando a seguir:
**cordova build android**.

	**Nota**: Antes de abrir seu projeto no Android Studio,
deve-se primeiro compilar o aplicativo Cordova por meio da CLI do Cordova. Caso
contrário, você encontrará erros de compilação.


## Inicializando o plug-in Cordova
{: #cordova_initialize}

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

## Registrando Dispositivos
{: #cordova_register}

Para registrar um dispositivo no Serviço de notificação push, chame o método de
registro.

Copie e cole o fragmento de código a seguir em seu aplicativo
Cordova para registrar um dispositivo.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

### Android
{: #cordova_register_android}
O Android não usa o parâmetro de definições. Se você estiver somente compilando um app
Android, passe um objeto vazio; por exemplo:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

### iOS
{: #cordova_register_ios}
Se deseja customizar o alerta, badge e propriedades de som,
inclua o seguinte fragmento de código JavaScript na
web part de seu aplicativo Cordova.

```
	var settings = {
	   ios: {
	       alert: true,
	       badge: true,
	       sound: true
	   }
	}
	MFPPush.registerDevice(settings, success, failure);
```



### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

É possível acessar o conteúdo do parâmetro de resposta de sucesso em Javascript usando JSON.parse:
**var token = JSON.parse(response).token**


As chaves disponíveis são estas: ```token```, ```userId`` e ```deviceId``.

O fragmento de código JavaScript a seguir mostra como inicializar o SDK do cliente Bluemix
Mobile Services, registrar um dispositivo no Serviço de notificação push e atender a
notificações push. Coloque esse código em seu arquivo Javascript.



```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

within the **onDeviceReady: function()**.

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
         ios: {
             alert: true,
             badge: true,
             sound: true
         }   
     };
     MFPPush.registerDevice(settings, success, failure);
     var notification = function(notif){
         alert (notif.message);
     };
     MFPPush.registerNotificationsCallback(notification);

 }
```

### Objective-C
{: #cordova_register_objective}
Inclua o fragmento de código Objective-C a seguir em sua classe de delegação de aplicativo.

```
	// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

###Swift
{: #cordova_register_swift}
Inclua o seguinte fragmento de código Swift em sua classe de
delegação de aplicativo.

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##Próximas Etapas

{: #cordova_register_next}

Compile seu projeto e, em seguida, execute-o usando os comandos a seguir:

	* Android - **cordova build android** e depois **cordova run android**

	* iOS - **cordova build ios** e depois **cordova run ios**



## Recebendo notificações push em dispositivos
{: #cordova_receive}

Copie e cole os fragmentos de código a seguir para receber
notificações push em dispositivos.

###JavaScript

Inclua o seguinte fragmento de código JavaScript
na web part do seu aplicativo Cordova.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

###Propriedades de notificação do Android

A seção a seguir lista as propriedades de notificação de Android:

* message - mensagem de notificação push
* payload - objeto JSON contendo uma carga útil de notificação


###Propriedades de notificação do iOS

A seguinte seção lista as propriedades de notificação iOS:

* message - mensagem de notificação push
* payload - objeto JSON que contém uma carga útil de notificação
action-loc-key - A sequência é usada como chave para obter uma sequência localizada na
localização atual a ser usada para o título do botão direito, em vez de “Visualizar".
* badge - O número a ser exeibido como o badge do ícone de app. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.
* sound - O nome de um arquivo de som no pacote configurável de app
ou na pasta Biblioteca/sons do contêiner de dados de app.

###Objective-C

Inclua os fragmentos de código Objective-C a seguir em sua classe de delegação de
aplicativo.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

###Swift

Inclua os fragmentos de código Swift a seguir em sua classe de delegação de
aplicativo.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```


{: #push-send-notifications}
## Enviando notificações push básicas


Depois de desenvolver seus aplicativos, é possível enviar notificações push básicas (sem usar tags, badges, cargas úteis adicionais ou arquivos de som).


Envie notificações push básicas.

1. Em **Escolher o público**,
selecione um dos seguintes públicos:
      **Todos os dispositivos**, ou por
plataforma: **Apenas dispositivos iOS**
ou
      **Apenas dispositivos Android**.


	**Nota**: Ao selecionar a opção **Todos os dispositivos**, todos os
dispositivos inscritos para notificações push recebem sua notificação.

	![Tela Notificações](images/tag_notification.jpg)

2. Em **Criar sua notificação**, insira sua mensagem e clique
em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

	A captura de tela a seguir mostra uma caixa de alerta que manipula uma
notificação push em primeiro plano em um dispositivo Android e iOS.

	![Notificação push em primeiro plano no Android](images/Android_Screenshot.jpg)

	![Notificação push em primeiro plano no iOS](images/iOS_Screenshot.jpg)

	A captura de tela a seguir mostra uma notificação push no plano de fundo para Android.
	![Notificação push no plano de fundo no Android](images/background.jpg)



## Etapas Seguintes
{: #next_steps_tags}

Depois de configurar com êxito notificações básicas,
é possível configurar notificações baseadas em tag e opções
avançadas.

Inclua esses recursos do Serviço de notificações push em seu app.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, consulte [Notificações push avançadas](t_advance_notifications.html).
