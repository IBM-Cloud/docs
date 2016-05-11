---

copyright:
 years: 2015, 2016

---

# Instalando o Client Push SDK com Gradle
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
a seguir no aplicativo móvel. Essas instruções de importação são necessárias para os
fragmentos de código que são listados abaixo.

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
