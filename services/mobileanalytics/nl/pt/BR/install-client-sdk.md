---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

# Instalando os SDKs do cliente {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Os SDKs do cliente {{site.data.keyword.mobileanalytics_short}} estão atualmente disponíveis para Android, iOS, WatchOS e Cordova.
{: #shortdesc}

## Instalando o SDK do cliente Android 
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

O SDK do cliente {{site.data.keyword.mobileanalytics_short}} é distribuído com o Gradle, um gerenciador de dependências para projetos Android. O Gradle faz download automaticamente dos artefatos de repositórios e os disponibiliza em seu aplicativo Android.

1. Crie um projeto [Android Studio](http://developer.android.com/sdk/index.html) ou abra um projeto existente.

2. Abra o arquivo `build.gradle` que está em seu **módulo de aplicativo**.

  **Dica**: o seu projeto do Android pode ter dois arquivos `build.gradle`: um para o projeto e um para o módulo de
aplicativo. Certifique-se de usar o arquivo de **módulo de aplicativo**.

3. Localize a seção `Dependencies` do arquivo `build.gradle`
e inclua uma dependência de compilação para o SDK do cliente
{{site.data.keyword.mobileanalytics_short}}. Sua instrução de repositórios deve ser semelhante ao exemplo de código a seguir:

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. Sincronize seu projeto com Gradle clicando em **Ferramentas &gt; Android &gt; Projeto de sincronização com arquivos Gradle**.

5. Abra o arquivo `AndroidManifest.xml` para seu projeto Android. É possível localizar esse arquivo em **app > manifests**. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Agora você instalou o SDK do cliente Android. Em seguida, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.   

## Instalando o SDK do Swift
{: #installing-sdk-ios}

![Compatível com CocoaPods](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

O SDK do {{site.data.keyword.mobileanalytics_full}} permite instrumentar seu aplicativo móvel. O SDK do Swift está disponível para iOS e watchOS.

### Antes de Começar
{: #before-you-begin-ios}

Assegure-se de ter configurado corretamente o Xcode. Para saber como configurar o ambiente de desenvolvimento do iOS, veja o [website Apple Developer](https://developer.apple.com/support/xcode/). Leia sobre os [Requisitos do Xcode](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)
para Analytics do Swift de SDK do cliente.

O SDK do {{site.data.keyword.mobileanalytics_short}} é distribuído com [CocoaPods](https://cocoapods.org/) e
[Carthage](https://github.com/Carthage/Carthage#getting-started), que são gerenciadores de dependência para projetos do Cocoa. O CocoaPods e o Carthage fazem download automaticamente de artefatos de repositório e os disponibilizam para seu aplicativo. 
Selecione CocoaPods ou Carthage:

#### CocoaPods
{: #cocoapods}

1. Siga as
[instruções do SDK do {{site.data.keyword.Bluemix_notm}} Mobile Services Swift](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) no
GitHub para instalar o `BMSAnalytics` usando o Cocoapods e incluí-lo no Podfile. 
	
2. Depois de ter instalado o SDK do cliente iOS, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.   

#### Carthage
{: #carthage}

Se você não estiver usando o CocoaPods, será possível incluir estruturas em seu projeto
usando o [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Siga as
[instruções
de instalação do Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) no GitHub para instalar o
`BMSAnalytics`.

2. Depois de ter instalado o SDK do cliente iOS, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.

## Instalando o plugin do Cordova
{: #installing-sdk-cordova}

O <!--SDK--> do plug-in do {{site.data.keyword.mobileanalytics_full}}
Cordova permite instrumentar seu
aplicativo móvel. 

1. Inclua as plataformas Android e iOS em seu aplicativo Cordova. Execute um ou ambos os comandos a seguir a partir da linha de comandos:

	```Bash
	cordova platform add android
	```
	
	```Bash
	cordova platform add ios
	```
	
2. Se você incluiu a plataforma Android, deve-se incluir o nível mínimo de API suportado no arquivo `config.xml` do aplicativo Cordova. Abra o arquivo `config.xml` e inclua a linha a seguir no elemento `<platform name="android">`:

	```XML
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  </platform>
```
O valor *minSdkVersion* deve ser maior que `15`. 
Consulte o
[Guia da plataforma Android](https://cordova.apache.org/docs/en/latest/guide/platforms/android/) para se manter atualizado com a
*targetSdkVersion* suportada para o SDK do Android.
3. Se você incluiu o sistema operacional iOS, atualize o elemento `<platform name="ios">` com uma declaração de destino:

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  </platform>
```

4. Instale o plug-in do
{{site.data.keyword.mobileanalytics_short}} Cordova:

 	```Bash
	cordova plugin add bms-core
	```

5. Verifique se o plug-in foi instalado com êxito executando o comando a seguir:
	```Bash
	cordova plugin list
	```
	
6. Agora você instalou o plug-in do Cordova. Em seguida, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.

# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [SDK do plug-in do
Cordova Core](https://www.npmjs.com/package/bms-core){: new_window}

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
