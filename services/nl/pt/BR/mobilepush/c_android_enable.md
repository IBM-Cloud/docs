---

copyright:
 years: 2015 2016

---


# Ativando aplicativos Android para receber notificações push
{: #tag_based_notifications}


Ative aplicativos Android para receber notificações push e enviar notificações push para seus dispositivos.

## Instalando o Client Push SDK com Gradle
{: #android_install}

Esta seção descreve como instalar e usar o Client Push SDK para desenvolver ainda mais
os aplicativos Android.

Os serviços Push SDK móveis do Bluemix® podem ser incluídos usando Gradle. O Gradle
faz download automaticamente dos artefatos de repositórios e os disponibiliza para seu
aplicativo Android. Certifique-se de configurar corretamente o Android Studio e o Android
Studio SDK. Para obter mais informações sobre como configurar o sistema, consulte [Visão geral do Android Studio](https://developer.android.com/tools/studio/index.html). Para
obter informações sobre o Gradle, consulte
[Configurando
compilações do Gradle](http://developer.android.com/tools/building/configuring-gradle.html).

1. No Android Studio, depois de criar e abrir seu aplicativo móvel, abra o arquivo
**build.gradle** do aplicativo. Em seguida, inclua as dependências
a seguir no aplicativo móvel. Essas instruções de importação são
requeridas para os fragmentos de código:

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Inclua as seguintes dependências em seu aplicativo móvel. As linhas a seguir
incluem o SDK do cliente Push do Bluemix™ Mobile Services e o SDK de serviços do Google
play nas dependências do escopo de compilação.

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. No arquivo **AndroidManifest.xml**, inclua as
permissões a seguir. Para visualizar um manifest de amostra, consulte
[Aplicativo
de amostra Android helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Para visualizar um arquivo Gradle de amostra, consulte
[Arquivo
de amostra Build Gradle](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

	```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="com.ibm.clientsdk.android.app.permission.C2D_MESSAGE" />
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
	<uses-permission android:name="android.permission.WAKE_LOCK" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	```

	É possível ler mais sobre as
[permissões
do Android](http://developer.android.com/guide/topics/security/permissions.html) aqui.

1. Inclua as configurações de intento de notificação da atividade. Essa configuração inicia o
aplicativo quando o usuário clica na notificação recebida da área de notificação.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Nota**: Substitua *Your_Android_Package_Name* na ação
acima pelo nome do pacote de aplicativos usado em seu aplicativo.

1. Inclua o serviço de intento Google Cloud Messaging (GCM) e os filtros de intento das
notificações de evento RECEIVE.

	```
	service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />

	<receiver
	    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.internal.MFPPushBroadcastReceiver"
	    android:permission="com.google.android.c2dm.permission.SEND">
	    <intent-filter>
	        <action android:name="com.google.android.c2dm.intent.RECEIVE" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	</receiver>
	```


## Inicializando os apps Push SDK for Android
{: #android_initialize}

Um local comum para colocar o código de inicialização está no método onCreate da atividade principal no aplicativo Android.

Clique no link **Opções móveis** no Painel do Aplicativo Bluemix
para obter a rota do aplicativo e o GUID do aplicativo. Use esses valores para a rota e o
GUID do App. Modifique o fragmento de código para usar os parâmetros appRoute e appGUID
do app Bluemix.


###Inicializar o SDK principal

```
// Inicialize o SDK for Java (Android) com o GUID do app IBM Bluemix e roteie
BMSClient.getInstance().initialize(getApplicationContext(), em que "applicationRoute","applicationGUID", bluemixRegion:"Local e seu app é hospedado");
```


**appRoute**

Especifica a rota que é designada ao aplicativo do servidor que você criou no
Bluemix.

**AppGUID**

Especifica a chave exclusiva que é designada ao aplicativo que você criou no
Bluemix. Esse valor faz
distinção entre maiúsculas e minúsculas.

**bluemixRegionSuffix**

Especifica o local em que o app está hospedado. Você pode usar um de três valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###Inicializar o Push SDK do cliente

```
//Inicialize o Push SDK for Java do cliente
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```

## Registrando dispositivos Android
{: #android_register}

Use a API ```IMFPush.register()``` para registrar o dispositivo com um Serviço de notificação push. Para o registro de dispositivos Android, primeiro
inclua as informações do Google Cloud Messaging (GCM) no painel de configuração de serviço de push do Bluemix. Para obter mais informações,
consulte [Configurando credenciais para o Google Cloud Messaging](t_push_provider_android.html).

Copie e cole os seguintes fragmentos de códigos em seu
aplicativo móvel Android.

```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //handle success here
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //handle failure here
	    }
	});
```

```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```


## Recebendo notificações push em dispositivos Android
{: #android_receive}

Para registrar o objeto notificationListener com Push, chame o método
**MFPPush.listen()**. Esse método é chamado geralmente a partir do
método** onResume() **da atividade que está
manipulando as notificações push.

1. Para registrar o objeto notificationListener com Push, chame o método
**listen()**. Esse método é chamado geralmente a partir do
método** onResume() **da atividade que está
manipulando as notificações push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Compile o projeto e execute-o no dispositivo ou simulador. Quando o método
onSuccess() para o listener de resposta no método register() é chamado, ele confirma se o
dispositivo foi registrado com sucesso no Serviço de notificação push. Nesse momento, é
possível enviar uma mensagem conforme descrito em Enviando notificações push básicas.
3. Verifique se seus dispositivos receberam sua notificação. Se o
aplicativo estiver em execução no primeiro plano, a notificação será
manipulada por **MFPPushNotificationListener**. Se o aplicativo estiver em segundo plano, uma mensagem será exibida na barra de notificações.


## Enviando notificações push básicas
{: #send}

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
