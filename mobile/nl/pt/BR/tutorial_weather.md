---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# Tutorial - Iniciador de código de clima
{: #tutorial_weather}

Última atualização: 13 de outubro de 2016
{: .last-updated}

O Iniciador de código do {{site.data.keyword.Bluemix}} Mobile para clima
exibe um projeto de andaime para começar a trabalhar com clima, usando Swift, e inclui
pontos de integração de Push e Analítica.


## Requisitos
{: #tutorial_requirements}

* Uma conta do [Bluemix](http://bluemix.net)
* Uma instância de serviço de
[Dados de
empresa de meteorologia](https://console.{DomainName}/catalog/services/weather-company-data/) obtidos do
[Catálogo do Bluemix](https://console.{DomainName}/catalog/)


## Guia de Introdução
{: #tutorial_gs}

Para colocar em funcionamento rapidamente o Iniciador de código de clima, siga estas etapas:

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

   1. Na página **Introdução** no painel Móvel, clique em
**Criar projeto**.

      Como alternativa, clique em **Novo projeto** na página **Projetos**.

   2. Clique em **Iniciadores de código**.

   3. Selecione **Clima** e clique em **Criar projeto**.

   4. Insira o nome do projeto e clique em **Criar**.

2. Opcional: Inclua notificações push.

   1. Clique em **Incluir** para **Notificações
push** na página **Visão geral do projeto**.

      Como alternativa, clique em **Criar** na página
**Notificações push**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS,
[configure o Serviço de
notificação push da Apple](../services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android,
[configure o Sistema de
mensagens em nuvem do Google](../services/mobilepush/t_push_provider_android.html){: new_window}.

3. Opcional: Inclua outros serviços.

   1. Clique em **Incluir** para o serviço na página
**Visão geral do projeto**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Siga as instruções do serviço para configurá-lo.

4. Faça download do seu projeto.

   1. Clique em **Código** e selecione seu idioma preferencial.

   2. Clique em **Fazer download do código**.

5. Extraia o archive e siga as instruções no arquivo `README.md`.


## O que Fazer a Seguir
{: #tutorial_next}

[Teste-o!](http://new-console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}


# Links relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Postagens do blog
{: #general}
* [Postagem do blog: Introducing the Bluemix Mobile
dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Postagem do blog: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Postagem do blog: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Tutoriais e amostras
{: #samples}
* [Backend móvel para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
