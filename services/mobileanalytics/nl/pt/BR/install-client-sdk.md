---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instalando os SDKs do cliente do {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Os SDKs do cliente {{site.data.keyword.mobileanalytics_short}} estão atualmente disponíveis para Android, iOS, WatchOS e Cordova.
{: shortdesc}

## Instalando o SDK do cliente Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

O {{site.data.keyword.mobileanalytics_short}} Client SDK é distribuído com o Gradle, um gerenciador de dependências para projetos Android. O Gradle faz download automaticamente dos artefatos de repositórios e os disponibiliza em seu aplicativo Android.

1. Crie um projeto [Android Studio![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://developer.android.com/sdk/index.html){: new_window} ou abra um projeto existente.

2. Abra o arquivo `build.gradle` que está em seu **módulo de aplicativo**.

  **Dica**: o seu projeto do Android pode ter dois arquivos `build.gradle`: um para o projeto e um para o módulo de aplicativo. Certifique-se de usar o arquivo de **módulo de aplicativo**.

3. Localize a seção `Dependencies` do arquivo `build.gradle` e inclua uma dependência de compilação para o SDK do cliente {{site.data.keyword.mobileanalytics_short}}. Sua instrução de repositórios deve ser semelhante ao exemplo de código a seguir:

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  	```
  	{: codeblock}

4. Sincronize seu projeto com Gradle clicando em **Ferramentas &gt; Android &gt; Projeto de sincronização com arquivos Gradle**.

5. Abra o arquivo `AndroidManifest.xml` para seu projeto Android. É possível localizar esse arquivo em **app > manifests**. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Agora você instalou o SDK do cliente Android. Em seguida, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.   

## Instalando o SDK do Swift
{: #installing-sdk-ios}

![Compatível com CocoaPods](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

O SDK do {{site.data.keyword.mobileanalytics_full}} permite instrumentar seu aplicativo móvel. O SDK do Swift está disponível para iOS e watchOS.

### Antes de Começar
{: #before-you-begin-ios notoc}

Assegure-se de ter configurado corretamente o Xcode. Para aprender a configurar seu ambiente de desenvolvimento iOS, consulte o [website do Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/support/xcode/){: new_window}. Leia sobre os [Requisitos do Xcode![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements){: new_window} para Client SDK Swift Analytics.

O SDK do {{site.data.keyword.mobileanalytics_short}} é distribuído com [CocoaPods ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cocoapods.org/){: new_window} e [Carthage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage#getting-started){: new_window}, que são gerenciadores de dependência para projetos Cocoa. O CocoaPods e o Carthage fazem download automaticamente de artefatos de repositório e os disponibilizam para seu aplicativo. Selecione CocoaPods ou Carthage:

#### CocoaPods
{: #cocoapods notoc}

1. Siga as [Instruções do SDK do {{site.data.keyword.Bluemix_notm}} Mobile Services Swift![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods){: new_window} no GitHub para instalar o `BMSAnalytics` usando o Cocoapods e inclua-o em seu Arquivo pod. 

	
2. Depois de ter instalado o SDK do cliente iOS, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.   

#### Carthage
{: #carthage notoc}

Se você não estiver usando o CocoaPods, será possível incluir estruturas em seu projeto usando [Carthage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}.

1. Siga as [instruções de instalação do Carthage![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage){: new_window} no
GitHub para instalar o `BMSAnalytics`.

2. Depois de ter instalado o SDK do cliente iOS, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.

## Instalando o plugin do Cordova
{: #installing-sdk-cordova}

O plug-in Cordova do {{site.data.keyword.mobileanalytics_full}} permite que você instrumente seu aplicativo móvel. 

1. Crie um projeto [Cordova ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://cordova.apache.org/#getstarted){: new_window} ou abra um projeto existente.

2. Inclua as plataformas Android e iOS em seu aplicativo Cordova. Execute um ou ambos os comandos a seguir da linha de comandos. Atualmente, a CLI Cordova V6.3.0 ou anterior é suportada:
   
   Android:

	 ```
	 cordova platform add android@5.2.2
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Se você incluiu a plataforma Android, deve-se incluir o nível mínimo de API suportado no arquivo `config.xml` do aplicativo Cordova. Abra o arquivo `config.xml` e inclua a linha a seguir no elemento `<platform name="android">`:

	```
	<platform name="android">  
  	 <preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	 <!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 O valor *minSdkVersion* deve ser da versão `15` ou superior. Consulte o [Android Platform Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} para se
manter atualizado com o *targetSdkVersion* suportado para o SDK do Android.

4. Se você incluiu o sistema operacional iOS, atualize o elemento `<platform name="ios">` com uma declaração de destino:

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. Inclua o plug-in `bms-core`.
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. Verifique se o plug-in foi instalado com êxito executando o comando a seguir:
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Configure seu ambiente Android e iOS![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.npmjs.com/package/bms-core#4-configuring-your-platform){: new_window}.

8. Agora você instalou o plug-in do Cordova e configurou seus ambientes. Em seguida, [importe e inicialize](sdk.html#initalize-ma-sdk) o SDK do cliente Analytics.

# Links Relacionados
{: #rellinks notoc}

## SDK
{: #sdk notoc}
* [SDK do Android![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK do iOS![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [SDK do Cordova Plugin Core![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.npmjs.com/package/bms-core){: new_window}

## Referência da API
{: #api notoc}
* [API de REST![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
