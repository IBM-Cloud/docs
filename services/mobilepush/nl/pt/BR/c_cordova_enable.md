---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando aplicativos Cordova para receber
notificações push
{: #cordova_enable}
Última atualização: 18 de janeiro de 2017
{: .last-updated}

Cordova é uma plataforma para criar aplicativos híbridos
com JavaScript, CSS e HTML. O serviço {{site.data.keyword.mobilepushshort}} suporta o desenvolvimento
de aplicativos iOS e Android baseados em Cordova.

É possível ativar aplicativos Cordova para receber notificações push para os seus dispositivos.

## Instalando o plug-in do push Cordova
{: #cordova_install}

Instale e use o plug-in de push do cliente para desenvolver ainda mais seus aplicativos Cordova. Isso também instala o plug-in núcleo do Cordova, que inicializa sua conexão com o Bluemix.

### Antes de começar

1. Faça download das versões mais recentes do Android Studio SDK e Xcode.
1. Configure o emulador. Para Android Studio, use um emulador que suporte a API do Google.
1. Instale a ferramenta de linha de comandos Git. Para Windows, certifique-se de
selecionar a opção **Executar Git no prompt de comandos do Windows**. Para obter informações sobre como fazer download e instalar essa ferramenta, veja o [Git ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}.
1. Instale o Node.js e a ferramenta Node Package Manager (NPM). A ferramenta de
linha de comandos NPM é empacotada com o Node.js. Para obter informações sobre como fazer download e instalar o Node.js, veja [Node.js ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/en/download/){: new_window}.
1. Na linha de comandos, instale as ferramentas de linha de comandos Cordova
usando o comando **npm install -g cordova**. Isso é necessário para usar o plug-in de push Cordova. Para obter informações sobre como instalar o Cordova e configurar seu app Cordova, veja [Cordova Apache ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}. Para obter mais informações, veja o [Arquivo leia-me ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} do plug-in push Cordova.
1. Mude para a pasta na qual deseja criar seu app Cordova e
execute o comando a seguir para criar um aplicativo Cordova. Se
você tiver um app Cordova existente, vá para a etapa 3.
```cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Opcional: é possível editar o arquivo **config.xml** e mudar o nome do aplicativo no elemento <name> para um nome de sua escolha, em
vez do nome HelloCordova padrão.

Assegure-se de especificar o ID de pacote configurável correto. As mensagens de erro a seguir poderão resultar em Xcode, se um ID de pacote configurável
incorreto for especificado.

* O executável foi assinado com autorizações inválidas.
* As autorizações especificadas no arquivo de autorizações de assinatura de código do aplicativo não correspondem às especificadas no seu perfil de fornecimento. Para corrigir esse problema, especifique o ID do pacote configurável correto no
Xcode ou no arquivo **config.xml** do seu app Cordova.

1. Inclua a API mínima suportada ou a declaração de destino de
implementação no arquivo config.xml do seu aplicativo Cordova. O valor minSdkVersion deve
ser maior que 15. O valor targetSdkVersion deve sempre refletir o SDK mais recente do
Android que esta disponível no Google.
	
	* Android - com seu editor, abra o arquivo **config.xml** e atualize o
elemento `<platform name="android">` com as versões de SDK mínima e de destino:

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - atualize o elemento <platform name="ios"> com uma declaração de destino de implementação:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. Na interface da linha de comandos (CLI) do Cordova, inclua suas plataformas: iOS, Android, ou ambas, usando o comando:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. No diretório-raiz do aplicativo Cordova, insira o comando a seguir para instalar o plug-in de push do Cordova: **cordova plugin add bms-push**. Dependendo das plataformas que você incluiu, será possível ver:
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Em your-app-root-folder, verifique se os plug-ins de núcleo e de push do Cordova foram instalados com sucesso usando o comando a seguir: **cordova plugin list**. Dependendo das plataformas que você incluiu, será possível ver:
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configure o ambiente de desenvolvimento iOS.
2. Compile e execute seu aplicativo com Xcode.
1. Faça download do `google-services.json` do Firebase para android e coloque-o na pasta raiz do projeto Cordova, em `[your-app-name]/platforms/android.
	1. Acesse `[your-app-name]/platforms/android`.
	2. Abra o arquivo `build.gradle` (caminho: plataforma > android > build.gradle).
	3. Localize o texto `buildscript` no arquivo `build.gradle`.
	4. Após a linha de caminho de classe, inclua a linha classpath 'com.google.gms:google-services:3.0.0'
	5. Em seguida, localize "dependencies". Selecione as dependências que tenham o texto `compile` e onde essas dependências terminam, logo após isso, inclua esta linha :apply plugin: 'com.google.gms.google-services'.
	6. Prepare e construa o projeto Cordova Android.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Nota**: antes de abrir o projeto no Android Studio, construa seu aplicativo Cordova por meio da CLI do Cordova. Isso ajudará a evitar erros de construção.

## Inicializando o plug-in Cordova
{: #cordova_initialize}

Antes de poder usar o plug-in do Cordova do serviço {{site.data.keyword.mobilepushshort}}, é necessário inicializá-lo passando a rota do aplicativo e o GUID do aplicativo. Depois de inicializar o plug-in, é possível conectar-se ao app de
servidor criado no painel do Bluemix. O plug-in Cordova é o wrapper dos SDKs de cliente
Android e iOS para permitir que um app Cordova se comunique com serviços Bluemix.

1. Inicialize o BMSClient copiando e colando o fragmento de código a seguir no
arquivo JavaScript principal (em geral, localizado no diretório **www/js**).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Transmita a região para seu aplicativo. As constantes a seguir são fornecidas:

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Por exemplo:

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Observação**: se você tiver criado um aplicativo Cordova usando a CLI do Cordova, por exemplo, o comando create app-name do Cordova, coloque este código Javascript no arquivo index.js, após a função app.receivedEvent na função onDeviceReady: function() para inicializar o `BMSClient`. 


## Registrando Dispositivos
{: #cordova_register}


Para registrar um dispositivo com o serviço {{site.data.keyword.mobilepushshort}}, chame o método de registro. Copie o fragmento de código a seguir em seu aplicativo Cordova para registrar um dispositivo.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

O fragmento de código JavaScript a seguir mostra como inicializar o Bluemix Mobile Services client SDK, registrar um dispositivo com o serviço {{site.data.keyword.mobilepushshort}} e atender a notificações push. Inclua esse código no arquivo Javascript.

Dentro de **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Inclua o seguinte fragmento de código Swift em sua classe de
delegação de aplicativo.

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

##Etapas Seguintes

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

Inclua o seguinte fragmento de código JavaScript
na web part do seu aplicativo Cordova.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

###Propriedades de notificação do Android

A seção a seguir lista as propriedades de notificação de Android:

* **message** - mensagem de notificação push
* **payload** - objeto JSON contendo uma carga útil de notificação


###Propriedades de notificação do iOS

A seguinte seção lista as propriedades de notificação iOS:

* **message** - mensagem de notificação push
* **payload** - objeto JSON que contém uma carga útil de notificação action-loc-key - a sequência é usada como chave para obter uma sequência localizada no local atual, a ser usada para o título de botão apropriado, em vez de `Visualizar`.
* **badge** - o número a ser exibido como o badge do ícone de app. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.
* **sound** - o nome de um arquivo de som no pacote configurável de app ou na
pasta Biblioteca/Sons do contêiner de dados de app.


Inclua os fragmentos de código Swift a seguir em sua classe de delegação de
aplicativo.
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
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
![Tela de notificações](images/tag_notification.jpg)

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

Inclua os recursos de serviço do {{site.data.keyword.mobilepushshort}} no seu app. Para usar
notificações baseadas em tag, consulte [Notificações baseadas em
tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, veja [Ativando notificações push avançadas](t_advance_badge_sound_payload.html).
