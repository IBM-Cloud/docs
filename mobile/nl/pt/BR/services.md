---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Serviços
{: #services}

Última atualização: 18 de outubro de 2016
{: .last-updated}

Na visualização **Serviços** do painel do
{{site.data.keyword.Bluemix}} Mobile, é possível visualizar seus serviços
existentes ou criar novos serviços. O painel Móvel fornece um único local para visualizar
todos os serviços do Bluemix que estão sendo gerenciados pelos projetos.  

Se você excluir serviços da visualização **Serviços**, irá desconectar o serviço do projeto ao qual ele está associado. Crie uma nova instância de serviço se quiser reconectar o serviço ao projeto.

## Visão geral de serviços móveis do {{site.data.keyword.Bluemix_notm}}
{: #mobile_services_overview}

A tabela a seguir representa os serviços do {{site.data.keyword.Bluemix_notm}}. É possível usar serviços individuais a partir do catálogo {{site.data.keyword.Bluemix_notm}} ou é possível integrá-los em seu projeto móvel.

<table summary="Esta tabela descreve Serviços móveis do {{site.data.keyword.Bluemix_notm}} e fornece links para a documentação do serviço">
<caption>Tabela 1. Serviços móveis do {{site.data.keyword.Bluemix_notm}}</caption>
<th>Serviço móvel do {{site.data.keyword.Bluemix_notm}}</th>
<th>Descrição</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}icon"><br/>{{site.data.keyword.mobileanalytics_short}} (Beta)</td>
<td valign="top">Use o serviço {{site.data.keyword.mobileanalytics_full}} para ganhar insight sobre como seus apps móveis estão executando e como estão sendo usados.<br/><br/>
Leia mais sobre a operação desse serviço na <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} documentation link">Documentação do {{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}}ícone de serviço"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Use o serviço {{site.data.keyword.amafull}} para incluir a funcionalidade de segurança em seu aplicativo móvel. É possível configurar a autenticação de cliente e os provedores de identidade para que os usuários possam efetuar login no aplicativo com suas contas Google ou Facebook existentes.<br/><br/> Leia mais sobre operar esse serviço na documentação <a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} documentation link">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}}ícone de serviço"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Use o serviço {{site.data.keyword.mobilefoundation_long}} para expedir a configuração de um ambiente {{site.data.keyword.mfp_full}} a partir do qual é possível desenvolver, testar e operar aplicativos móveis corporativos.<br/><br/> Leia mais sobre operar esse serviço na documentação
<a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} documentation link">{{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}}ícone de serviço"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Use o serviço {{site.data.keyword.mqafull}} para descobrir e configurar serviços de qualidade móveis para seus aplicativos. É possível visualizar métricas de qualidade de alto nível para seus apps móveis para obter uma compreensão rápida dos problemas dos apps com os quais você está trabalhando. Essas métricas incluem informações sobre travamentos, erros, feedback do usuário e impressão do usuário. Ao visualizar essas informações para seus aplicativos, é possível determinar se deve investigar problemas específicos adicionalmente.<br/><br/>
Leia mais sobre operar esse serviço na documentação <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} documentation link">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="ícone de serviço das Notificações Push"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Use o serviço {{site.data.keyword.mobilepushfull}} para enviar e gerenciar notificações push móveis destinadas a plataformas iOS e Android. Esse serviço gerencia o mapeamento dos usuários do aplicativo para seus dispositivos, plataforma de dispositivo e manipula o despacho de notificações push para os dispositivos. com esse serviço, é possível enviar transmissões, unicasts (com base no userID, deviceID) e tags (ou tópicos) baseados nas notificações push para seus usuários de aplicativo móvel.<br/><br/>
Leia mais sobre operar esse serviço na documentação <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} documentation link">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Integrando serviços móveis
{: #services_integration}
É possível integrar seus serviços existentes do
{{site.data.keyword.Bluemix_notm}} Mobile, como o
{{site.data.keyword.cloudant}}, em seu projeto.


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
