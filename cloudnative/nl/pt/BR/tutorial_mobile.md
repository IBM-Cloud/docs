---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutorial de ponta a ponta do Iniciador Mobile Basic
{: #tutorial}

O tutorial de ponta a ponta a seguir percorre as etapas para criar um projeto por meio do Iniciador Mobile Basic, incluindo as ferramentas que devem ser instaladas e, subsequentemente, as etapas para executar o projeto no Xcode e Android Studio.


## Instalando ferramentas do desenvolvedor
{: #dev_tools}

Assegure-se de que você tenha instalado as [ferramentas do desenvolvedor de pré-requisito ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](get_code.html#prereq-dev-tools){: new_window}.


## Criando um projeto usando o {{site.data.keyword.dev_console}}
{: #create-devex}

1. Crie um projeto {{site.data.keyword.dev_console}} no {{site.data.keyword.Bluemix}}.

   1. Na página **Introdução** no {{site.data.keyword.dev_console}}, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Selecione **Mobile App** e clique em **Avançar**.

   3. Selecione **Basic** e clique em **Avançar**.

   4. Insira o nome do projeto. Para este tutorial, use `MobileBasicProject`.

   5. Selecione sua plataforma. Para este tutorial, use `Swift`.
   
   6. Clique em **Criar**.

2. Opcional: inclua o recurso Autenticação.

   1. Clique em **Incluir** para **Autenticação** na página **Visão geral do projeto**.

      Como alternativa, é possível selecionar **Criar** ou **Incluir existente** na página **Recursos > Autenticação**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Alterne em **Autenticação**.
   
   4. Selecione seu provedor de identidade e insira as informações requeridas para configurá-lo. É possível ativar apenas um provedor de identidade.
   
   5. Veja [Configurando provedores de identidade} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/appid/identity-providers.html){: new_window} para obter mais informações sobre como configurar a Autenticação.

3. Opcional: inclua o recurso de Analítica.

   1. Clique em **Incluir** para **Analítica** na página **Visão geral do projeto**.

      Como alternativa, clique em **Criar** ou **Incluir existente** na página **Recursos > Analítica**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Desligue o **Modo demo** para ver os seus lados de analítica após executar o seu aplicativo.
   
   4. Veja [Introdução ao {{site.data.keyword.mobileanalytics_short}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/index.html){: new_window} para obter mais informações sobre como configurar o Analytics.

4. Opcional: inclua o recurso {{site.data.keyword.mobilepushshort}}.

   1. Clique em **Incluir** para o **{{site.data.keyword.mobilepushshort}}** na página **Visão geral do projeto**.

      Como alternativa, clique em **Criar** ou **Incluir existente** na página **Recursos > {{site.data.keyword.mobilepushshort}}**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Apple Push Notification Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure o Firebase Cloud Messaging ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Opcional: inclua o recurso Dados.

   1. Clique em **Visualizar** para **Dados** na página **Visão geral do projeto**.

      Como alternativa, é possível selecionar **Criar** na página **Dados**.
      
   2. Escolha **{{site.data.keyword.cloudant_short_notm}}** ou **{{site.data.keyword.objectstorageshort}}**.

   3. Insira o nome do serviço e clique em **Criar**.

   4. Veja [Introdução ao {{site.data.keyword.cloudant_short_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/Cloudant/index.html){: new_window} para obter mais informações sobre como configurar o {{site.data.keyword.cloudant_short_notm}}.

   5. Veja [Introdução ao {{site.data.keyword.objectstorageshort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ObjectStorage/index.html){: new_window} para obter mais informações sobre como configurar o {{site.data.keyword.objectstorageshort}}.

6. Gere seu código do projeto.

   1. Clique em **Obter o código** na página **Visão geral do projeto** para selecionar sua linguagem.
   
      Como alternativa, é possível clicar na página **Código**.
      
   2. Clique em **Gerar Swift**.
   
   3. Quando o código do projeto concluir a geração, clique em **Fazer download do Swift** para fazer download de seu archive de projeto.

7. Opcional: [atualize seu projeto](project_overview_page.html#update_language) para gerar uma nova linguagem.


## Criando um projeto usando a {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assegure-se de que tenha instalado a [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. No prompt do Terminal, navegue para um diretório local de sua preferência e execute o comando a seguir.

	```
	bx dev create
	```
	{: codeblock}
	
3. Forneça os valores a seguir quando solicitado:

	* Selecione um padrão: 2 (para Mobile)
	* Selecione um iniciador: 1 (para Basic)
	* Selecione uma plataforma: 3 (para iOS Swift)
	* Insira um nome para seu projeto: `MobileBasicProjectCLI`

4. Se desejar incluir serviços no projeto, digite `y` no prompt de pergunta e responda às perguntas restantes.

5. Quando o `MobileBasicProjectCLI` tiver sido salvo com sucesso, navegue para a pasta `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift`.


## Executando seu projeto do Swift no Xcode
{: #run_swift}

1. Extraia o arquivo `MobileBasicProject-Swift.zip`.

2. Abra o arquivo `README.md` em um
visualizador Redução para revisar as etapas para configurar seu
projeto.

   1. Abra seu Terminal e navegue para sua pasta de
projeto.
   
      1. Execute `pod setup` se precisar
configurar seu repositório CocoaPods.
      
      2. Execute `pod update` se precisar
atualizar os seus módulos existentes.
      
      3. Execute `pod install` para instalar
os módulos requeridos para seu projeto.
      
   3. Abra sua área de trabalho do Xcode `BasicProject.xcworkspace`.
      
3. Execute seu app.


## Executando seu projeto do Cordova no Xcode
{: #run_cordova_xcode}

1. Extraia o arquivo `MobileBasicProject-Cordova.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `platforms/ios` no Xcode.
      
3. Execute seu app.


## Executando seu projeto do Cordova no Android Studio
{: #run_cordova_studio}

1. Extraia o arquivo `BasicProject-Cordova.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `platforms/android` no Android Studio.
      
3. Execute seu app.


## Executando seu projeto do Android no Android Studio
{: #run_android}

1. Extraia o arquivo `MobileBasicProject-Android.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `BasicProject-Android` no Android Studio.
      
3. Execute seu app.
