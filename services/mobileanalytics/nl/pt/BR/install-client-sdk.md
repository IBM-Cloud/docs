---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# Instalando os SDKs do cliente do {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Última atualização: 18 de outubro de 2016
{: .last-updated}

Os SDKs do cliente {{site.data.keyword.mobileanalytics_short}}
estão atualmente disponíveis para Android, iOS e WatchOS.
{: #shortdesc}

## Instalando o SDK do cliente Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

O {{site.data.keyword.mobileanalytics_short}} Client SDK é distribuído com o Gradle, um gerenciador de dependências para projetos Android. O Gradle faz download automaticamente dos artefatos de repositórios e os disponibiliza em seu aplicativo Android.

1. Crie um projeto [Android Studio](http://developer.android.com/sdk/index.html) ou abra um projeto existente.

2. Abra o arquivo `build.gradle` que está em seu **módulo de aplicativo**.

  **Dica**: o seu projeto do Android pode ter dois arquivos `build.gradle`: um para o projeto e um para o módulo de
aplicativo. Certifique-se de usar o arquivo de **módulo de aplicativo**.

3. Localize a seção `Dependencies` do arquivo `build.gradle` e inclua uma dependência de compilação para o SDK do cliente
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
6. Agora você instalou o SDK do cliente Android. Em seguida, [Importe e inicialize](sdk.html#initalize-ma-sdk-android) o SDK do cliente
Analytics.   

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

#### CocoaPods
{: #cocoapods}

1. Se o CocoaPods não estiver instalado, execute:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Para Xcode 8: `sudo gem install cocoapods --pre`
    
   Certifique-se de ter a versão mais recente de `BMSAnalytics` atualizando o seu repositório local do CocoaPods, como segue:
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Siga as [{{site.data.keyword.Bluemix_notm}}
Instruções do SDK do Swift do Mobile Services](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) no GitHub.
	
3. Após você ter instalado o SDK do cliente iOS, [Importe e inicialize](sdk.html#init-ma-sdk-ios) o SDK do cliente Analytics.   

#### Carthage
{: #carthage}

Inclua estruturas em seu projeto usando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Siga as [Instruções de instalação
do Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) no GitHub.

2. Após você ter instalado o SDK do cliente iOS, [Importe e inicialize](sdk.html#init-ma-sdk-ios) o SDK do cliente Analytics.

# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
