---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Instalando e conectando o aplicativo móvel de amostra
{: #iot4i_gettingstarted}

O app móvel de amostra do {{site.data.keyword.iotinsurance_full}} é uma implementação de referência para um cliente móvel do {{site.data.keyword.iotinsurance_short}}. É possível usar o aplicativo para registrar novos dispositivos no sistema e receber alertas para os dispositivos.
{:shortdesc}

**Nota**: o {{site.data.keyword.iotinsurance_short}} não implementa mais o {{site.data.keyword.amafull}} nem o {{site.data.keyword.mobilepushfull}}. Versões anteriores do {{site.data.keyword.iotinsurance_short}} usavam o serviço {{site.data.keyword.amashort}} para processar as respostas do app móvel. Esse processo continua a funcionar para todas as instâncias existentes do {{site.data.keyword.iotinsurance_short}}. Entretanto, deve-se criar um processo de autenticação customizado para usar o app móvel com novas instâncias do
{{site.data.keyword.iotinsurance_short}}. Opcionalmente, também é possível [criar uma instância do {{site.data.keyword.mobilepushshort}}](../mobilepush/index.html), configurá-la e vinculá-la à API {{site.data.keyword.iotinsurance_short}}.

**Pré-requisitos:** antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:
  - Ambiente de desenvolvimento integrado do Apple Xcode 8 ou superior.
  - Um iOS 9.0 ou dispositivo móvel iPhone superior.
  - CocoaPods instalado no computador. Veja o [website CocoaPods ![Ícone de link externo](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window}.
  - Os [parâmetros](#iot4i_mobileParam) necessários para conectar o app móvel de amostra à instância do serviço.

## Construindo o app móvel de amostra
{: #building_mobile}
Para experimentar o app móvel de amostra, execute as tarefas a seguir:

1. Clone o [repositório de código-fonte para o app móvel de amostra ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} em um computador que tenha o Xcode 7.3 ou superior instalado.
2. Instale os pacotes necessários e gere o arquivo IoT4I.xcworkspace executando um comando pod install do CocoaPods em seu projeto. O CocoaPods deve estar instalado para concluir essa tarefa.
3. Abra o projeto no Xcode clicando duas vezes no arquivo IoT4I.xcworkspace.
4. Conecte seu iPhone ao computador e selecione-o como um destino de construção.
5. Selecione o arquivo IoT4I na lista de arquivos para exibir a caixa de diálogo Identidade.
6. Na caixa de diálogo Identidade, no Xcode, faça as mudanças a seguir:
  - Mude o **Identificador de pacote configurável** para um identificador exclusivo, por exemplo: **myIoT4Ibundle**.
  - Configure **Equipe** com o nome de sua equipe pessoal e, em seguida, clique em **Corrigir problema**.
7. Para conectar seu app à instância do {{site.data.keyword.iotinsurance_short}}, configure os parâmetros a seguir no arquivo **constants.swift**:  
    - [applicationRoute](#iot4i_mobileParam) = a URL para o aplicativo da API {{site.data.keyword.iotinsurance_short}}. É possível localizar esse valor na guia Credenciais de serviço do console de serviço do {{site.data.keyword.iotinsurance_short}}.
    - [applicationId](#iot4i_mobileParam) = o GUID para sua instância do {{site.data.keyword.amashort}}. É possível localizar esse valor ao abrir {{site.data.keyword.amashort}} e, em seguida, clicar em **Opções móveis**.  O valor é chamado App GUID / TenantId.
8. No computador, clique na seta para construir e executar o esquema atual. O app móvel de amostra é instalado em seu telefone. Para obter mais informações, veja as [Instruções do desenvolvedor Apple para executar apps em dispositivos do Xcode ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window}.

  **Nota:** se for exibido um erro quando você tentar construir que diz *Não foi possível ativar o IoT4I porque você ainda não verificou se o certificado do app desenvolvedor é confiável no dispositivo*, selecione você mesmo como Desenvolvedor confiável, como a seguir:  
    1. Em seu telefone, acesse **Configurações > Geral > Gerenciamento de dispositivo > yourDeveloperID**.
    2. Pressione o nome da conta de seu ID de desenvolvedor para estabelecer confiança para seu ID de desenvolvedor.
    3. Quando solicitado, confirme que o ID de desenvolvedor é confiável.

## Ativando notificações push para o app móvel
{: #iot4i_pushNotification}

Execute as tarefas a seguir para ativar notificações push para seu dispositivo móvel. Deve-se ter uma associação válida de Conta de desenvolvedor Apple para usar o serviço de notificação push.

1. Efetue login em sua [conta do desenvolvedor Apple ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window}.

2. Crie um arquivo de certificado.
  1. Selecione **Certificados, identificadores e perfis**.
  2. Selecione identificadores: IDs do app.
  3. Clique no botão Incluir (+) para criar um novo ID de app.
  4. Insira uma descrição para o app em **Descrição**.
  5. Selecione **ID de app explícito** e insira um ID de pacote configurável, por exemplo, com.YourOrganizationName.iot4i.mobileApp).
  6. Selecione (V) em **Push Notifications** e clique em **Continuar > Registrar > Pronto**.

3. Crie um certificado de notificação push.
  1. Selecione **Certificados: todos**.
  2. Clique no botão Incluir (+) para criar um novo certificado APN.
  3. Na página Incluir certificado iOS, selecione **SSL do serviço Apple Push Notification (ambiente de simulação)** e clique em **Continuar**.
  4. Selecione o ID do app criado na etapa anterior e clique em **Continuar**.
  5. Crie um arquivo CSR usando as instruções que estão na página e clique em **Continuar**.
  6. Selecione o arquivo CSR criado e clique em **Continuar**.
  7. Faça download e execute o arquivo de certificado.

4. Crie um perfil.
  1. Selecione **Perfil de fornecimento: desenvolvimento**.
  2. Clique no botão Incluir (+) para criar um novo perfil de desenvolvimento.
  3. Selecione **Desenvolvimento de app iOS** e clique em **Continuar**.
  4. Selecione o ID do app criado anteriormente.
  5. Selecione **Certificados do desenvolvedor: todos** e clique em **Continuar**.
  5. Selecione **Todos os dispositivos de desenvolvimento (dispositivos de teste)** e clique em **Continuar**.
  6. Especifique um nome de Perfil e clique em **Continuar**.
  7. Faça download e execute o perfil gerado.

5. Crie um arquivo de Padrões de Criptografia de Chave Pública (PKCS) 12 e inclua-o no serviço {{site.data.keyword.mobilepushshort}}.
  1. Abra o Acesso Keychain e selecione **Meus certificados**.
  2. Clique com o botão direito em **Apple Development IOS Push Service: (bundleID)** e, em seguida, exporte, salve e insira uma senha para o arquivo.
  3. Em seu console do {{site.data.keyword.Bluemix_notm}}, abra o serviço do {{site.data.keyword.mobilepushshort}}.
  4. Clique em **Configurar**.
  5. Na seção Certificado do Apple Push Notifications, faça upload do arquivo PKCS 12 e insira a senha.
  6. No Xcode, mude o identificador de pacote configurável para aquele criado anteriormente.
  7. Execute o app e conceda permissões para o serviço Push Notification.
