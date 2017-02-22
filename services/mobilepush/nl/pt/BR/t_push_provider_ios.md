---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando credenciais para o APNs
{: #create-push-credentials-apns}
Última atualização: 16 de janeiro de 2017
{: .last-updated}

O Apple Push Notification Service (APNs) permite que os desenvolvedores de aplicativos enviem notificações remotas da instância do serviço {{site.data.keyword.mobilepushshort}} no Bluemix (o provedor) para dispositivos e aplicativos do iOS. Mensagens são enviadas para um aplicativo de
destino no dispositivo. 

Obtenha e configure suas credenciais APNs. Os certificados do APNs são gerenciados com segurança pelo serviço {{site.data.keyword.mobilepushshort}} e usados para se conectar ao servidor APNs como um provedor.

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/ "External link icon"){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


##Registrando um ID de app
{: #create-push-credentials-apns-register}


O ID de app (o identificador de pacote configurável) é um
identificador exclusivo que identifica um aplicativo específico. Cada
aplicativo requer um ID de app. Serviços, como o serviço {{site.data.keyword.mobilepushshort}}, são configurados para o ID do app.

1. Certifique-se de ter uma conta do [Apple Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/ "Ícone de link externo"){: new_window}.
2. Acesse o portal do [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com "Ícone de link externo"){: new_window}, clique em **Centro de membros** e selecione **Certificados, identificadores e perfis**.
3. Acesse a seção **Registrando IDs de app** na [Biblioteca do Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991 "Ícone de link externo"){: new_window} e siga as instruções para registrar o ID de app.

Ao registrar um ID do App, selecione as opções a seguir:

* Notificações push ![Serviços de app](images/appID_appservices_enablepush.jpg)
* Sufixo de ID explícito
![ID explícito](images/appID_bundleID.jpg)
4. Crie um certificado SSL de APNs de desenvolvimento e
distribuição.

##Crie um certificado SSL de APNs de desenvolvimento e distribuição
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

1. Acesse o website [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com "Ícone de link externo"){: new_window}, clique em **Centro de membros** e selecione **Certificados, identificadores e perfis**.
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


##Criando um perfil de fornecimento de desenvolvimento
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

1. Acesse o portal do [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com "Ícone de link externo"){: new_window}, clique em **Centro de membros** e selecione **Certificados, identificadores e perfis**.
2. Acesse a [Biblioteca do Mac Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site "Ícone de link externo"){: new_window}, role para a seção **Criando perfis de fornecimento de desenvolvimento** e siga as instruções para criar um perfil de desenvolvimento.
**Nota**: Ao configurar um perfil de provisão de
desenvolvimento, selecione as opções a seguir:
	* **iOS App Development**
	* **Para apps iOS e watchOS **



##Criando um perfil de fornecimento de distribuição de
armazenamento
{: #create-push-credentials-apns-distribute_profile}

Use o perfil de fornecimento de armazenamento para
enviar seu app para distribuição para a App Store.

1. Acesse o portal do [Apple Developer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com "Ícone de link externo"){: new_window}, clique em **Centro de membros** e selecione **Certificados, identificadores e perfis**.
2. Dê um clique duplo no perfil de fornecimento
transferido por download para instalá-lo em Xcode.

##Configurando o APNs no Painel {{site.data.keyword.mobilepushshort}}
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

Para obter mais informações sobre como usar os APNs, veja [iOS Developer Library: Local and Push Notification Programming Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4 "Ícone de link externo"){: new_window}.

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
