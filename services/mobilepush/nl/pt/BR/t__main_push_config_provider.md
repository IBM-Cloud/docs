
---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando credenciais para um
provedor de notificação
{: #create-push-credentials}
Última atualização: 12 de abril de 2017
{: .last-updated}

Para configurar o serviço {{site.data.keyword.mobilepushshort}}, obtenha as credenciais necessárias com seu provedor de notificação push - Firebase Cloud Messaging (FCM) ou Apple Push Notification service (APNs) para dispositivos móveis. 

É possível configurar o {{site.data.keyword.mobilepushshort}} usando o painel do **IBM Bluemix Services** ou usando as [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.


## Configurando credenciais para o FCM
{: #create-push-enable-gcm}

Firebase Cloud Messaging (FCM) é o gateway usado para entregar notificações push para dispositivos Android e para o Google Chrome. FCM é a nova versão do Google Cloud Messaging (GCM). Para configurar o serviço {{site.data.keyword.mobilepushshort}} no painel, é necessário obter suas credenciais do FCM. Assegure-se de usar configurações do FCM para novos apps. Apps existentes continuarão a funcionar com configurações do GCM.

### Obtendo seu ID de emissor e chave de API
{: #android-senderid-apikey}

A chave API é armazenada com segurança e usada pelo serviço {{site.data.keyword.mobilepushshort}} para se conectar ao servidor FCM e o ID do emissor
(número do projeto) é usado pelo SDK do Android e o SDK do JS para Google Chrome e Mozilla Firefox no lado do cliente. 

Para configurar o FCM, gerar a chave API e o ID do emissor, conclua as etapas:

1. Visite o [console do Firebase ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://console.firebase.google.com/?pli=1){: new_window}.
2. Selecione **Criar novo projeto**. 
3. Na janela Criar um projeto, forneça um nome do projeto, escolha um país/região e clique em **Criar projeto**.
3. Na área de janela de navegação, clique no ícone Configurações e selecione **Configurações do projeto**.
4. Escolha a guia Cloud Messaging para gerar uma Chave API Server e um ID do emissor.

### Configurando o Push Notification service para Android e apps Chrome e extensões
{: #setup-push-android}

**Nota:** você precisará da sua Chave API e do ID do emissor do FCM/GCM (número do projeto).

1. Abra o painel Bluemix e, em seguida, clique na instância de serviço
{{site.data.keyword.mobilepushfull}} que você criou para abrir o painel. O painel Push é exibido. Para configurar um serviço {{site.data.keyword.mobilepushshort}} desvinculado
para Android, selecione o ícone do serviço {{site.data.keyword.mobilepushshort}}
desvinculado para abrir o painel do serviço {{site.data.keyword.mobilepushshort}}. 

![painel Push](images/push_unbound.jpg)

2. Clique no botão **Configurar push**, para configurar as credenciais do FCM/GCM para aplicativos Android e Apps Google Chrome e Extensões.
3. Na página **Configuração**, para Android, acesse a guia **Móvel** e configure o ID do emissor (número do projeto do
GCM) e a Chave API. Para Apps Google Chrome e Extensões, acesse a guia **Web** e configure o ID do emissor (número do projeto do FCM/GCM) e
a Chave API apropriadamente.
4. Clique em **Salvar**.
5. Próximas etapas. [Ativando notificações para Android](c_enable_push.html) ou [Ativando notificações para Apps Google Chrome e Extensões](c_web_extensions.html).


## Configurando credenciais para o APNs
{: #create-push-credentials-apns}

O Apple Push Notification Service (APNs) permite que os desenvolvedores de aplicativos enviem notificações remotas da instância do serviço {{site.data.keyword.mobilepushshort}} no Bluemix (o provedor) para dispositivos e aplicativos do iOS. Mensagens são enviadas para um aplicativo de
destino no dispositivo. 

Obtenha e configure suas credenciais APNs. Os certificados do APNs são gerenciados com segurança pelo serviço {{site.data.keyword.mobilepushshort}} e usados para se conectar ao servidor APNs como um provedor.

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


### Registrando um ID de app
{: #create-push-credentials-apns-register}


O ID de app (o identificador de pacote configurável) é um
identificador exclusivo que identifica um aplicativo específico. Cada
aplicativo requer um ID de app. Serviços, como o serviço {{site.data.keyword.mobilepushshort}}, são configurados para o ID do app.

1. Certifique-se de ter uma conta do [Apple Developers ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window}.
2. Acesse o portal [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com){: new_window}, clique em **Member Center** e selecione **Certificates, Identifiers & Profiles**.
3. Acesse a seção **Registering App IDs** na [Apple Developer Library ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} e siga as instruções para registrar o ID do app.

Ao registrar um ID do App, selecione as opções a seguir:

* Notificações push ![Serviços de app](images/appID_appservices_enablepush.jpg)
* Sufixo de ID explícito
![ID explícito](images/appID_bundleID.jpg)
4. Crie um certificado SSL de APNs de desenvolvimento e
distribuição.

### Crie um certificado SSL de APNs de desenvolvimento e distribuição
{: #create-push-credentials-apns-ssl}

Antes de obter um certificado APNs, deve-se primeiro gerar uma solicitação de assinatura de certificado (CSR) e enviá-la para Apple, a autoridade de certificação (CA). A CSR contém informações que identificam sua empresa e suas chaves pública e privada usadas para assinar suas notificações push da Apple. Depois, gere o certificado SSL no
            portal de Desenvolvedor de iOS. O certificado, junto com
seu público e chave privada, é armazenado no Keychain Access.

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

É possível usar APNs de dois modos: 

* Modo de ambiente de simulação para desenvolvimento e teste.
* Modo de produção ao distribuir aplicativos por meio da App Store (ou outros mecanismos de distribuição da empresa).

É necessário obter certificados separados para
seus ambientes de desenvolvimento e distribuição. Os certificados são
associados a um ID de app para o app que é o destinatário das
notificações remotas. Para produção, é possível criar até dois
certificados. O Bluemix usa os certificados para estabelecer uma
conexão SSL com APNs.

<!-- Create a development and distribution SSL certificate. -->

1. Acesse o website [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com){: new_window}, clique em **Member Center** e selecione **Certificates, Identifiers & Profiles**.
2. Na área **Identificadores**, clique em
**IDs de app**.
3. A partir da sua lista de IDs do app, selecione o seu <!--newly created--> ID do app e, em seguida, selecione
**Configurações**.
4. Na área **Serviço Push
Notifications**, crie um
certificado SSL de desenvolvimento e depois um certificado SSL de
produção.

	![Certificados SSL de notificação push](images/certificate_createssl.jpg)

5. Quando a **tela Sobre a criação de uma solicitação de assinatura
de certificado (CSR)** for exibida, inicie o aplicativo
**Keychain Access** em seu Mac para criar uma solicitação de
assinatura de certificado (CSR).
6. No menu, selecione **Keychain Access > Assistente de certificado > Solicitar um certificado de uma autoridade de certificação…** 
7. Em **Informações de certificado**, insira o endereço de
e-mail associado à sua conta de Desenvolvedor de app e um nome comum. Forneça um nome
significativo que ajude a identificar se é um certificado para desenvolvimento (ambiente
de simulação) ou distribuição (produção); por exemplo,
*sandbox-apns-certificate* ou *production-apns-certificate*.
8. Selecione **Salvar no disco** para fazer download do arquivo
`.certSigningRequest` para sua área de trabalho e, em seguida, clique em
**Continuar**.
9. Na opção de menu **Salvar como**, nomeie o arquivo
`.certSigningRequest` e clique em **Salvar**.
10. Clique em **Pronto**. Agora você tem uma
CSR.
11. Retorne para a janela **Sobre como criar uma solicitação de
assinatura de certificado (CSR)** e clique em **Continuar**. 
12. Na tela **Gerar**, clique em
**Escolher arquivo ... **e selecione o arquivo CSR
salvo em sua área de trabalho. Em seguida, clique em **Gerar**.
	![Gerar certificado
](images/generate_certificate.jpg)
13. Quando seu certificado estiver pronto, clique em
**Concluído**.
14. Na tela **Notificações push**, clique em
**Fazer download** para fazer download do seu certificado e depois
clique em **Concluído**. 
	![Fazer download de certificado](images/certificate_download.jpg)
15. No Mac, acesse **Keychain Access > Meus certificados** e
localize seu certificado recém-instalado. Dê um clique duplo no certificado
para instalá-lo no Keychain Access.
16. Selecione o certificado e a chave privada; em seguida, selecione
**Exportar** para converter o certificado no formato de troca de
informações pessoais (formato `.p12`).
	![Exportar certificado e chaves](images/keychain_export_key.jpg)
17. No campo **Salvar como**, dê um nome significativo para o certificado. Por
exemplo, `sandbox_apns.p12_certifcate` ou
`production_apns.p12`; em seguida, clique em **Salvar**.
	![Exportar certificado e
chaves](images/certificate_p12v2.jpg)
18. No campo **Inserir uma senha**, insira
uma senha para proteger os itens exportados e clique em **OK**. É possível usar essa senha para configurar as definições do APNs no painel Push.{: #step18}
	![Exportar certificado e chaves](images/export_p12.jpg)
19. O **Key Access.app** solicita que
você exporte sua chave da tela **Keychain**. Insira sua senha
administrativa para seu Mac para permitir que o sistema exporte esses itens; em seguida,
selecione a opção **Sempre permitir**. Um certificado
`.p12` é gerado em sua área de trabalho.


### Criando um perfil de fornecimento de desenvolvimento
{: #create-push-credentials-dev-profile}

O perfil de fornecimento funciona com o ID de app para
determinar quais dispositivos podem instalar e executar seu app e
quais serviços seu app pode acessar. Para cada ID de app, você cria
dois perfis de fornecimento: um para desenvolvimento e outro para
distribuição. Xcode usa o perfil de fornecimento de desenvolvimento
para determinar quais desenvolvedores podem criar o aplicativo e
quais dispositivos podem ser testados no aplicativo.

Certifique-se de registrar um ID de app, de ativá-lo para o serviço {{site.data.keyword.mobilepushshort}} e de configurá-lo para
usar um certificado SSL APNs de desenvolvimento e produção.

Crie um perfil de fornecimento de desenvolvimento, da seguinte forma:

1. Acesse o portal [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com){: new_window}, clique em **Member Center** e selecione **Certificates, Identifiers & Profiles**.
2. Acesse a [Mac Developer Library ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}, role até a seção **Creating Development Provisioning Profiles** e siga as instruções para criar um perfil de desenvolvimento.
**Nota**: Ao configurar um perfil de provisão de
desenvolvimento, selecione as opções a seguir:
	* **iOS App Development**
	* **Para apps iOS e watchOS **


### Criando um perfil de fornecimento de distribuição de
armazenamento
{: #create-push-credentials-apns-distribute_profile}

Use o perfil de fornecimento de armazenamento para
enviar seu app para distribuição para a App Store.

1. Acesse o portal [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com){: new_window}, clique em **Member Center** e selecione **Certificates, Identifiers & Profiles**.
2. Dê um clique duplo no perfil de fornecimento
transferido por download para instalá-lo em Xcode.

### Configurando APNs no painel Notificação push
{: #create-push-credentials-apns-dashboard}

Para usar o serviço {{site.data.keyword.mobilepushshort}} para enviar notificações, faça upload dos certificados SSL necessários para o Apple Push Notification Service (APNs). A API REST também pode ser
usada para fazer upload de um certificado APNs.

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

Os certificados necessários para APNs são certificados `.p12`. Esses certificados
contêm a chave privada e os certificados SSL que são necessários
para construir e publicar seu aplicativo. Deve-se gerar os certificados a partir do Member Center do
website do Apple Developer (para o qual é necessária uma conta válida do Apple Developer). São necessários certificados separados para o
ambiente de desenvolvimento (ambiente de
simulação) e para o ambiente de produção (distribuição).

**Nota**: depois que o arquivo `.cer` estiver
em seu acesso de cadeia de chaves, exporte-o para seu computador para criar um
certificado `.p12`.

Para obter mais informações sobre o uso de APNs, veja [iOS Developer Library: Local and Push Notification Programming Guide ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}.

Para configurar os APNs no painel de serviços de Notificação push, conclua as etapas:

1. Selecione **Configurar** no painel de
serviços de Notificação push.
2. Escolha a opção **Móvel** para atualizar
as informações no formulário **Credenciais push de
APNs**.
3. Selecione **Ambiente de simulação**
(desenvolvimento) ou **Produção** (distribuição)
conforme apropriado e, em seguida, faça upload do certificado
`p.12` que você criou, usando a
[etapa](#step18) anterior.
  ![Configure o painel de notificações
push](images/wizard.jpg)
3. No campo **Senha**, insira a senha que está
associada ao arquivo de certificado `.p12`; em seguida, clique em
**Salvar**.

Após o
upload bem-sucedido dos certificados com uma senha válida, é possível iniciar
o envio de notificações.

## Configurando credenciais para navegadores da web
{: #configure-credential-for-browsers}

Agora, o serviço IBM {{site.data.keyword.mobilepushshort}} estende os recursos para enviar notificações para seu navegador. 

A URL do website ou o nome de domínio de seu website é requerido pelo serviço {{site.data.keyword.mobilepushshort}} para identificar as solicitações que precisam ser permitidas. Uma instância do serviço {{site.data.keyword.mobilepushshort}} suporta somente um nome de domínio por vez. Portanto, assegure-se de que o mesmo valor seja configurado para o Chrome, Firefox e Safari. 

Os navegadores Chrome e Safari requerem configuração adicional para push da web. Você precisaria de uma chave de API do FCM, pois um terminal do FCM é usado para entregar mensagens no Chrome. 


### Configurando para push da web do Chrome e do Firefox 
{: #config-chrome-firefox}

1. Na área do Painel push, selecione **Configurar**.
2. Selecione a guia Web.
	![Configuração de WebPush](images/webpush_configure.jpg)
3. Configure a chave API do FCM/GCM e a URL de seu website que estará registrada para receber notificações push.
4. Clique em **Salvar**.
5. Próximas etapas. [Ativando notificações para navegadores Google Chrome e Mozilla Firefox](c_chrome_firefox_enable.html).


### Configurando para push da web do Safari 
{: #configure-safari}

A versão suportada para o serviço {{site.data.keyword.mobilepushshort}} no Safari é 10.0. É necessário gerar um certificado por meio de sua conta do Apple Developer, antes de poder configurar o navegador para receber notificações.

#### Gerando um certificado
{: #certificate-generation}

Assegure-se de ter uma conta do Apple Developer. É necessário
registrar um ID de push do website e gerar um certificado para
configurar o seu navegador Safari para receber notificações. As
etapas a seguir ajudarão na introdução.

1. No centro de Membro de desenvolvedor Apple, clique em
**Certificados, ID e perfis**. 
2. Clique em **Identificadores** e, sem
seguida, **IDs de push do website**.
3. Escolha criar uma nova entrada, selecionando o ícone de
mais.
  ![painel Push](images/safari_1.jpg)

4. No painel Registrar ID de push do website, forneça uma
descrição do ID de push do website e um ID do identificador
apropriados. Recomenda-se que estejam no formato de nome de domínio reverso, começando com `web`. Por exemplo: `web.com.example.dailyweatherreports`.
5. Registre o ID de push do website. Agora, você tem seu ID de push do website. 
6. Selecione **Editar** para criar um certificado a ser usado pelo ID de push do
website.
7. Na janela Assistente de certificado, forneça seu ID do
e-mail e um nome comum. Deixe o endereço de e-mail da Autoridade
de certificação em branco.
8. Clique em **Salvar em disco** e
selecione **Continuar**.
9. Escolha para salvar o certificado em uma pasta
apropriada.
10. Escolha `.certSigningRequest` criado no disco, quando solicitado, no assistente
para gerar o certificado. Certifique-se de fazer download do certificado de push do website criado no
formato `.cer`.
11. Abra o certificado na ferramenta KeyChain Access. Clique com o botão direito e exporte
como um certificado p12. Observe a senha fornecida durante a geração do certificado p12.


#### Configurando para notificações
{: #configuration-notification}
 
Após gerar o certificado, é possível configurar o serviço para enviar notificações para o Safari. 

Conclua estas etapas:

1. No painel de serviço Notificações push, **clique em Configurar**. 
2. Selecione a guia Web. 
3. Na seção Push do Safari, atualize o formulário com as informações necessárias. 
	- **Nome do website**: este é o nome que você forneceu no centro de notificação.
	- **ID de push do website**: atualize com a sequência de domínio reversa para seu
ID de push do website. Por exemplo, web.com.example.www.
	- **URL do website**: forneça a URL do website que deve ser inscrita para
notificações push. Por exemplo, https://www.example.com.
	- **Domínios permitidos**: este é parâmetro opcional. Esta é a lista de websites
que solicitam permissão do usuário. Certifique-se de que as URLs sejam valores separados por vírgula. Observe
que o valor na URL do website será usado se isso não for fornecido. 
	- **Sequência de formatações de URL**: a URL a ser resolvida quando a notificação é clicada. Por exemplo, ["https://www.example.com"]. Assegure-se de que a URL use o esquema HTTPS ou HTTP.
	- **Certificado de push da web do Safari**: faça upload do
certificado .p12 e forneça a senha.
4. Clique em **Salvar**.	

![painel Push](images/push_configure_safari.jpg)	

Agora, você está configurado para enviar notificações push para o navegador Safari.
