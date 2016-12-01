---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Tutorial de ponta a ponta do
Iniciador de código
do {{site.data.keyword.visualrecognitionshort}} 
{: #tutorial}

O tutorial de ponta a ponta a seguir percorre as etapas para criar um projeto do Iniciador de código do {{site.data.keyword.visualrecognitionshort}}, incluindo as ferramentas que se deve ter instalado e, posteriormente, as
etapas para executar o iniciador em Xcode e Android Studio.


### Instalando ferramentas do desenvolvedor
{: #dev_tools}

Assegure-se de que você tenha instalado as [ferramentas de desenvolvedor de pré-requisito](get_code.html#prereq-dev-tools){: new_window}.


### Criando um projeto do Iniciador de código do {{site.data.keyword.visualrecognitionshort}}
{: #create_project}

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Reconhecimento visual** e clique em **Criar projeto**.

   4. Insira o nome do projeto. Para este tutorial, use `VisualRecognitionProject`.
   
   5. Clique em **Criar**.

2. Opcional: inclua o recurso Notificações push.

   1. Clique em **Incluir** para **Notificações push** na página **Visão geral do projeto**.

      Como alternativa, clique em **Criar** na página **Notificações push**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Serviço de notificação push da Apple](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android,
[configure
o Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Opcional: inclua o recurso de Analítica.

   1. Clique em **Incluir** para
**Analítica** na página **Visão geral
do projeto**.

      Como alternativa, é possível clicar em
**Criar** a partir da página
**Analítica**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Desligue o **Modo demo** para ver os
seus lados de analítica após executar o seu aplicativo.
   
   4. Consulte [Introdução ao {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window} para obter mais informações sobre a configuração Analítica.
  
4. Opcional: inclua o recurso Autenticação.

   1. Clique em **Incluir** para
**Autenticação** na página **Visão
geral do projeto**.

      Como alternativa, é possível selecionar
**Criar** na página
**Autenticação**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Alterne em
**Autenticação**.
   
   4. Selecione seu provedor de identidade e insira as
informações requeridas para configurá-lo. É possível ativar apenas um provedor de identidade.

   5. Consulte
[Introdução
ao {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window}
para obter mais informações sobre a configuração Autenticação.

5. Gere o seu código do projeto.

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
visualizador Redução para revisar as etapas para configurar o seu
projeto.

   1. Crie a sua instância de serviço do [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}.
   
   2. Abra o seu Terminal e navegue para a sua pasta de
projeto.
   
      1. Execute `pod setup` se precisar
configurar o seu repositório CocoaPods.
      
      2. Execute `pod update` se precisar
atualizar os seus módulos existentes.
      
      3. Execute `pod install` para instalar
os módulos requeridos para o seu projeto.
      
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
visualizador Redução para configurar o seu projeto.

   1. Crie a sua instância de serviço do
[{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}.
   
      Pule esta etapa se você já tiver uma instância de
serviço do {{site.data.keyword.visualrecognitionshort}}.
   
   2. Abra o seu projeto
`VisualRecognitionProject-Android` no Android Studio.
   
   4. Inclua as suas credenciais de serviço do
{{site.data.keyword.visualrecognitionshort}}.
   
      1. Copie o seu `api_key` a partir das
suas credenciais de serviço do
{{site.data.keyword.visualrecognition}}.
      
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

* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
* [Tutorial - Clima](tutorial_weather.html)
