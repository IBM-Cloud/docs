---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando notificações para dispositivos móveis
{: #c_enable_push-notifications}
Última atualização: 12 de abril de 2017
{: .last-updated}

Assegure-se de que você tenha passado por [Configurando credenciais para um provedor de notificação](t__main_push_config_provider.html).

Esta seção descreve como ativar os seus aplicativos clientes - aplicativos móveis e de navegador da web, bem como os Apps Chrome e Extensões para receber notificações push, como criar notificações de configuração básica, obter e inicializar o SDK ou o plug-in e como registrar o seu dispositivo ou navegador para receber notificações push. Também é possível ativar seus aplicativos móveis e de navegador da web para receber notificações push usando a [API REST](t_restapi.html).

**Nota**: para registros de dispositivo, navegador, Apps Chrome e Extensões, o serviço {{site.data.keyword.mobilepushshort}} mantém uma referência exclusiva para tokens emitidos de provedores de notificação - APNs para Apple ou FCM para Google. Os tokens podem ser invalidados pelo provedor de notificação de serviço {{site.data.keyword.mobilepushshort}} por vários motivos. 

Por exemplo, durante a desinstalação de um app no dispositivo. Nesse cenário, quando a entrega de uma notificação for tentada com base na resposta dos provedores de que o dispositivo está invalidado, o serviço {{site.data.keyword.mobilepushshort}} removerá os registros do dispositivo ou do navegador da web. Isso, por sua vez, restringiria tentativas subsequentes de enviar a notificação a esses dispositivos invalidados.


## Ativando aplicativos Android para receber notificações push
{: #tag_based_notifications}


É possível ativar os aplicativos do Android para receber notificações push para os seus dispositivos. O Android Studio é um pré-requisito e é o método recomendado para construir projetos Android. É essencial um conhecimento básico do Android Studio.

### Instalando o Client Push SDK com Gradle
{: #android_install}

Esta seção descreve como instalar e usar o Client Push SDK para desenvolver ainda mais os aplicativos Android.

É possível incluir o {{site.data.keyword.Bluemix}} Mobile Services Push SDK usando o [Gradle ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}, que faz download automaticamente dos artefatos de repositórios e os disponibiliza para seu aplicativo Android. Assegure-se de configurar corretamente o [Android Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.android.com/tools/studio/index.html) e o Android Studio SDK. 

Depois de criar e abrir seu aplicativo móvel, conclua as etapas a seguir usando o Android Studio.

1. Inclua dependências em seu arquivo de nível Módulo **build.gradle**. 	

	- Inclua a dependência a seguir para incluir o SDK do cliente Push dos serviços do Bluemix™ Mobile e o SDK dos serviços do Google Play em suas dependências do escopo de compilação.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Inclua as dependências a seguir para importar instruções que são requeridas para os fragmentos de código.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Inclua a dependência a seguir no arquivo de nível Módulo **build.gradle** no final.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Inclua as dependências a seguir para o seu arquivo de nível Projeto **build.gradle**.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. No arquivo **AndroidManifest.xml**, inclua as permissões a seguir. Para visualizar um manifest de amostra, veja [Aplicativo de amostra helloPush Android ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. Para visualizar um arquivo Gradle de amostra, veja [Arquivo Gradle de construção de amostra ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
Saiba mais sobre as [permissões do Android ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} aqui.

4. Inclua as configurações de intento de notificação da atividade. Essa configuração inicia o aplicativo quando o usuário clica na notificação recebida da área de notificação.
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Nota**: substitua *Your_Android_Package_Name* na ação anterior pelo nome do pacote de aplicativos usado em seu aplicativo.

5. Inclua o serviço de intenção e os filtros de intenção do Firebase Cloud Messaging (FCM) ou do Google Cloud Messaging (GCM) para as notificações de eventos RECEIVE e REGISTRATION.
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    android:exported="true" >
    	<intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. O serviço {{site.data.keyword.mobilepushshort}} suporta a recuperação de notificações individuais a partir da bandeja de notificação. Para notificações acessadas a partir da bandeja de notificação, você receberá um identificador somente para a notificação que estiver sendo clicada. Todas as notificações são exibidas quando o aplicativo é aberto normalmente. Para usar essa funcionalidade, atualize o seu arquivo **AndroidManifest.xml** com o fragmento a seguir:

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

Assegure-se de que tenha passado por [Configurando credenciais para um provedor de notificação](t__main_push_config_provider.html) para configurar o projeto FCM e obter suas credenciais. Conclua as etapas a seguir usando o console do Firebase Cloud Messaging (FCM).

1. No console do Firebase, clique no ícone **Configurações de projeto**.
    ![Configurações de projeto do Firebase](images/FCM_4.jpg)

3. Selecione **INCLUIR APP** ou **Incluir Firebase em seu ícone de app Android** a partir da guia Geral no painel Seus apps.
    ![Incluindo Firebase no Android](images/FCM_5.jpg)

4. Na janela Incluir Firebase no seu app Android, inclua **com.ibm.mobilefirstplatform.clientsdk.android.push** como o Nome do pacote. O campo de apelido App é opcional. Clique em **INCLUIR APP**. 
    ![Incluindo o Firebase em sua janela do Android](images/FCM_1.jpg)

5. Inclua o nome do pacote do seu aplicativo inserindo o nome do pacote na janela Incluir Firebase no seu app Android. O campo de apelido App é opcional. Clique em **INCLUIR APP**. 

	![Incluindo o nome do pacote do seu aplicativo](images/FCM_2.jpg)

6. O arquivo `google-services.json` é gerado. Copie o arquivo `google-services.json` para o seu diretório-raiz do módulo do aplicativo Android. Observe que o arquivo `google-service.json` inclui os nomes de pacote adicionados.

    ![Incluindo o arquivo json no diretório-raiz do seu aplicativo](images/FCM_7.jpg)

5. Na janela Incluir Firebase no seu app Android, clique em **Continuar** e, em seguida, **Concluir**. 

  

Construa e execute o seu aplicativo.

### Inicializando os apps Push SDK for Android
{: #android_initialize}

Um local comum para colocar o código de inicialização está no método onCreate da atividade principal no aplicativo Android. Há dois componentes do SDK que precisam ser inicializados. Um é o SDK principal e o outro é o SDK push construído no SDK principal.

#### Inicializando o SDK principal
{: #initz_core_sdk}

```
// Initialize the SDK for Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

Especifica o local em que o app está hospedado. É possível usar um destes três valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### Inicializar o Push SDK do cliente
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

Esta é a chave AppGUID do serviço {{site.data.keyword.mobilepushshort}}. Esse valor faz distinção entre maiúsculas e minúsculas. Abra o painel Notificação push e selecione a guia Configurar. É possível obter esse valor em Opções móveis na guia configurar no painel de serviço Notificação push. 

### Registrando dispositivos Android
{: #android_register}

Use a API `MFPPush.register()` para registrar o dispositivo com o serviço {{site.data.keyword.mobilepushshort}}. Para se registrar para dispositivos Android, inclua as informações do Firebase Cloud Messaging (FCM) no painel de configuração do serviço {{site.data.keyword.mobilepushshort}} do Bluemix. Para obter mais informações, veja [Configurando credenciais para um provedor de notificação](t__main_push_config_provider.html). 

Copie os fragmentos de código a seguir para seu aplicativo móvel Android.

```
	//Register Android devices
push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//handle success here
    }
		@Override
	    public void onFailure(MFPPushException ex) {
    		//handle failure here
    }
		});
```
	{: codeblock}


```
	//Handles the notification when it arrives
MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
    public void onReceive (final MFPSimplePushNotification message){
// Handle Push Notification
    }
		};
```
	{: codeblock}

### Recebendo notificações push em dispositivos Android
{: #android_receive}

1. Para registrar o objeto notificationListener com o Push Notifications servive, use o método `MFPPush.listen()`. Este método é geralmente chamado a partir dos métodos `onResume()` e `onPause` da atividade que está manipulando as notificações push.
```
	@Override
protected void onResume(){
   super.onResume();
   if(push != null) {
       push.listen(notificationListener);
   }
	}
```
	{: codeblock}
```
	@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	}
```
	{: codeblock}

2. Compile o projeto e execute-o no dispositivo ou simulador. Quando o método onSuccess() para o listener de resposta no método register() for chamado, ele confirmará que o dispositivo foi registrado com sucesso no serviço {{site.data.keyword.mobilepushshort}} e será possível agora enviar uma notificação push.
3. Verifique se seus dispositivos receberam sua notificação. Se o aplicativo estiver em execução no primeiro plano, a notificação será manipulada por `MFPPushNotificationListener`. Se o aplicativo estiver em segundo plano, uma mensagem será exibida na barra de notificações.

### Monitorando notificações push em dispositivos Android
{: #android_monitor}

Para monitorar o status atual da notificação dentro do aplicativo, é possível implementar a interface `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` e definir o método onStatusChange(String messageId, MFPPushNotificationStatus status). 

O `messageId` é o identificador da mensagem enviada do servidor.  `MFPPushNotificationStatus` define o status das notificações como valores:

- RECEIVED - O app recebeu a notificação. 
- QUEUED - O app enfileira a notificação para chamar o listener de notificação. 
- OPENED - O usuário abre a notificação clicando na notificação na bandeja, ativando-a no ícone do app ou quando o app está em primeiro plano. 
- DISMISSED - O usuário limpa/descarta a notificação na bandeja.

É necessário registrar a classe `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` com MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


#### Atendendo ao status DISMISSED
{: #android_monitor_listen}

É possível optar por atender ao status DISMISSED em uma das seguintes condições:

- Quando o app está ativo (em execução em primeiro plano ou em segundo plano)

  Inclua o fragmento no seu arquivo `AndroidManifest.xml`:

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- Quando o app está ativo (em execução em primeiro plano ou em segundo plano) e não executando (encerrado)

Amplie o receptor de transmissão `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` e substitua o método `onReceive()`, em que o `MFPPushNotificationStatusListener` deve ser registrado antes de chamar o método `onReceive()` da classe base.

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
	@Override
public void onReceive(Context context, Intent intent) {
	MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
	// Handle status change
}
	});
super.onReceive(context, intent);
}
	}
```
    {: codeblock}


Inclua o fragmento a seguir no arquivo `AndroidManifest.xml`:

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

### Enviando notificações push básicas
{: #send-basic-notification}

Depois de ter desenvolvido seus aplicativos, será possível enviar notificações push básicas.

Para enviar notificações push básicas, conclua as etapas a seguir:

1. Selecione **Enviar notificações** e componha uma mensagem escolhendo uma opção **Enviar para**. As opções suportadas são **Dispositivo por tag**, **ID do dispositivo**, **ID do usuário**, **Dispositivos Android**, **Dispositivos iOS**, **Notificações da web** e **Todos os dispositivos**.
**Nota**: ao selecionar a opção **Todos os dispositivos**, todos os dispositivos inscritos para {{site.data.keyword.mobilepushshort}} receberão notificações.
![Tela de notificações](images/tag_notification.jpg)

2. No campo **Mensagem**, componha sua mensagem. Escolha a configurar das definições opcionais conforme necessário.
3. Clique em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

A captura de tela a seguir mostra uma caixa de alerta que manipula uma notificação push no primeiro plano em um dispositivo Android.

![Notificação push em primeiro plano no Android](images/Android_Screenshot.jpg)

A captura de tela a seguir mostra uma notificação push no plano de fundo para Android.

![Notificação push no plano de fundo no Android](images/background.jpg)

### Configurações opcionais do Android para envio de notificações
{: #send_otpional_setting}

É possível customizar ainda mais as configurações do {{site.data.keyword.mobilepushshort}} para enviar notificações a dispositivos Android. As opções de customização opcionais a seguir são suportadas:
![Configurações customizadas do Android](images/android_custom_settings.jpg)

- Chave de redução: as chaves de redução são anexadas às notificações. Se diversas notificações chegarem sequencialmente com a mesma chave de redução quando o dispositivo estiver off-line, elas serão reduzidas. Quando um dispositivo fica on-line, ele recebe notificações a partir do servidor FCM/GCM e exibe somente a notificação mais recente que comporta a mesma chave de redução. Se a chave de redução não estiver configurada, as mensagens novas e antigas serão armazenadas para entrega futura.
- Som: indica que um clique de som seja reproduzido no recebimento de uma notificação. Suporta o padrão ou o nome de um recurso de som empacotado no app.
- Ícone: especifique o nome do ícone a ser exibido para a notificação. Assegure-se de ter empacotado o ícone na pasta `res/drawable` com o aplicativo cliente.
- Prioridade: especifica as opções para designar prioridade de entrega às mensagens. Uma prioridade `high` ou `max` resultará em notificação direta, enquanto mensagens com prioridade `low` ou `default` não abririam conexões de rede em um dispositivo em suspensão. Para mensagens com a opção configurada como `min`, será uma notificação silenciosa.
- Visibilidade: é possível optar por configurar a opção de visibilidade de notificação como `public` ou `private`. A opção `private` restringe a visualização pública, e é possível optar por ativá-la se seu dispositivo é protegido com pin ou um padrão e a configuração de notificação está configurada como **Ocultar conteúdo de notificação confidencial**. Quando a visibilidade for configurada como `private`, um campo `redact` deverá ser mencionado. Somente o conteúdo especificado no campo `redact` será exibido em uma tela bloqueada segura no dispositivo. A escolha de `public` renderizaria as notificações para serem livremente lidas.
- Time to live: esse valor é configurado em segundos. Se esse parâmetro não for especificado, o servidor FCM/GCM armazenará a mensagem por quatro semanas e tentará entregar. A validade expira após quatro semanas. A faixa de valores possíveis vai de 0 a 2.419.200 segundos.
- Atrasar quando inativo: configurar esse valor como `true` instruirá o servidor FCM/GCM a não entregar a notificação se o dispositivo estiver inativo. Configure esse valor como `false` para assegurar a entrega de notificação mesmo que o dispositivo esteja inativo.
- Sincronizar: a configuração dessa opção como `true` sincroniza as notificações entre todos os dispositivos registrados. Se o usuário com um nome de usuário tiver diversos dispositivos com o mesmo aplicativo instalado, a leitura da notificação em um dispositivo assegura a exclusão das notificações nos outros dispositivos. É preciso assegurar-se de estar registrado no serviço {{site.data.keyword.mobilepushshort}} com userId para que essa opção funcione.
- Carga útil adicional: especifica os valores de carga útil customizados para suas notificações.


### Etapas Seguintes
{: #next_steps_tag_based_notifications}

Depois de configurar com êxito notificações básicas, é possível configurar notificações baseadas em tag e opções avançadas.

Inclua esses recursos do serviço de notificações push em seu aplicativo.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, veja [Ativando notificações push avançadas](t_advance_badge_sound_payload.html).


## Ativando aplicativos Cordova para receber notificações push
{: #cordova_enable}


Cordova é uma plataforma para criar aplicativos híbridos com JavaScript, CSS e HTML. O serviço {{site.data.keyword.mobilepushshort}} suporta o desenvolvimento de aplicativos iOS e Android baseados em Cordova.

É possível ativar aplicativos Cordova para receber notificações push para os seus dispositivos.

### Instalando o plug-in do push Cordova
{: #cordova_install}

Instale e use o plug-in de push do cliente para desenvolver ainda mais seus aplicativos Cordova. Isso também instala o plug-in núcleo do Cordova, que inicializa sua conexão com o Bluemix.

1. Faça download das versões mais recentes do Android Studio SDK e Xcode.
1. Configure o emulador. Para Android Studio, use um emulador que suporte a API do Google.
1. Instale a ferramenta de linha de comandos Git. Para Windows, certifique-se de selecionar a opção **Executar Git no prompt de comandos do Windows**. Para obter informações sobre como fazer download e instalar essa ferramenta, veja o [Git ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}.
1. Instale o Node.js e a ferramenta Node Package Manager (NPM). A ferramenta de linha de comandos NPM é empacotada com o Node.js. Para obter informações sobre como fazer download e instalar o Node.js, veja [Node.js ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/en/download/){: new_window}.
1. Na linha de comandos, instale as ferramentas de linha de comandos Cordova usando o comando **npm install -g cordova**. Isso é necessário para usar o plug-in de push Cordova. Para obter informações sobre como instalar o Cordova e configurar seu app Cordova, veja [Cordova Apache ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}. Para obter mais informações, veja o [Arquivo leia-me ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} do plug-in push Cordova.
1. Mude para a pasta na qual deseja criar seu app Cordova e execute o comando a seguir para criar um aplicativo Cordova. Se você tiver um app Cordova existente, vá para a etapa 3.
```cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- Opcional: é possível editar o arquivo **config.xml** e mudar o nome do aplicativo no elemento <name> para um nome de sua escolha, em vez do nome HelloCordova padrão.

Assegure-se de especificar o ID de pacote configurável correto. As mensagens de erro a seguir poderão resultar em Xcode, se um ID de pacote configurável incorreto for especificado.

* O executável foi assinado com autorizações inválidas.
* As autorizações especificadas no arquivo de autorizações de assinatura de código do aplicativo não correspondem às especificadas no seu perfil de fornecimento. Para corrigir esse problema, especifique o ID do pacote configurável correto no Xcode ou no arquivo **config.xml** do seu app Cordova.

1. Inclua a API mínima suportada ou a declaração de destino de implementação no arquivo config.xml do seu aplicativo Cordova. O valor minSdkVersion deve ser maior que 15. O valor targetSdkVersion deve sempre refletir o SDK mais recente do Android que esta disponível no Google.
	
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

### Inicializando o plug-in Cordova
{: #cordova_initialize}

Antes de poder usar o plug-in do Cordova do serviço {{site.data.keyword.mobilepushshort}}, é necessário inicializá-lo passando a rota do aplicativo e o GUID do aplicativo. Depois de inicializar o plug-in, é possível conectar-se ao app de servidor criado no painel do Bluemix. O plug-in Cordova é o wrapper dos SDKs de cliente Android e iOS para permitir que um app Cordova se comunique com serviços Bluemix.

1. Inicialize o BMSClient copiando e colando o fragmento de código a seguir no arquivo JavaScript principal (em geral, localizado no diretório **www/js**).

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


### Registrando Dispositivos
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

Inclua o seguinte fragmento de código Swift em sua classe de delegação de aplicativo.

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

### Etapas Seguintes
{: #cordova_register_next}

Compile seu projeto e, em seguida, execute-o usando os comandos a seguir:

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### Recebendo notificações push em dispositivos
{: #cordova_receive}

Copie o fragmento de código a seguir para receber notificações push em dispositivos.

#### JavaScript
{: #jvscrpt}

Inclua o seguinte fragmento de código JavaScript
na web part do seu aplicativo Cordova.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Propriedades de notificação do Android
{: #And_notif}

A seção a seguir lista as propriedades de notificação de Android:

* **message** - mensagem de notificação push
* **payload** - objeto JSON contendo uma carga útil de notificação


#### Propriedades de notificação do iOS
{: #ios_notif}

A seguinte seção lista as propriedades de notificação iOS:

* **message** - mensagem de notificação push
* **payload** - objeto JSON que contém uma carga útil de notificação action-loc-key - a sequência é usada como chave para obter uma sequência localizada no local atual, a ser usada para o título de botão apropriado, em vez de `Visualizar`.
* **badge** - o número a ser exibido como o badge do ícone de app. Se essa propriedade estiver ausente, o badge não será mudado. Para remover o badge, configure o valor dessa propriedade para 0.
* **sound** - o nome de um arquivo de som no pacote configurável de app ou na pasta Biblioteca/Sons do contêiner de dados de app.


Inclua os fragmentos de código Swift a seguir em sua classe de delegação de aplicativo.
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

### Enviando notificações push básicas
{: #push-send-notifications}

Depois de ter desenvolvido seus aplicativos, será possível enviar notificações push básicas.

Para enviar notificações push básicas, conclua as etapas:

1. Selecione **Enviar notificações** e componha uma mensagem escolhendo uma opção **Enviar para**. As opções suportadas são **Dispositivo por tag**, **ID do dispositivo**, **ID do usuário**, **Dispositivos Android**, **Dispositivos iOS**, **Notificações da web** e **Todos os dispositivos**.
**Nota**: ao selecionar a opção **Todos os dispositivos**, todos os dispositivos inscritos para {{site.data.keyword.mobilepushshort}} receberão notificações.
![Tela de notificações](images/tag_notification.jpg)

2. No campo **Mensagem**, componha sua mensagem. Escolha a configurar das definições opcionais conforme necessário.
3. Clique em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

A captura de tela a seguir mostra uma caixa de alerta que manipula um {{site.data.keyword.mobilepushshort}} no primeiro plano em dispositivos Android e iOS.

![Notificação push em primeiro plano no Android](images/Android_Screenshot.jpg)

![Notificação push em primeiro plano no iOS](images/iOS_Screenshot.jpg)

   A imagem a seguir mostra {{site.data.keyword.mobilepushshort}} no segundo plano para Android.
![Notificação push no plano de fundo no Android](images/background.jpg)

#### Etapas Seguintes
{: #next_steps_basic_notifications}

Depois de configurar com êxito notificações básicas, é possível configurar notificações baseadas em tag e opções avançadas.

Inclua os recursos do serviço {{site.data.keyword.mobilepushshort}} em seu app.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, veja [Ativando notificações push avançadas](t_advance_badge_sound_payload.html).


## Ativando aplicativos iOS para receber notificações push
{: #enable-push-ios-notifications}

É possível ativar aplicativos iOS para enviar {{site.data.keyword.mobilepushshort}} para os seus dispositivos.


### Instalando o CocoaPods
{: #enable-push-ios-notifications-install}

Para obter um projeto Xcode existente, é possível configurar o SDK do cliente de serviços móveis do Bluemix usando a ferramenta de gerenciamento de dependência CocoaPods. Uma alternativa é instalar o SDK manualmente.

Para visualizar o arquivo leia-me Push Swift, acesse o [Leia-me ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Instale o CocoaPods usando o comando a seguir em seu terminal Mac.
	```
		$ sudo gem install cocoapods
	```
	{: codeblock}
2. Insira o comando `pod init` no terminal para inicializar o CocoaPods. Assegure-se de executar o comando a partir do diretório no qual seu projeto Xcode está. O comando `pod init` cria um Podfile.  
3. No Podfile gerado, inclua as dependências necessárias de SDK. Copie o Podfile a seguir.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. A partir do terminal, acesse a sua pasta do projeto e instale as dependências com o comando `pod update`.

O comando instala as suas dependências e cria uma nova área de trabalho do Xcode.  
**Nota**: assegure-se de sempre abrir a nova área de trabalho do Xcode, em vez do arquivo de projeto do Xcode original:
```
  $ open App.xcworkspace
```
	{: codeblock}

A área de trabalho contém o projeto original e o projeto Pods que contém suas dependências. Para modificar a pasta de origem de serviços móveis do Bluemix, é possível localizá-la em seu projeto Pods, em `Pods/yourImportedSourceFolder`, por exemplo: `Pods/BMSPush`.

### Incluindo estruturas usando Carthage
{: #carthage}

Inclua estruturas em seu projeto usando o [Carthage ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Observe que Carthage em Xcode8 não é suportado.

1. Inclua as estruturas `BMSPush` em seu Cartfile:
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
	```
	{: codeblock}
2. Execute o comando `carthage update`. Quando a construção for concluída, arraste `BMSPush.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` até seu projeto Xcode.
3. Siga as instruções no site [Carthage ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} para concluir a integração.

### Configurando o SDK do iOS
{: #ios-sdk}

Configure o SDK iOS, inclua o código a seguir no arquivo **AppDelegate.swift** em seu aplicativo. Observe que isso também é registrado com o APNs.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### Usando estruturas importadas e pastas de origem
{: #using-imported-frameworks}

Referencie o SDK no código. Assegure-se de que os pré-requisitos a seguir sejam atendidos.

- iOS 8.0 ou superior	
- Xcode 7

Grave diretivas `#import` para os cabeçalhos relevantes, por exemplo:
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

Para o arquivo leia-me Push Swift, veja o [Leia-me ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Nota**: a atualização de seu projeto Pods usando os comandos `pod install` ou `pod update` do CocoaPods pode substituir as pastas de origem de serviços móveis do Bluemix. Para reter as versões customizadas dos arquivos originais, assegure-se de que sejam submetidas a backup antes de emitir um destes comandos.


### Configurações de Compilação
{: #build-settings}

Acesse **Xcode > Configurações de compilação > Opções de compilação e configure Ativar Bitcode** como **Não**.

**Atenção**: Desde o iOS 9, mudanças no recurso App Transport Security (ATS) podem afetar a maneira de manipular o processo de autenticação. As postagens do blog a seguir descrevem mais informações sobre as mudanças: [ATS e Bitcode no iOS 9 ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} e [Conecte seu app iOS 9 ao Bluemix hoje ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

### Inicializando apps Push SDK para iOS
{: #enable-push-ios-notifications-initialize}

Um local comum para colocar o código de inicialização é no aplicativo delegado do aplicativo iOS. Clique no link **Opções móveis** no Painel Push para obter a rota e o GUID do aplicativo.

#### Inicializando o SDK principal
{: #Initializing-the-core-sdk}

Para inicializar o Core SDK for Swift com o GUID, a rota e a região do IBM Bluemix, use o fragmento de código a seguir.
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### Rota, GUID e região do Bluemix
{: #route-guid-bluemix-region}


- **appRoute**: especifica a rota que é designada ao aplicativo do servidor que você criou no Bluemix.


- **GUID**: especifica a chave exclusiva que é designada ao aplicativo que você criou no Bluemix. Esse valor faz distinção entre maiúsculas e minúsculas.


- **bluemixRegionSuffix**: especifica o local em que o app está hospedado. O parâmetro `bluemixRegion` especifica qual implementação do Bluemix você está usando. É possível configurar esse valor com uma propriedade estática `BMSClient.REGION` e use um dos três valores:

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**: especifica a chave AppGUID exclusiva que é designada ao serviço {{site.data.keyword.mobilepushshort}} que você criou no Bluemix.

#### Inicializando o SDK de Push do cliente
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### Registrando aplicativos e dispositivos iOS
{: #enable-push-ios-notifications-register}

Um aplicativo deve se registrar com os APNs para receber notificações remotas, após a instalação em um dispositivo. Depois que o token de dispositivo gerado pelo APNs é recebido pelo app, ele deve ser passado de volta ao serviço {{site.data.keyword.mobilepushshort}}.

Para registrar aplicativos e dispositivos iOS, será necessário:

1. Criar um aplicativo backend.
2. Passar o token para o {{site.data.keyword.mobilepushshort}}.


#### Criar um aplicativo backend
{: #create-a-backend-app}

Crie um aplicativo backend no catálogo do Bluemix® da seção Modelos, que ligará automaticamente o serviço {{site.data.keyword.mobilepushshort}} a esse aplicativo. Se você já tiver criado um app backend, assegure-se de ligar o app ao serviço {{site.data.keyword.mobilepushshort}}.


#### Passando tokens para o Push Notifications
{: #pass-token-push-notifications}

Depois que o token for recebido do APNs, passe-o para {{site.data.keyword.mobilepushshort}} como parte do método `registerWithDeviceToken`.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
       else{
            print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
   }
  }
```
	{: codeblock}


### Recebendo notificações push em dispositivos iOS
{: #enable-push-ios-notifications-receiving}

Para receber notificações push em dispositivos iOS, inclua o método Swift a seguir na delegação de seu aplicativo.

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### Monitorando notificações push em dispositivos iOS
{: #ios-monitoring}


É possível monitorar a contagem e o status atual das notificações push que foram enviadas. Para ativar o monitoramento, inclua um dos métodos Swift a seguir na delegação de aplicativo do aplicativo baseado no evento.



- Enviar o status de notificação quando o app estiver aberto, clicando na notificação.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
				let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- Enviar o status de notificação quando o app estiver no modo de plano de fundo.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
	 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
	 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### Enviando notificações push básicas
{: #send}

Depois de ter desenvolvido seus aplicativos, será possível enviar notificações push básicas.

Para enviar notificações push básicas, conclua as etapas:

1. Selecione **Enviar notificações** e componha uma mensagem escolhendo uma opção **Enviar para**. As opções suportadas são **Dispositivo por tag**, **ID do dispositivo**, **ID do usuário**, **Dispositivos Android**, **Dispositivos iOS**, **Notificações da web** e **Todos os dispositivos**.  
**Nota**: ao selecionar a opção **Todos os dispositivos**, todos os dispositivos inscritos para {{site.data.keyword.mobilepushshort}} receberão notificações.
![Tela de notificações](images/tag_notification.jpg)

2. No campo **Mensagem**, componha sua mensagem. Escolha a configurar das definições opcionais conforme necessário.
3. Clique em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

A imagem a seguir mostra uma caixa de alerta manipulando um {{site.data.keyword.mobilepushshort}} e um dispositivo iOS.

![Notificação push em primeiro plano no iOS](images/iOS_Screenshot.jpg) 

#### Configurações opcionais para enviar notificações
{: #send_ios_otpional_setting}

É possível customizar ainda mais as configurações do {{site.data.keyword.mobilepushshort}} para enviar notificações a dispositivos iOS. As opções de customização opcionais a seguir são suportadas.

- **Badge**: indica o número que é exibido no badge do aplicativo. O valor padrão é zero (0) e isso não exibiria um badge. 
- **Som**: indica que um clique de som seja reproduzido no recebimento de uma notificação. Suporta o padrão ou o nome de um recurso de som empacotado no app.
- **Carga útil adicional**: especifica os valores de carga útil customizados para suas notificações.

### Ativando notificações interativas
{: #enb_snd_ios_otpional}

Agora, é possível enriquecer suas notificações de iOS com mais detalhes, como incluir uma imagem, um mapa ou um botão de resposta ativando notificações interativas. Isso fornece mais contexto aos clientes, além da capacidade de executar ação imediata sem sair do contexto atual.  

Para ativar as notificações interativas, use o código:



- Para definir a ação do botão
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
	```
		{: codeblock}


- Para definir a categoria dos botões
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- Para atualizar o registro para incluir botões
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

Para enviar uma notificação interativa, conclua estas etapas:

1. Na seção Editar, para a lista suspensa Enviar para, selecione **Dispositivos iOS**.
2. Insira a mensagem de notificação que talvez queira enviar.
3. Na seção Configurações opcionais, selecione **Móvel** e clique em
**iOS**.
4. Na lista suspensa Tipo, selecione **Combinado**.
5. No campo Categoria, especifique o tipo de notificação que você definiu em seu app. 

![Notificação interativa para iOS](images/push_ios_notification_interactive.jpg) 

#### Etapas Seguintes
{: #next_steps_02}

Depois de configurar com êxito notificações básicas, é possível configurar notificações baseadas em tag e opções avançadas.

Inclua esses recursos do Serviço de notificações push em seu app.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, veja [Ativando notificações push avançadas](t_advance_badge_sound_payload.html).
