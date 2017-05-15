---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visão geral
{: #index}

É possível gerenciar APIs nativamente no {{site.data.keyword.Bluemix}} se elas estiverem associadas a uma ação do {{site.data.keyword.openwhisk_short}} ou a uma lista crescente de serviços {{site.data.keyword.Bluemix_notm}} integrados, como o serviço {{site.data.keyword.appconserviceshort}}. Gerenciar suas APIs permite controlar o uso, aumentar a adoção e rastrear as estatísticas.

Conforme exibido no diagrama a seguir, o gerenciamento de API funciona inserindo um gateway rápido e leve na frente de terminais existentes de nuvem. O gateway, referido como API Gateway no diagrama, é responsável por responder a chamadas API recebidas de aplicativos. O API Gateway fornece um conjunto abrangente de políticas de API para segurança, gerenciamento de tráfego, mediação, aceleração e suporte a protocolo não HTTP.

![Fluxo do API Gateway.](images/bluemix-native-apim-flow_ow.png "Fluxo de gerenciamento de API.")

Ao expor uma API, você a torna disponível para ser usada por outras pessoas. Isso geralmente significa fornecer aos usuários o acesso limitado à API para informações que estão em servidores que você mantém. Esse acesso permite uma experiência de cliente mais transparente para o usuário final porque eles podem acessar as informações diretamente da interface atual.

Há momentos em que você deseja controlar algumas atividades em seus servidores. Por exemplo, se houver muitas solicitações de API em um servidor em um curto período de tempo, o servidor poderá ficar sobrecarregado e encerrar. Para evitar uma situação como essa, é possível gerenciar a taxa das chamadas API usando o gerenciamento de API. O gateway leve que está conectado à API rastreia o número de chamadas para sua API e impinge limites sobre quantas chamadas ele aceita. O gerenciamento de API também permite rastrear o volume de chamadas API de uma origem específica registrando sua chave API. A chave API é uma sequência exclusiva que a equipe de desenvolvimento de API fornece à equipe de consumo de API que permite que o desenvolvedor de API monitore estatísticas sobre as chamadas que as solicitações da equipe de consumo estão gerando.  

Os recursos a seguir estão disponíveis com o gerenciamento de API do {{site.data.keyword.Bluemix_notm}}:
## Analítica de API
{: #basic_analytics notoc}

Se você deseja monetizar o uso de suas APIs, é possível usar o recurso de analítica para rastrear o uso de chamada. Também é possível monitorar o uso para entender como suas APIs estão sendo usadas para que você possa tomar decisões comunicadas sobre como atualizar suas APIs para aumentar a adoção.

É possível visualizar as estatísticas a seguir sobre suas APIs:
* O número de respostas e o tempo médio de resposta na última hora ou seu intervalo de tempo especificado.
* O número de chamadas API por minuto.
* As últimas 100 respostas.

## Limitação de taxa por assinatura (chave API)
{: #rate_limit notoc}

É possível aplicar um limite de taxa para gerenciar o número de chamadas que os aplicativos podem fazer para suas APIs. É possível especificar um limite de taxa para que somente um número permitido de chamadas seja feito por segundo, minuto, hora, para que, por exemplo, seu backend não seja sobrecarregado. É possível configurar isso por API geral ou por chave API.

## OAuth
{: #oauth notoc}

Para parar o uso indesejado dos dados que você fornece, é possível assegurar que somente usuários com a autenticação correta possam acessar suas APIs. É possível controlar o acesso às suas APIs por meio do padrão de autorização OAuth. OAuth é um
protocolo de autorização baseado em token que permite que websites ou aplicativos de terceiros acessem seus
dados sem requerer que o usuário compartilhe informações pessoais.

## CORS
{: #cors notoc}

O CORS permite que os scripts integrados em uma página da web chamem a API entre limites de domínio. Isso beneficia o usuário da API porque permite que a API recupere as informações de outro domínio quando ele é chamado pela API. Sem ativar o CORS, qualquer recuperação de conteúdo é limitada ao mesmo domínio que a solicitação original. Para obter mais informações sobre o CORS e como implementá-lo, veja [Controle de acesso HTTP (CORS) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS.html){: new_window}.

## Opções adicionais de gerenciamento de API
{: #add_mgt_options notoc}

Esses recursos para o gerenciamento de API estão disponíveis na guia Gerenciamento de API do painel do {{site.data.keyword.openwhisk_short}} ou do App Connect. Para soluções de gerenciamento mais complexas, é possível fazer upgrade para o serviço {{site.data.keyword.apiconnect_full}} integral para acessar mais recursos, como analítica detalhada, estratégias de empacotamento para suas APIs ou um portal do desenvolvedor para socializar APIs. Veja [Introdução ao API Connect](https://console.ng.bluemix.net/docs/services/apiconnect/index.html){: new_window} para obter mais informações sobre o serviço {{site.data.keyword.apiconnect_full}}.

Para obter mais informações sobre o upgrade de suas APIs que você está gerenciando no {{site.data.keyword.Bluemix_notm}} para o serviço {{site.data.keyword.apiconnect_short}}, veja [Acessando mais recursos de gerenciamento de API](upgrade.html).

