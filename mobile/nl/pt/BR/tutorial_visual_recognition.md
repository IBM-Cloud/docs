---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Tutorial de ponta a ponta do
Iniciador de código
do {{site.data.keyword.visualrecognitionshort}}
{: #tutorial_vr}

O tutorial de ponta a ponta a seguir percorre as etapas para criar um projeto do Iniciador de código do {{site.data.keyword.visualrecognitionshort}}, incluindo as ferramentas que se deve ter instalado e, posteriormente, as
etapas para executar o iniciador em Xcode e Android Studio.


### Instalando ferramentas do desenvolvedor
{: #dev_tools}

Assegure-se de que você tenha instalado as [ferramentas do desenvolvedor de pré-requisito ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](get_code.html#prereq-dev-tools "Ícone de link externo"){: new_window}.


### Criando um projeto do Iniciador de código do {{site.data.keyword.visualrecognitionshort}}
{: #create_project}

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Reconhecimento visual** e clique em **Criar projeto**.

   4. Insira o nome do projeto. Para este tutorial, use `VisualRecognitionProject`.
   
   5. Clique em **Criar**.

2. Opcional: inclua o recurso {{site.data.keyword.mobilepushshort}}.

   1. Clique em **Incluir** para o **{{site.data.keyword.mobilepushshort}}** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** na página **{{site.data.keyword.mobilepushshort}}**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Apple Push Notification Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_ios.html "Ícone de link externo"){: new_window}.

   4. Para Android, [configure o Firebase Cloud Messaging ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_android.html "Ícone de link externo"){: new_window}.
   
3. Opcional: inclua o recurso de Analítica.

   1. Clique em **Incluir** para **Analítica** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** a partir da página **Analítica**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Desligue o **Modo demo** para ver os seus lados de analítica após executar o seu aplicativo.
   
   4. Veja [Introdução ao {{site.data.keyword.mobileanalytics_short}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/index.html "Ícone de link externo"){: new_window} para obter mais informações sobre como configurar o Analytics.
  
4. Opcional: inclua o recurso Autenticação.

   1. Clique em **Incluir** para **Autenticação** na página **Visão geral do projeto**.

      Como alternativa, é possível selecionar **Criar** na página **Autenticação**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Alterne em **Autenticação**.
   
   4. Selecione seu provedor de identidade e insira as informações requeridas para configurá-lo. É possível ativar apenas um provedor de identidade.

   5. Veja [Introdução ao {{site.data.keyword.amashort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileaccess/index.html "Ícone de link externo"){: new_window} para obter mais informações sobre como configurar a Autenticação.

5. Gere seu código do projeto.

   1. Clique em **Obter código** na
página **Visão geral do projeto** para selecionar sua plataforma e idioma.
   
      Como alternativa, é possível clicar na página **Código**.
      
   2. Para iOS, clique em **iOS Swift**.
   
   3. Para Android, clique em **Android**.
   
   4. Quando o código do projeto concluir a geração, clique
em **Fazer download do código** para fazer
download do seu archive de projeto.


### Executando o seu projeto do Xcode
{: #run_xcode}

1. Extraia o arquivo `VisualRecognitionProject-Swift.zip`.

2. Abra o arquivo `README.md` em um
visualizador Redução para revisar as etapas para configurar seu
projeto.

   1. Crie sua instância do serviço [{{site.data.keyword.visualrecognitionshort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/visual-recognition/ "Ícone de link externo"){: new_window}.
   
   2. Abra seu Terminal e navegue para sua pasta de
projeto.
   
      1. Execute `pod setup` se precisar
configurar seu repositório CocoaPods.
      
      2. Execute `pod update` se precisar
atualizar os seus módulos existentes.
      
      3. Execute `pod install` para instalar
os módulos requeridos para seu projeto.
      
      4. Execute `carthage update --platform
iOS` para construir as dependências e estruturas para usar o
SDK do iOS {{site.data.keyword.ibmwatson}} Developer Cloud.
      
   3. Abra a sua área de trabalho Xcode `VisualRecognitionProject.xcworkspace`.
   
   4. Inclua as suas credenciais de serviço
do {{site.data.keyword.visualrecognitionshort}}.
   
      1. Copie o seu `api_key` a partir das
suas credenciais de serviço
do {{site.data.keyword.visualrecognition}}.
      
      2. Cole o `api_key` na chave
`VisualRecognitionAPIKey` no arquivo `WatsonCredentials.plist`.
      
3. Execute seu app.


### Execute o seu projeto no Android Studio
{: #run_studio}

1. Extraia o arquivo `VisualRecognitionProject-Android.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Crie sua instância do serviço [{{site.data.keyword.visualrecognitionshort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/visual-recognition/ "Ícone de link externo"){: new_window}.
   
      Pule esta etapa se você já tiver uma instância de
serviço do {{site.data.keyword.visualrecognitionshort}}.
   
   2. Abra o seu projeto
`VisualRecognitionProject-Android` no Android Studio.
   
   4. Inclua as suas credenciais de serviço
do {{site.data.keyword.visualrecognitionshort}}.
   
      1. Copie o seu `api_key` a partir das
suas credenciais de serviço
do {{site.data.keyword.visualrecognitionshort}}.
      
      2. Cole o seu `api_key` na chave
`watson_visual_recognition_api_key` no arquivo `res/values/watson_credentials.xml`.
      
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
* [Tutorial - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
* [Tutorial - Clima](tutorial_weather.html)

