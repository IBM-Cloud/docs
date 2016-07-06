---

copyright:
  years: 2015, 2016

---

# Instalando o {{site.data.keyword.mobileanalytics_short}}
SDKs Clientes
{: #mobileanalytics_sdk}
*Última atualização: 21 de abril de 2016*
{: .last-updated}

Os SDKs do cliente do {{site.data.keyword.mobileanalytics_short}}
estão atualmente disponíveis para Android, iOS e WatchOS.
{: #shortdesc}

## Instalando o SDK do cliente Android
{: #install-sdk-android}

O {{site.data.keyword.mobileanalytics_short}} Client SDK é distribuído com o Gradle, um gerenciador de dependências para projetos Android. O Gradle faz download automaticamente dos artefatos de repositórios e os disponibiliza em seu aplicativo Android.

1. Crie um projeto [Android Studio](http://developer.android.com/sdk/index.html) ou abra um projeto existente.

2. Abra o arquivo `build.gradle` que está em seu módulo aplicativo.

  **Dica**: seu projeto Android pode ter dois arquivos `build.gradle`: um para o projeto e um para o módulo aplicativo. Certifique-se de usar o arquivo de **módulo aplicativo**.

3. Localize a seção `Dependências` do arquivo `build.gradle` e inclua uma dependência de compilação para o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}, conforme a seguir:

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  Sua instrução de repositórios deve ser semelhante ao exemplo de código a seguir:

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. Sincronize seu projeto com Gradle clicando em **Ferramentas &gt; Android &gt; Projeto de sincronização com arquivos Gradle**.

5. Abra o arquivo `AndroidManifest.xml` para seu projeto Android e inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Instalando o SDK do Swift
{: #installing-sdk-ios}

O SDK do {{site.data.keyword.mobileanalytics_full}} permite instrumentar seu aplicativo móvel. O SDK do Swift está disponível para iOS e watchOS.

### Antes de Começar
{: #before-you-begin-ios}

Assegure-se de ter configurado corretamente o Xcode. Para saber como configurar o ambiente de desenvolvimento do iOS, veja o [website Apple Developer](https://developer.apple.com/support/xcode/).

O SDK do {{site.data.keyword.mobileanalytics_short}} é distribuído com [Cocoapods](https://cocoapods.org/) e [Carthage](https://github.com/Carthage/Carthage#getting-started), que são gerenciadores de dependência para projetos Cocoa. O CocoaPods e o Carthage fazem download automaticamente de artefatos de repositório e os disponibilizam para seu aplicativo.

#### Cocoapods
{: #cocoapods}
1. Se o CocoaPods não estiver instalado, execute:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. Se você ainda não inicializou sua área de trabalho para o CocoaPods, execute o comando `pod init` no diretório-raiz de seu projeto. O CocoaPods cria um arquivo `Podfile`, que é onde você define as dependências para seu projeto Xcode.

3. Inclua o pod `BMSAnalytics` no destino em seu Podfile, por exemplo:

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. Salve o arquivo `Podfile` e execute `pod install` a partir da linha de comandos.

5. Abra sua área de trabalho do projeto Xcode usando o arquivo `.xcworkspace` que foi gerado pelo CocoaPods.

#### Carthage
{: #carthage}

Inclua estruturas em seu projeto usando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Inclua estruturas `BMSAnalytics` no Cartfile:
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. Execute o comando `carthage update`. Quando a construção for concluída, arraste `BMSAnalytics.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` para seu projeto Xcode.
3. Siga as instruções no site [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) para concluir a integração.

# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
