---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# Criando projetos móveis a partir do Painel móvel
{: #mobile}
*Última atualização: 18 de julho de 2016*
{: .last-updated}

Com os Serviços móveis do {{site.data.keyword.Bluemix}}, é possível incorporar serviços de nuvem pré-construídos, gerenciados e escaláveis em seus aplicativos móveis sem depender do envolvimento da TI. Você pode focar na construção dos seus apps móveis em vez de nas complexidades de gerenciamento da infraestrutura de backend.

O Painel móvel fornece uma experiência integrada no {{site.data.keyword.Bluemix_notm}}. É possível criar novos projetos móveis facilmente a partir do painel. Com a visualização **Projetos**, é possível gerenciar todos os seus projetos em um lugar. A visualização **Serviços** mostra suas instâncias de serviço móvel existentes.

Para visualizar o Painel móvel, clique na categoria **Móvel** em sua página inicial do {{site.data.keyword.Bluemix_notm}}.
<img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}} home">

Para iniciar, clique em **Novo projeto** na visualização **Projetos** do Painel móvel.

## Visão geral de serviços móveis do {{site.data.keyword.Bluemix_notm}}
{: #mobile_services_overview}

A tabela a seguir representa os Serviços móveis do {{site.data.keyword.Bluemix_notm}} disponíveis. É possível usar serviços individuais a partir do catálogo {{site.data.keyword.Bluemix_notm}} ou é possível integrá-los em seu projeto móvel.

<table summary="Esta tabela descreve Serviços móveis do {{site.data.keyword.Bluemix_notm}} e fornece links para a documentação do serviço">
<caption>Tabela 1. Serviços móveis do {{site.data.keyword.Bluemix_notm}}</caption>
<th>Serviço móvel do {{site.data.keyword.Bluemix_notm}}</th>
<th>Descrição</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}icon"><br/><b>{{site.data.keyword.mobileanalytics_short}} (Experimental)</b></td>
<td valign="top">Use o serviço {{site.data.keyword.mobileanalytics_full}} para medir o estado, comportamento e contexto dos seus aplicativos móveis, usuários móveis e dispositivos móveis.<br/><br/>
Leia mais sobre operar esse serviço na documentação do <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} documentation link">{{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}}ícone de serviço"><br/><b>{{site.data.keyword.amashort}}</b></td>
<td valign="top">Use o serviço {{site.data.keyword.amafull}} para incluir a funcionalidade de segurança em seu aplicativo móvel. É possível configurar a autenticação de cliente e os provedores de identidade para que os usuários possam efetuar login no aplicativo com suas contas Google ou Facebook existentes.<br/><br/>
Leia mais sobre operar esse serviço na documentação <a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} documentation link">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}}ícone de serviço"><br/> <b>{{site.data.keyword.mobilefoundation_short}}</b></td>
<td valign="top">Use o serviço {{site.data.keyword.mobilefoundation_long}} para expedir a configuração de um ambiente {{site.data.keyword.mfp_full}} a partir do qual é possível desenvolver, testar e operar aplicativos móveis corporativos.<br/><br/> Leia mais sobre operar esse serviço na documentação
<a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} documentation link">{{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}}ícone de serviço"><br/><b>{{site.data.keyword.mqa}}</b></td>
<td valign="top">Use o serviço {{site.data.keyword.mqafull}} para descobrir e configurar serviços de qualidade móveis para seus aplicativos. É possível visualizar métricas de qualidade de alto nível para seus apps móveis para obter uma compreensão rápida dos problemas dos apps com os quais você está trabalhando. Essas métricas incluem informações sobre travamentos, erros, feedback do usuário e impressão do usuário. Ao visualizar essas informações para seus aplicativos, é possível determinar se deve investigar problemas específicos adicionalmente.<br/><br/>
Leia mais sobre operar esse serviço na documentação <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} documentation link">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="ícone de serviço das Notificações Push"><br/><b>{{site.data.keyword.mobilepushshort}}</b></td>
<td valign="top">Use o serviço {{site.data.keyword.mobilepushfull}} para enviar e gerenciar notificações push móveis destinadas a plataformas iOS e Android. Esse serviço gerencia o mapeamento dos usuários do aplicativo para seus dispositivos, plataforma de dispositivo e manipula o despacho de notificações push para os dispositivos. com esse serviço, é possível enviar transmissões, unicasts (com base no userID, deviceID) e tags (ou tópicos) baseados nas notificações push para seus usuários de aplicativo móvel.<br/><br/>
Leia mais sobre operar esse serviço na documentação <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} documentation link">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Integrando serviços móveis
{: #services_integration}
É possível integrar seus Serviços móveis existentes do {{site.data.keyword.Bluemix_notm}}, como {{site.data.keyword.mobilepushshort}} e {{site.data.keyword.cloudant}}, em seu projeto.

#### Integrando o {{site.data.keyword.mobilepushshort}}
{: #push_integration}

Para integrar o serviço existente do {{site.data.keyword.mobilepushshort}}, siga estas etapas:

1. Clique em sua instância de serviço do {{site.data.keyword.mobilepushshort}}.
2. Clique em **Opções móveis** e copie os valores **Route** e **AppGuid**.

   **Nota**: seu serviço {{site.data.keyword.mobilepushshort}} deve ser ligado a um aplicativo para ver **Opções móveis**.

3. Navegue novamente até a visualização **Projetos** do Painel móvel.
4. Clique em seu projeto para editá-lo.
5. Clique em **Push** e ative as notificações.
6. Forneça o valor **AppGuid** que copiou anteriormente no **ID do aplicativo**.
7. Forneça o valor de **Rota** que copiou
anteriormente na **URL de rota do aplicativo**.

#### Integrando o {{site.data.keyword.cloudant}}
{: #cloudant_integration}

Para integrar o serviço existente do {{site.data.keyword.cloudant}}, siga estas etapas:

1. Clique em sua instância de serviço do {{site.data.keyword.cloudant}}.
2. Clique em **ATIVAR**.
3. Na visualização **Bancos de dados**, clique no Nome do banco de dados.
4. Clique em **API** e copie o valor de **Chave API** por meio do nome do banco de dados.

   **Nota**: não copie o conteúdo depois do nome do banco de dados.

5. Clique em **Permissões** >
**Gerar chave API** e copie os valores de
**Chave** e **Senha**.
6. Navegue novamente até a visualização **Projetos** do Painel móvel.
7. Clique em seu projeto para editá-lo.
8. Clique em **Dados** > **+ origem de dados** > **Cloudant** e forneça o nome
da origem de dados e clique em **Incluir**.
9. Clique em **Configuração de Cloudant**.
10. Forneça o valor de **Chave API** que
copiou anteriormente na **URL da API**.
11. Forneça o valor **Chave** que copiou
anteriormente no **Usuário**.
12. Forneça o valor de **Senha** que
copiou anteriormente na **Senha**.
13. Clique em **Ok**.


# Links relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Postagens do blog
{: #general}
* [Postagem do blog: Introducing the Bluemix Mobile
dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Tutoriais e amostras
{: #samples}
* [Backend móvel para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
