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

# Tutorial de ponta a ponta do Iniciador de código Basic
{: #tutorial}

O tutorial de ponta a ponta a seguir percorre as etapas para criar um projeto por meio do Iniciador de código Basic, incluindo as ferramentas que deverão ser instaladas e, posteriormente, as etapas para executar o iniciador no Xcode e no Android Studio.


### Instalando ferramentas do desenvolvedor
{: #dev_tools}

Assegure-se de que você tenha instalado as [ferramentas do desenvolvedor de pré-requisito ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](get_code.html#prereq-dev-tools "Ícone de link externo"){: new_window}.


### Criando um projeto por meio do Iniciador de código Basic
{: #create_project}

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Basic** e clique em **Criar projeto**.

   4. Insira o nome do projeto. Para este tutorial, use `BasicProject`.
   
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
      
   2. Para Objective-C, clique em **iOS Obj-C**.

   3. Para Swift, clique em **iOS Swift**.
   
   4. Para Cordova, clique em **Cordova**.

   5. Para Android, clique em **Android**.
   
   6. Quando o código do projeto concluir a geração, clique
em **Fazer download do código** para fazer
download do seu archive de projeto.


### Executando seu projeto do Objective-C no Xcode
{: #run_obj-c}

1. Extraia o arquivo `BasicProject-ObjC.zip`.

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
      
   2. Abra sua área de trabalho do Xcode `BasicProject.xcworkspace`.
      
3. Execute seu app.


### Executando seu projeto do Swift no Xcode
{: #run_swift}

1. Extraia o arquivo `BasicProject-Swift.zip`.

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


### Executando seu projeto do Cordova no Xcode
{: #run_cordova_xcode}

1. Extraia o arquivo `BasicProject-Cordova.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `platforms/ios` no Xcode.
      
3. Execute seu app.


### Executando seu projeto do Cordova no Android Studio
{: #run_cordova_studio}

1. Extraia o arquivo `BasicProject-Cordova.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `platforms/android` no Android Studio.
      
3. Execute seu app.


### Executando seu projeto do Android no Android Studio
{: #run_android}

1. Extraia o arquivo `BasicProject-Android.zip`.

2. Abra o arquivo `README.md` no
visualizador Redução para configurar seu projeto.

   1. Abra seu projeto `BasicProject-Android` no Android Studio.
      
3. Execute seu app.


## O que Fazer a Seguir
{: #what_next}

Visualize outros tutoriais.


### Tutoriais do iniciador de UI (interface com o usuário)
{: #tutorials_UI}

* [Tutorial - Catálogo de loja](tutorial_store_catalog.html)


### Tutoriais do iniciador de código
{: #tutorials_Code}

* [Tutorial - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
* [Tutorial - Clima](tutorial_weather.html)
