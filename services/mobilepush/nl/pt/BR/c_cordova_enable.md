---

copyright:
 years: 2015, 2016

---

# Ativando aplicativos Cordova para receber notificações push
{: #cordova_enable}
Última atualização: 17 de outubro de 2016
{: .last-updated}

Cordova é uma plataforma para construir aplicativos híbridos com JavaScript, CSS e HTML. O {{site.data.keyword.mobilepushshort}} suporta o desenvolvimento de aplicativos iOS e Android baseados em Cordova.

É possível ativar aplicativos Cordova para receber notificações push para os seus dispositivos.

## Instalando o plug-in do push Cordova
{: #cordova_install}

Instale e use o plug-in de push do cliente para desenvolver ainda mais seus aplicativos Cordova. Isso também instala o plug-in núcleo do Cordova, que inicializa sua conexão com o Bluemix.

### Antes de começar

1. Faça download das versões mais recentes do Android Studio SDK e Xcode.
1. Configure o emulador. Para Android Studio, use um emulador que suporte a API do Google.
1. Instale a ferramenta de linha de comandos Git. Para Windows, certifique-se de selecionar a opção **Executar Git no prompt de comandos do Windows**. Para obter informações sobre como fazer download e instalar essa ferramenta, consulte [Git](https://git-scm.com/downloads).
1. Instale o Node.js e a ferramenta Node Package Manager (NPM). A ferramenta de linha de comandos NPM é empacotada com o Node.js. Para obter informações sobre como fazer download e instalar o Node.js, consulte [Node.js](https://nodejs.org/en/download/).
1. Na linha de comandos, instale as ferramentas de linha de comandos Cordova usando o comando **npm install -g cordova**. Isso é necessário para usar o plug-in de push Cordova. Para obter informações sobre como instalar o Cordova e configurar o app Cordova, consulte [Cordova Apache](https://cordova.apache.org/#getstarted). Para
obter mais informações, veja o [arquivo
Leia-me](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push) do plug-in push do Cordova.
1. Mude para a pasta na qual deseja criar seu app Cordova e execute o comando a seguir para criar um aplicativo Cordova. Se você tiver um app Cordova existente, vá para a etapa 3.
```
cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Opcional: é possível editar o arquivo **config.xml** e mudar o nome do aplicativo no elemento <name> para um nome de sua escolha, em
vez do nome HelloCordova padrão.

Assegure-se de especificar o ID de pacote configurável correto. As mensagens de erro a seguir poderão resultar em Xcode, se um ID de pacote configurável
incorreto for especificado.

* O executável foi assinado com autorizações inválidas.
* As autorizações especificadas no arquivo de autorizações de assinatura de código do aplicativo não correspondem às especificadas no seu perfil de fornecimento. Para corrigir esse problema, especifique o ID do pacote configurável correto no Xcode ou no arquivo **config.xml** do seu app Cordova.

1. Inclua a API mínima suportada ou a declaração de destino de implementação no arquivo config.xml do seu aplicativo Cordova. O valor minSdkVersion deve ser maior que 15. O
valor targetSdkVersion deve sempre refletir o SDK mais recente do Android que está disponível no Google.
	
	* Android - com seu editor, abra o arquivo config.xml e atualize o
elemento `<platform name="android">` com as versões de SDK mínima e de destino:

```
< !-- add deployment target declaration --> 
add deployment target declaration <preference name="android-minSdkVersion" value="15" />
  <preference name="android-targetSdkVersion" value="23" />
</platform>
```
    {: codeblock}

   * iOS - atualize o elemento <platform name="ios"> com uma declaração de destino de implementação:

```
<platform name ="ios">
<preference name=deployment-target" value="8.0" /> <!-- other properties -->
</ platform>
```
	{: codeblock}

1. Na interface da linha de comandos (CLI) do Cordova, inclua suas plataformas: iOS, Android, ou ambas, usando o comando:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. No diretório raiz do aplicativo Cordova, insira o comando a seguir para instalar o plug-in de push Cordova: **cordova plugin add ibm-mfp-push**. Dependendo
das plataformas que você incluiu, será possível ver:
```
Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
```
	{: codeblock}

1. Em *your-app-root-folder*, verifique se os plug-ins núcleo e de push do Cordova foram instalados com sucesso usando o comando a seguir: **cordova plugin list**. 
Dependendo das plataformas que você incluiu, será possível ver:
```
ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
```
	{: codeblock}

1. (Somente iOS) - Configure seu ambiente de desenvolvimento iOS.
2. Conclua as subetapas a seguir:

 a. Abra o arquivo your-app-name.xcodeproj no diretório *your-app-name***/platforms/ios** com Xcode.

 b. Inclua o Cabeçalho de ponte. Acesse **Configurações de construção > Compilador Swift - Geração de código > Cabeçalho de ponte Objective-C** e
inclua
o caminho a seguir: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

 c. Inclua o parâmetro Frameworks. Acesse **Configurações de compilação > Vinculação > Caminhos da procura runpath** e inclua o parâmetro
`@executable_path/Frameworks`.

 d. Remova o comentário das instruções de importação Push a seguir em seu cabeçalho de ponte. Acesse *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

```
//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
```
	{: codeblock}

 e. Compile e execute seu aplicativo com Xcode.

1. (Somente Android)- Construa seu projeto Android usando o comando a seguir: **cordova build android**.

	**Nota**: antes de abrir o projeto no Android Studio, construa seu aplicativo Cordova por meio da CLI do Cordova. Isso ajudará a evitar erros de construção.


## Inicializando o plug-in Cordova
{: #cordova_initialize}

Antes de poder usar o plug-in Cordova do serviço {{site.data.keyword.mobilepushshort}}, é necessário inicializá-lo passando a rota do aplicativo e o GUID do aplicativo. Depois de inicializar o plug-in, é possível conectar-se ao app de servidor criado no painel do Bluemix. O plug-in Cordova é o wrapper dos SDKs de cliente Android e iOS para permitir que um app Cordova se comunique com serviços Bluemix.

1. Inicialize o BMSClient copiando e colando o fragmento de código a seguir no arquivo JavaScript principal (em geral, localizado no diretório **www/js**).

```
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
```
	{: codeblock}

1. Modifique o fragmento de código para usar os parâmetros Route e appGUID do Bluemix. Clique no link **Opções móveis** no Painel Push para obter a rota do app, o GUID do app e o segredo do cliente. Use os valores de GUID de rota e aplicativo como seus parâmetros em seu fragmento de código `BMSClient.initialize`.

	**Nota**: se você tiver criado um aplicativo Cordova usando a CLI Cordova, por exemplo, comando do nome do
aplicativo de criação Cordova, coloque este código Javascript no arquivo **index.js**, após a função `app.receivedEvent` na função `onDeviceReady: function()` para inicializar o cliente BMS.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
    },
```
	{: codeblock}

## Registrando Dispositivos
{: #cordova_register}


Para registrar um dispositivo com o serviço {{site.data.keyword.mobilepushshort}}, chame o método de registro. Copie o fragmento de código a seguir em seu aplicativo Cordova para registrar um dispositivo.

```
var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

### Android
{: #cordova_register_android}
O Android não usa o parâmetro de definições. Se você estiver somente construindo um aplicativo Android, passe um objeto vazio. Por exemplo:

```
MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```
	{: codeblock}

### iOS
{: #cordova_register_ios}
Para customizar o alerta, badge e propriedades do som, inclua o fragmento de código JavaScript a seguir na web part do seu aplicativo Cordova.

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
	{: codeblock}


### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

É possível acessar o conteúdo do parâmetro de resposta de sucesso em Javascript usando JSON.parse:
**var token = JSON.parse(response).token**


As chaves disponíveis são: `token` e `deviceId`.

O fragmento de código JavaScript a seguir mostra como inicializar o Bluemix Mobile Services client SDK, registrar um dispositivo com o serviço {{site.data.keyword.mobilepushshort}} e atender a notificações push. Inclua esse código no arquivo Javascript.

```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```
	{: codeblock}

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}
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
	{: codeblock}

### Objective-C
{: #cordova_register_objective}
Inclua o fragmento de código Objective-C a seguir em sua classe de delegação de aplicativo.

```
// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application
didRegisterForRemoteNotificationsWithDeviceToken:(NSData
*)deviceToken {
  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```
	{: codeblock}

###Swift
{: #cordova_register_swift}
Inclua o seguinte fragmento de código Swift em sua classe de delegação de aplicativo.

```
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}

##Próximas Etapas

{: #cordova_register_next}

Compile seu projeto e, em seguida, execute-o usando os comandos a seguir:

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Recebendo notificações push em dispositivos
{: #cordova_receive}

Copie o fragmento de código a seguir para receber notificações push em dispositivos.

###JavaScript

Inclua o seguinte fragmento de código JavaScript na web part do seu aplicativo Cordova.
```
var notification = function(notification){
    // notification is a JSON object.
alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```
	{: codeblock}

###Propriedades de notificação do Android

A seção a seguir lista as propriedades de notificação de Android:

* message - mensagem de notificação push
* payload - objeto JSON contendo uma carga útil de notificação


###Propriedades de notificação do iOS

A seguinte seção lista as propriedades de notificação iOS:

* message - mensagem de notificação push
* payload - Objeto JSON que contém uma carga útil de notificação
action-loc-key - A sequência é usada como chave para obter uma sequência localizada na localização atual para ser usada para o título de botão apropriado, em vez de `Visualizar`.
* badge - O número a ser exibido como o badge do ícone de app. Se essa propriedade estiver ausente, o badge não será mudado. Para remover o badge, configure o valor dessa propriedade para 0.
* sound - O nome de um arquivo de som no pacote configurável de app ou na pasta Biblioteca/sons do contêiner de dados de app.

###Objective-C

Inclua os fragmentos de código Objective-C a seguir em sua classe de delegação de aplicativo.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
fetchCompletionHandler:(void
(^)(UIBackgroundFetchResult))completionHandler {
 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```
	{: codeblock}


```
// Handle receiving a remote notification on launch
		- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
	}
```
	{: codeblock}

###Swift

Inclua os fragmentos de código Swift a seguir em sua classe de delegação de aplicativo.
```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){
  CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
	}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
	}
```
	{: codeblock}

## Enviando notificações push básicas
{: #push-send-notifications}

Depois de ter desenvolvido seus aplicativos, será possível enviar notificações push básicas.

Para enviar notificações push básicas, conclua as etapas:

1. Selecione **Enviar notificações** e componha uma mensagem
escolhendo uma opção **Enviar para**. As opções suportadas são
**Dispositivo por tag**, **ID do dispositivo**,
**ID do usuário**, **Dispositivos Android**,
**Dispositivos iOS**, **Notificações da web** e
**Todos os dispositivos**.
**Nota**: ao selecionar a opção **Todos os dispositivos**, todos os dispositivos inscritos para {{site.data.keyword.mobilepushshort}} receberão notificações.
![Tela Notificações](images/tag_notification.jpg)

2. No campo **Mensagem**, componha sua mensagem. Escolha a
configurar das definições opcionais conforme necessário.
3. Clique em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

A captura de tela a seguir mostra uma caixa de alerta que manipula um {{site.data.keyword.mobilepushshort}} no primeiro plano em dispositivos Android e iOS.

![Notificação push em primeiro plano no Android](images/Android_Screenshot.jpg)

![Notificação push em primeiro plano no iOS](images/iOS_Screenshot.jpg)

   A imagem a seguir mostra {{site.data.keyword.mobilepushshort}} no segundo plano para Android.
![Notificação push no plano de fundo no Android](images/background.jpg)

## Etapas Seguintes
{: #next_steps_tags}

Depois de configurar com êxito notificações básicas,
é possível configurar notificações baseadas em tag e opções
avançadas.

Inclua os recursos do serviço {{site.data.keyword.mobilepushshort}} em seu app.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, veja [Ativando notificações push avançadas](t_advance_badge_sound_payload.html).
