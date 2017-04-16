---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} SDKs, amostras e referência de API


Para incluir {{site.data.keyword.amafull}} SDKs
para seu cliente aplicativo, escolha os SDKs que você deseja
usar. Em seguida, configure seu
gerenciador de dependência para puxar os SDKs em seu aplicativo.
{:shortdesc}

**Nota:** seções subsequentes fornecem informações adicionais sobre instalar os SDKs.

## Core SDK
{: #coresdk}

O Core SDK inclui APIs para ativar a autenticação
customizada e criação de log.

### Android
{: #coresdk-android}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Ícone de link externo"){: new_window}

#### Instale o Core SDK com o Gradle
{: #coresdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security "Ícone de link externo"){: new_window}

#### Instale o Core SDK com o CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edite o Podfile e inclua a linha a seguir nos destinos necessários e execute:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[Repositório GitHub e referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Ícone de link externo"){: new_window}

#### Instale o Core SDK com o Cordova CLI
{: #coresdk-cordova-cli}

Instale o plug-in do Mobile Client Access Cordova:
```Bash
cordova plugin add bms-core
```
{: codeblock}

## SDK do cliente para autenticação de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication "Ícone de link externo"){: new_window},


#### Instale o Facebook SDK com o Gradle
{: #facebooksdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication "Ícone de link externo"){: new_window}

#### Instale o Facebook SDK com o CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edite o Perfil e inclua o seguinte nos destinos necessários e execute:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[Repositório GitHub e referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Ícone de link externo"){: new_window}

#### Instale o Facebook SDK com o Cordova CLI
{: #facebooksdk-cordova-cli}

Instale o plug-in Cordova:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK do cliente para autenticação do Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication "Ícone de link externo"){: new_window},



#### Instale o Google+ SDK com o Gradle
{: #googlesdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication "Ícone de link externo"){: new_window}

#### Instale o Google+ SDK com o CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edite o Perfil e inclua o seguinte e execute:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[Repositório GitHub e referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Ícone de link externo"){: new_window}

#### Instale o Google+ SDK com o Cordova CLI
{: #googlesdk-cordova-cli}

Instale o plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server SDK para servidores Node.js
{: #serversdk}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy "Ícone de link externo"){: new_window}

#### Instalar o server SDK com o npm
{: #serversdk-npm}

Execute NPM para instalar o SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Server SDK para servidor Liberty for Java&trade;
{: #serverlibertysdk}

[Fazer download de artefatos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

#### Instale o Liberty SDK
{: #libertysdk}

1. Copie o arquivo `com.ibm.worklight.oauth.tai_1.0.0.jar` no diretório
`$<wlp.user.dir>/extensions/lib`.

  **Dica:** `$<wlp.user.dir>` é o diretório do usuário do tempo de execução do Liberty for Java. O nome do diretório padrão é `usr`.

1. Copie o diretório `OAuthTai-1.0.mf` para o diretório `$<wlp.user.dir>/extension/lib/features`.


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[Repositório GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk "Ícone de link externo"){: new_window}

#### Instale o OAuth SDK com o npm
{: #oauthsdk}

Execute NPM para instalar o SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Amostras do provedor de identidade customizado
{: #customidprovider}

[Repositório GitHub de amostra simples ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Ícone de link externo"){: new_window}

[Repositório GitHub de amostra avançado ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Ícone de link externo"){: new_window}


