---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Tutorial - Iniciador de código de clima
{: #tutorial_weather}

O Iniciador de código do {{site.data.keyword.Bluemix}} Mobile para clima
exibe um projeto de andaime para começar a trabalhar com clima, usando Swift, e inclui
pontos de integração de Push e Analítica.


## Requisitos
{: #tutorial_requirements}

* Uma conta do [Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net "Ícone de link externo")
* Uma instância de serviço [Weather Company Data ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/weather-company-data/ "Ícone de link externo") obtida do [Catálogo do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/ "Ícone de link externo")


## Guia de Introdução
{: #tutorial_gs}

Para colocar em funcionamento rapidamente o Iniciador de código de clima, siga estas etapas:

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Novo projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Clima** e clique em **Criar projeto**.

   4. Insira o nome do projeto e clique em **Criar**.

2. Opcional: inclua o recurso {{site.data.keyword.mobilepushshort}}.

   1. Clique em **Incluir** para o **{{site.data.keyword.mobilepushshort}}** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** na página **{{site.data.keyword.mobilepushshort}}**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Apple Push Notification Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_ios.html "Ícone de link externo"){: new_window}.

   4. Para Android, [configure o Google Cloud Messaging ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_android.html "Ícone de link externo"){: new_window}.
   
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

   5. Veja [Introdução ao Mobile Client Access ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileaccess/index.html "Ícone de link externo"){: new_window} para obter mais informações sobre como configurar a autenticação.

5. Faça download do seu projeto.

   1. Clique em **Código** e selecione seu idioma preferencial.

   2. Clique em **Fazer download do código**.

5. Extraia o archive e siga as instruções no arquivo `README.md`.


## O que Fazer a Seguir
{: #tutorial_next}

[Teste-o! ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "Ícone de link externo"){: new_window}


### Tutoriais do iniciador de UI (interface com o usuário)
{: #tutorials_UI}

* [Tutorial - Catálogo de loja](tutorial_store_catalog.html)


### Tutoriais do iniciador de código
{: #tutorials_Code}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
