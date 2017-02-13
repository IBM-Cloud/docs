---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutorial de ponta a ponta do Iniciador de código Cloudant Sync
{: #tutorial}

O tutorial de ponta a ponta a seguir percorre as etapas para criar um projeto por meio do Iniciador de código Cloudant Sync, incluindo as ferramentas que deverão ser instaladas e, posteriormente, as etapas para executar o iniciador no Android Studio.


### Instalando ferramentas do desenvolvedor
{: #dev_tools}

Assegure-se de que você tenha instalado as [ferramentas do desenvolvedor de pré-requisito ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](get_code.html#prereq-dev-tools "Ícone de link externo"){: new_window}.


### Criando um projeto por meio do Iniciador de código Cloudant Sync
{: #create_project}

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Cloudant Sync** e clique em **Criar projeto**.

   4. Insira o nome do projeto. Para este tutorial, use `CloudantSyncProject`.
   
   5. Clique em **Criar**.

2. Inclua o recurso de Dados. É possível criar uma nova instância de serviço
{{site.data.keyword.cloudant}} ou incluir uma instância de serviço existente.

   1. Clique em **Visualizar** no tile **Dados** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** ou **Incluir existente** e, em seguida, **Cloudant NoSQL DB** na página **Dados**.
      
   2. Opcional: se você optou por criar uma nova instância de serviço, insira seu nome de serviço e
clique em **Criar**.

   3. Opcional: se você escolheu incluir uma instância de serviço existente, selecione sua instância de serviço na lista e clique em **Incluir existente**.

   4. Clique no ícone **Menu** em seu ladrilho de serviço e selecione
**Ativar...** para ativar sua instância de serviço.

      1. Clique em **ATIVAR** para ativar seu console {{site.data.keyword.cloudant}}.

      2. Clique em **Criar banco de dados**, insira seu nome do banco de dados e
clique em **Criar**.

      3. Clique no ícone **+** ao lado de **Todos os documentos**
para incluir documentos.

3. Opcional: inclua o recurso {{site.data.keyword.mobilepushshort}}.

   1. Clique em **Incluir** para o **{{site.data.keyword.mobilepushshort}}** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** na página **{{site.data.keyword.mobilepushshort}}**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para Android, [configure o Firebase Cloud Messaging ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_android.html "Ícone de link externo"){: new_window}.
   
4. Opcional: inclua o recurso de Analítica.

   1. Clique em **Incluir** para **Analítica** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** a partir da página **Analítica**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Desligue o **Modo demo** para ver os seus lados de analítica após executar o seu aplicativo.
   
   4. Veja [Introdução ao {{site.data.keyword.mobileanalytics_short}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/index.html "Ícone de link externo"){: new_window} para obter mais informações sobre como configurar o Analytics.
  
5. Opcional: inclua o recurso Autenticação.

   1. Clique em **Incluir** para **Autenticação** na página **Visão geral do projeto**.

      Como alternativa, é possível selecionar **Criar** na página **Autenticação**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Alterne em **Autenticação**.
   
   4. Selecione seu provedor de identidade e insira as informações requeridas para configurá-lo. É possível ativar apenas um provedor de identidade.

   5. Veja [Introdução ao {{site.data.keyword.amashort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileaccess/index.html "Ícone de link externo"){: new_window} para obter mais informações sobre como configurar a Autenticação.

6. Gere seu código do projeto.

   1. Clique em **Obter código** na
página **Visão geral do projeto** para selecionar sua plataforma e idioma.
   
      Como alternativa, é possível clicar na página **Código**.
      
   2. Para Android, clique em **Android**.
   
   3. Quando o código do projeto concluir a geração, clique
em **Fazer download do código** para fazer
download do seu archive de projeto.


### Executando seu projeto do Android no Android Studio
{: #run_android}

1. Extraia o arquivo `CloudantSyncProject-Android.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `CloudantSyncProject-Android` no Android Studio.

   2. Inclua as suas credenciais do Cloudant.

      1. Na página **Dados**, clique no ícone **Menu** em
seu ladrilho de serviço e selecione **Ativar...** para ativar sua instância de
serviço.

         1. Clique em **ATIVAR** para ativar seu console {{site.data.keyword.cloudant}}.

         2. Clique em seu nome de banco de dados e, depois, em **Permissões**.

         3. Insira seu nome do banco de dados na sequência `cloudant_dbname` no
arquivo `res/values/cloudant_credentials.xml`.

         4. Clique em **Gerar chave de API**.

             1. Copie o valor de **Chave** e cole-o na sequência `cloudant_api_key` no arquivo `res/values/cloudant_credentials.xml`.

             2. Copie o valor de **Senha** e cole-o na sequência `cloudant_api_password` no arquivo `res/values/cloudant_credentials.xml`.

             3. Selecione a permissão **_admin**.
      
3. Execute seu app.


## O que Fazer a Seguir
{: #what_next}

Visualize outros tutoriais.


### Tutoriais do iniciador de UI (interface com o usuário)
{: #tutorials_UI}

* [Tutorial - Catálogo de loja](tutorial_store_catalog.html)


### Tutoriais do iniciador de código
{: #tutorials_Code}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
* [Tutorial - Clima](tutorial_weather.html)
