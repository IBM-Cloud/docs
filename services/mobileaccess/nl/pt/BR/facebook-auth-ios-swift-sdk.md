---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Ativando a autenticação do Facebook para apps iOS (Swift SDK)
{: #facebook-auth-ios}

Para usar o Facebook como um provedor de identidade em seus aplicativos {{site.data.keyword.amafull}} iOS, inclua e configure a Plataforma iOS para seu aplicativo Facebook.
{: shortdesc}

## Antes de iniciar
{: #before-you-begin}

Você deve ter

* Uma instância de um serviço
{{site.data.keyword.amafull}} e um aplicativo
{{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos
seguintes: `US South`, `United Kingdom` ou `Sydney`, e corresponder aos
valores de SDK requeridos no código Swift SDK:
`BMSClient.Region.usSouth`,
`BMSClient.Region.unitedKingdom` ou
`BMSClient.Region.sydney`. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.
* Um projeto do iOS configurado para funcionar com o CocoaPods.  Para obter mais informações,
veja **Instalar o CocoaPods** em [Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html).  
   **Nota:** não é necessário instalar o {{site.data.keyword.amashort}} client SDK principal antes de continuar.
* Um aplicativo Facebook no website [Facebook for Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developers.facebook.com "Ícone de link externo"){: new_window}.

**Importante:** não é necessário instalar separadamente o Facebook SDK (`com.facebook.FacebookSdk`). O Facebook SDK é instalado automaticamente com o pod {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. É possível ignorar a etapa **Incluir o Facebook SDK em seu projeto do Xcode** ao incluir ou configurar seu app no website Facebook for Developers.

## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}

No site Facebook for Developers:

1. Efetue login em sua conta no  [Facebook for Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developers.facebook.com "Ícone de link externo"){: new_window}.

1. Assegure-se de que a plataforma iOS tenha sido incluída em seu app. Ao incluir ou
configurar a plataforma iOS, será necessário fornecer o **bundleId** do
seu aplicativo iOS. Para
localizar o **bundleId** de seu aplicativo
iOS, procure o **Identificador de pacote
configurável** no arquivo
`info.plist` ou na guia
**Geral** do projeto Xcode.

  **Dica**: considere a ativação do sufixo de esquema URL ou a Conexão única se estiver planejamento usar esses recursos.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-ios-configmca}

Depois de configurar o ID do app Facebook e seu aplicativo
Facebook para atender clientes iOS, é possível ativar a
autenticação do Facebook no seu serviço
{{site.data.keyword.amashort}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Facebook**.
1. Inclua o **ID do aplicativo Facebook** e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} client SDK para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #install-cocoapods}

1. Abra o Terminal e execute o comando **pod --version**. Se o CocoaPods estiver instalado, o número da versão será exibido. É possível pular para a próxima seção para instalar o SDK.

1. Se você não tiver o CocoaPods instalado, execute:

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

Para obter mais informações, veja o [website CocoaPods ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cocoapods.org/ "Ícone de link externo"){: new_window}.

### Instalando o {{site.data.keyword.amashort}} client Swift SDK com o CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se você não tiver nenhum `Podfile` em seu projeto do iOS, execute `pod init` para criar o arquivo.

1. Edite o `Podfile` e inclua as linhas a seguir:

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Nota:** se você tiver esta linha em seu arquivo pod: `pod 'BMSSecurity'`, ela deverá ser removida. O pod `BMSFacebookAuthentication` instala todas as estruturas necessárias.

   **Dica:** é possível incluir `use_frameworks!` em seu destino Xcode em vez de tê-lo no Podfile.

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos.

   **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Ativar Compartilhamento Keychain para iOS
{: #enable_keychain}

Ative `Compartilhamento Keychain`. Acesse
a guia `Recursos` e mude
`Compartilhamento Keychain` para
`On` em seu projeto Xcode.

### Configurando seu projeto do iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto Xcode.

1. Configure a integração do Facebook incluindo as propriedades a seguir em seu arquivo `info.plist`:

   ![image](images/ios-facebook-infoplist-settings.png)

   Atualize o esquema URL e as propriedades FacebookAppID com seu ID do aplicativo Facebook.

   Também é possível atualizar o arquivo `info.plist` clicando com o botão direito no arquivo, selecionando **Abrir como > Código-fonte** e incluindo o XML a seguir:

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>                
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Atualize as propriedades `CFBundleURLSchemes` e
`FacebookappID` com seu ID do aplicativo Facebook. Atualize o
`FacebookDisplayName` com o nome do seu aplicativo Facebook.

   **Importante**: assegure-se de não substituir quaisquer propriedades existentes no arquivo `info.plist`. Se você tiver propriedades de sobreposição, deverá mesclá-las manualmente. Para obter mais informações, veja [Configurar o Projeto Xcode![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developers.facebook.com/docs/ios/getting-started/ "Ícone de link externo"){: new_window} e [Preparando seus apps para o iOS9 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developers.facebook.com/docs/ios/ios9 "Ícone de link externo"){: new_window}.

## Inicializando o {{site.data.keyword.amashort}} client Swift SDK
{: #facebook-auth-ios-initalize-swift}

Inicialize o SDK do cliente passando o `tenantId`.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK incluindo os cabeçalhos a seguir:

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
   ```
   {: codeblock}

1. Inicialize o client SDK.

   ```Swift 	let tenantId = "<serviceTenantID>" 	let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: 		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   No código:

   * Substitua `<applicationBluemixRegion>` pela região em que seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado.
   * Substitua `tenantId` pelo valor
**TenantId/App GUID**.

   Para obter mais informações sobre esses valores, veja [Antes de iniciar](#before-you-begin).

1. Notifique o Facebook SDK sobre a ativação do app e registre o Manipulador de
autenticação do Facebook incluindo o código a seguir no método
`application:didFinishLaunchingWithOptions` na delegação do app. Inclua esse código depois de inicializar a instância BMSClient e registre o Facebook como o gerenciador de autenticação.

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Copie o arquivo `FacebookAuthenticationManager.swift` dos
arquivos de origem pod `BMSFacebookAuthentication` para o diretório de
projeto.

1. Inclua o código a seguir no delegado do app.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Testando a Autenticação
{: #facebook-auth-ios-testing}

Após o Cliente SDK ser
inicializado e o Facebook
Authentication Manager ser registrado, será possível começar a fazer solicitações ao seu
aplicativo backend móvel.

### Antes de iniciar
{: #facebook-auth-ios-testing-before}

Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido do seu aplicativo backend móvel recém-criado em seu navegador. Abra a URL a seguir:
`{applicationRoute}/protected`, substituindo o `{applicationRoute}` pelo valor que você recuperou a partir das
**Opções de dispositivo móvel** (veja [Configurando o Mobile Client Access para autenticação do
Facebook](#facebook-auth-ios-configmca)).
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é
protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal.

   ```Swift 	let protectedResourceURL = "<your protected resource absolute path>" 	let request = Request(url: protectedResourceURL, method:
HttpMethod.GET)

   let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
 if error == nil {
         print ("response:\(response?.responseText), no error")
 } else {
         print ("error: \(error)")
    	}
   }

	request.send(completionHandler: callBack)
   ```
   {: codeblock}

1. Execute o aplicativo. Uma tela de login do Facebook é exibida.

   ![image](images/ios-facebook-login.png)

   Essa tela poderá parecer um pouco diferente se você não estiver conectado ao Facebook no momento.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no console do Xcode:

   ```
   response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
   ```
   {: screen}

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   Se você chamar esse código após um usuário ter efetuado login com o Facebook e o usuário tentar efetuar login novamente, ele será
solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Facebook para fins de autenticação.

   Para alternar usuários, deve-se chamar esse código e o usuário deve efetuar logout do Facebook em seu navegador.

   Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
