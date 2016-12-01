---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Tutorial - Iniciador de código de idioma do Watson
{: #tutorial_watson_language}

O Iniciador de código do {{site.data.keyword.Bluemix}} Mobile para idioma do Watson apresenta os serviços de Texto para fala e Tradução do idioma para cada um dos serviços do {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisitos
{: #tutorial_requirements}

* Uma conta do [Bluemix](http://bluemix.net)
* Instâncias de serviços de
[Tradutor
de idioma](https://console.{DomainName}/catalog/services/language-translator/) e
[Texto para
fala](https://console.{DomainName}/catalog/services/text-to-speech/) obtidas do [Catálogo
do Bluemix](https://console.{DomainName}/catalog/)


## Guia de Introdução
{: #tutorial_gs}

Para colocar em funcionamento rapidamente o Iniciador de código de idioma do Watson, siga estas etapas:

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Idioma do Watson** e clique em **Criar projeto**.

   4. Insira o nome do projeto e clique em **Criar**.

2. Opcional: inclua o recurso Notificações push.

   1. Clique em **Incluir** para **Notificações push** na página **Visão geral do projeto**.

      Como alternativa, clique em **Criar** na página **Notificações push**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Serviço de notificação push da Apple](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure o Sistema de mensagens em nuvem do Google](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Opcional: inclua o recurso de Analítica.

   1. Clique em **Incluir** para **Analítica** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** a partir da página **Analítica**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Desligue o **Modo demo** para ver os seus lados de analítica após executar o seu aplicativo.

4. Opcional: inclua o recurso Autenticação.

   1. Clique em **Incluir** para **Autenticação** na página **Visão geral do projeto**.

      Como alternativa, é possível selecionar **Criar** na página **Autenticação**.

   2. Insira o nome do serviço e clique em **Criar**.
   
   3. Alterne em **Autenticação**.
   
   4. Selecione seu provedor de identidade e insira as informações requeridas para configurá-lo. É possível ativar apenas um provedor de identidade.

   5. Consulte [Introdução ao Mobile Client Access](/docs/services/mobileaccess/index.html){: new_window} para obter mais informações sobre a configuração da autenticação.

5. Faça download do seu projeto.

   1. Clique em **Código** e selecione seu idioma preferencial.

   2. Clique em **Fazer download do código**.

6. Extraia o archive e visualize o arquivo `README.md` em um visualizador de Redução de preço para concluir a configuração.


## O que Fazer a Seguir
{: #tutorial_next}

[Teste-o!](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}
