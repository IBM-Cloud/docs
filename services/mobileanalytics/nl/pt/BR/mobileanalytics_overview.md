---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sobre {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
O serviço {{site.data.keyword.mobileanalytics_full}}
fornece insights do uso do aplicativo-chave e de desempenho para desenvolvedores
de aplicativos móveis e proprietários do aplicativo. Ao usar o
{{site.data.keyword.mobileanalytics_short}},
proprietários e desenvolvedores do aplicativo podem entender o que está
acontecendo no lado do usuário e podem usar este insight para melhor construir
aplicativos que são extremamente relevantes para os usuários e que se
destaquem na verdadeira imensidão de dispositivos móveis. 

{: #overview}  
O serviço inclui o
{{site.data.keyword.mobileanalytics_short}} Console no qual
os desenvolvedores e proprietários de aplicativo podem monitorar o
desempenho do aplicativo móvel, ver estatísticas de uso e
procurar logs do dispositivo.  O {{site.data.keyword.mobileanalytics_short}} fornece SDKs do cliente para iOS 8+ (somente Swift) e Android 4+.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

Com o serviço {{site.data.keyword.mobileanalytics_short}}, é possível:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Obter insight imediato</dt>
		<dd>Veja as métricas de desempenho e uso em tempo real.</dd>
	<dt>Implementar em minutos</dt>
		<dd>Crie uma instância de serviço no
{{site.data.keyword.Bluemix}}, inclua o SDK em seu projeto, cole duas linhas de código em seu aplicativo e prepare-se para
coletar dezenas de métricas predefinidas.</dd>
	<dt>Coletar quaisquer dados desejados</dt>
		<dd>Instrumente aplicativos com eventos customizados, descubra como os usuários estão interagindo com seu aplicativo, rastreie as compras e monitore a atividade do aplicativo.  
</dd>
<dt>Ver métricas para todos os aplicativos em uma visão rápida</dt>
	<dd>O console do {{site.data.keyword.mobileanalytics_short}} oferece gráficos <!-- both -->prontos<!--and custom-->, sem a necessidade de gravar consultas.</dd>
<dt>Concentrar-se no que é importante para você</dt>
	<dd>Filtre as métricas por horário, adaptador, aplicativo, versão do aplicativo, sistema operacional,
versão do sistema operacional ou modelo de dispositivo.</dd>
<dt>Descobrir problemas rapidamente</dt>
	<dd>Monitore o status de travamento. Configure acionadores de alerta sobre métricas críticas e roteie alertas para qualquer terminal REST. </dd>
<dt>Solucionar problemas na causa raiz</dt>
	<dd>Use a criação de log customizada em seu aplicativo e faça upload
dos logs automaticamente e procure-os a partir do console. Realize drill down em eventos de travamento para ver os rastreios de pilha. </dd>
</dl>
 

## Usando métricas e eventos
{: #usingmetrics}

Com as **métricas predefinidas**, é possível responder perguntas como:

* Quantos novos usuários eu tenho?  
* Quantas pessoas estão usando ativamente meu aplicativo?  
* Com que frequência as pessoas estão usando meu aplicativo? 
* Que hora do dia as pessoas estão usando meu aplicativo?  
* Quais modelos de dispositivo meus usuários preferem? 
* Quando deverei descontinuar o suporte para sistemas operacionais legados? 
* Quais aplicativos estão tendo problemas de desempenho?  

Incluindo seus próprios **eventos customizados**, é possível responder perguntas como: 

* Quais recursos são mais e menos usados?  
* Onde os usuários estão entrando e saindo do meu app?  
* Quais atividades os usuários estão visualizando mais?  
* Os usuários estão concluindo fluxos de trabalho no app (por exemplo, funis de conversão)?   

Os logs do lado do cliente e os dados de uso são coletados automaticamente e enviados
para o serviço Mobile Analytics on demand. Os desenvolvedores e administradores podem usar
o painel do serviço {{site.data.keyword.mobileanalytics_short}} para visualizar os
dados que são coletados pelo SDK do cliente.

## Visualização de dados
{: data-visualization}

Todos os dados coletados pelo serviço de analítica podem ser visualizados por meio do painel do {{site.data.keyword.mobileanalytics_short}} que
é acessível no seu painel do {{site.data.keyword.Bluemix_notm}} clicando na
instância do tile de serviço do IBM {{site.data.keyword.mobileanalytics_short}}. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> Além de uma visão rápida de sua analítica móvel, o recurso analítico inclui a capacidade de
executar uma procura bruta nos logs de clientes, dados capturados de travamento do cliente
e quaisquer dados extras que você forneça explicitamente por meio de chamadas de
função de API do cliente que são alimentadas no serviço {{site.data.keyword.mobileanalytics_short}}. 

## Perguntas mais frequentes do {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>O que é o {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>O {{site.data.keyword.mobileanalytics_full}} é um
serviço
que fornece insight em tempo real e histórico sobre como seus
aplicativos móveis são executados e estão sendo usados. Ao usar o
{{site.data.keyword.mobileanalytics_short}}, os
desenvolvedores de aplicativos e proprietários de aplicativos podem
tomar decisões orientadas a dados monitorando tendências em usuários
ativos, sessões, plataformas móveis e travamentos de aplicativos. Também é possível configurar alertas em métricas selecionadas que, uma vez acionadas, enviam mensagens para qualquer terminal REST, incluindo um serviço de push ou seus serviços de sistema de mensagens internas.</dd>
	<dt>O que posso fazer com o
{{site.data.keyword.mobileanalytics_short}} for
{{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>Como um Gerente de produto de aplicativos móveis, é possível ver
quantas pessoas usam seu aplicativo (métricas do usuário) e quando elas
o estão usando (métricas de sessão). Essas informações são
apresentadas como uma série temporal e atualizadas em tempo real para
que você possa ver o efeito das mudanças feitas em seu aplicativo. É
possível filtrar para ver versões específicas do aplicativo ou
sistemas operacionais para tomar decisões de descontinuação e
priorização. </dd>
		<dd>Como um Comerciante de aplicativo móvel, você pode usar métricas
de usuário e de sessão para monitorar participação, gerenciar a
rotatividade e avaliar a efetividade dos esforços de marketing do
aplicativo móvel, observando mudanças ao longo do tempo e
correlacionando com as suas datas de evento.</dd>
		<dd>Como um Desenvolvedor de aplicativos móveis, é possível usar
métricas de travamento para descobrir e resolver problemas de
desempenho do aplicativo móvel antes que eles frustrem os usuários e
prejudiquem a reputação do aplicativo. É possível monitorar a contagem de travamentos e a taxa de travamento do console de analítica, além de priorizar travamentos que estão afetando a maioria dos usuários. É possível configurar alertas para enviar notificações ou executar ações automatizadas quando os
travamentos excedem um determinado limite e é possível solucionar problemas realizando drill down
em instâncias de travamento para ver logs de dispositivo e rastreios de pilha de aplicativos.</dd>
	<dt>Preciso de habilidades de analista de dados para usar o Mobile Analytics?</dt>
		<dd>Não, o {{site.data.keyword.mobileanalytics_short}}
oferece um console de analítica pronto para uso para partes
interessadas nos negócios e para desenvolvedores de aplicativos. Não são necessárias qualificações de consulta.</dd>
	<dt>Posso executar consultas customizadas em meus dados de analítica?</dt>
		<dd>O {{site.data.keyword.mobileanalytics_short}} não permite
consultas customizadas, mas há consideração para este recurso no
futuro.</dd>
	<dt>Como conecto meu aplicativo ao
{{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Faça download de nosso SDK de software livre para iOS ou Android](install-client-sdk.html) ou use
a [API de REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/)
do {{site.data.keyword.mobileanalytics_short}} para outras plataformas. </dd>
	<dt>Em quais regiões do Bluemix o {{site.data.keyword.mobileanalytics_short}} está disponível?</dt>
		<dd>Atualmente, o Mobile Analytics está disponível nos Estados
Unidos - Sul e no Reino Unido. A disponibilidade em outras regiões está
planejada, mas o período ainda não foi determinado.</dd>
	<dt>Quanto custa esse serviço?</dt>
		<dd>Os primeiros 100 milhões de eventos que são coletados a cada mês
são grátis e depois, os eventos custarão US$ 1 por milhão de eventos.</dd>
	<dt>O que é um evento?</dt>
		<dd>Atualmente eventos relatados incluem o início de sessão do
aplicativo, término de sessão do aplicativo (incluindo travamento do
aplicativo), notificações de alerta e entradas de log.</dd>
	<dt>Como posso estimar quanto o serviço vai custar por mês?</dt>
		<dd>Como a precificação depende do número de eventos que são
enviados para o serviço por conta do cliente, a estimativa de
precificação significa estimar eventos.  
<p>
O preço que é cobrado é a soma de eventos de todos os aplicativos que
você conectou ao
{{site.data.keyword.mobileanalytics_short}}. Para um
determinado aplicativo, o número de eventos depende do grau de
instrumentação do que você implementou no aplicativo, do número de
usuários e de quão ativos os usuários são.   
</p>
<p>
Use esta fórmula para estimar o uso: eventos por mês por app =
(usuários por dia) (sessões por usuário por dia) (dias por mês)
(eventos por sessão)
</p>
<p>
Eventos por sessão pode variar amplamente de 2 a várias centenas,
dependendo
de quais chamadas de rede, analítica customizada, captura de log e
definições de alerta o desenvolvedor configurou no aplicativo.
</p>
	<dt>Quanto tempo meus dados de analítica são mantidos?</dt>
		<dd>Os dados são mantidos por pelo menos 30 dias.</dd>
	<dt>Quanto tempo leva para que os dados sejam exibidos no console do {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Os dados no console do {{site.data.keyword.mobileanalytics_short}} são quase em tempo real, o que significa que são exibidos com diferença de segundos dos eventos reais.</dd>
	<dt>Qual é a diferença entre o {{site.data.keyword.mobileanalytics_full}} e a analítica móvel localizada no MobileFirst Platform Foundation?</dt>
		<dd>Usuário e sessão são muito semelhantes nesses dois consoles, mas a analítica que vem com o MobileFirst Platform Foundation contém métricas adicionais e configurações que permitem que os clientes gerenciem seus próprios clusters de analítica no local. Além disso, o console de analítica do MobileFirst Platform Foundation
divide as métricas para adaptadores e procedimentos do adaptador,
enquanto que no
serviço do {{site.data.keyword.mobileanalytics_short}}, essas
métricas são integradas em gráficos e tabelas de solicitação
de rede.</dd>
	<dt>Estou usando o MobileFirst Platform Foundation no local para desenvolver meus apps, mas não quero hospedar meu próprio cluster de analítica. Posso usar o {{site.data.keyword.mobileanalytics_full}} no lugar?</dt>
		<dd>Sim. Você tem duas opções: se estiver usando o MobileFirst
Platform Foundation 7.x ou 8.0 e seus apps forem instrumentados
com os SDKs do MobileFirst Platform,
poderá configurar seu servidor MobileFirst para relatar dados de
analítica para o {{site.data.keyword.mobileanalytics_short}} for
{{site.data.keyword.Bluemix_notm}}. Leia a postagem do blog [Configurando os serviços Mobile Analytics e Mobile Foundation do Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/ "Ícone de link externo"){: new_window} para obter detalhes. Como alternativa, é possível instrumentar seus apps usando o {{site.data.keyword.mobileanalytics_short}} SDK do {{site.data.keyword.Bluemix_notm}} e relatar diretamente para o serviço {{site.data.keyword.mobileanalytics_short}}.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# rellinks
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [SDK do
Android![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Ícone de link externo"){: new_window} 
* [SDK do iOS![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core "Ícone de link externo"){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
