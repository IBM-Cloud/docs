---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# Sobre {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
Última atualização: 29 de agosto de 2016
{: .last-updated}

{: shortdesc}
O serviço {{site.data.keyword.mobileanalytics_full}} fornece insights chave de uso e desempenho de aplicativo para desenvolvedores de aplicativo móvel e proprietários de aplicativo. Usando o {{site.data.keyword.mobileanalytics_short}}, os proprietários e desenvolvedores de app podem entender o que está acontecendo no lado do usuário e podem usar este insight para construir apps melhores que sejam extremamente relevantes para os usuários e que se destaquem no verdadeiro mundo de apps móveis. 

{: #overview}  
O serviço inclui o {{site.data.keyword.mobileanalytics_short}} Console no qual os desenvolvedores e proprietários de aplicativo podem monitorar o desempenho do aplicativo móvel, ver estatísticas de uso e procurar logs do dispositivo.  O {{site.data.keyword.mobileanalytics_short}} fornece SDKs do cliente para iOS 8+ (somente Swift) e Android 4+.

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
		<dd>Crie uma instância de serviço no {{site.data.keyword.Bluemix}}, inclua o SDK em seu projeto, cole duas linhas de código no aplicativo e prepare-se para coletar dezenas de métricas predefinidas.</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>Ver métricas para todos os aplicativos em uma visão rápida</dt>
	<dd>O console do {{site.data.keyword.mobileanalytics_short}} oferece gráficos <!-- both -->prontos<!--and custom-->, sem a necessidade de gravar consultas.</dd>
<dt>Concentrar-se no que é importante para você</dt>
	<dd>Filtre as métricas por horário, adaptador, aplicativo, versão do aplicativo, S.O., versão do S.O ou modelo de dispositivo.</dd>
<dt>Descobrir problemas rapidamente</dt>
	<dd>Monitore o status de travamento. Configure acionadores de alerta sobre métricas críticas e roteie alertas para qualquer terminal REST. </dd>
<dt>Solucionar problemas na causa raiz</dt>
	<dd>Use a criação de log customizada em seu app, faça upload dos logs automaticamente e procure-os a partir do console. Realize drill down em eventos de travamento para ver os rastreios de pilha. </dd>
</dl>
 

## Usando métricas e eventos
{: #usingmetrics}

Com as **métricas predefinidas**, é possível responder perguntas como:

* Quantos novos usuários eu tenho?  
* Quantas pessoas estão usando ativamente meu app?  
* Com que frequência as pessoas estão usando meu app? 
* Em que horário do dia as pessoas estão usando meu app?  
* Quais modelos de dispositivo meus usuários preferem? 
* Quando eu devo descontinuar o suporte para sistemas operacionais anteriores? 
* Quais apps estão tendo problemas de desempenho?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## Perguntas mais frequentes do {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>O que é o {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} é um serviço que fornece insight em tempo real e histórico sobre como seus apps móveis são executados e estão sendo usados.  Usando o {{site.data.keyword.mobileanalytics_short}}, desenvolvedores e proprietários de apps podem tomar decisões orientadas a dados, monitorando tendências em usuários ativos, sessões, plataformas móveis e travamentos de apps. Também é possível configurar alertas em métricas selecionadas que, uma vez acionadas, enviam mensagens para qualquer terminal REST, incluindo um serviço de push ou seus serviços de sistema de mensagens internas.</dd>
	<dt>O que posso fazer com o {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} beta?</dt>
		<dd>Como um Gerente de produto de app móvel, é possível ver quantas pessoas usam seu app (métricas do usuário) e quando elas estão usando (métricas de sessão).  Essas informações são apresentadas como uma série temporal e são atualizadas em tempo real para que você possa ver o efeito de mudanças feitas em seu app.  É possível filtrar para ver versões específicas do app ou sistemas operacionais para tomar decisões de descontinuação e priorização. </dd>
		<dd>Como um Comerciante de app móvel, é possível usar métricas de usuário e de sessão para monitorar participação, gerenciar a rotatividade e avaliar a eficácia dos esforços de marketing do app móvel, observando mudanças ao longo do tempo e correlacionando com suas datas de eventos.</dd>
		<dd>Como um Desenvolvedor de app móvel, é possível usar métricas de travamento para descobrir e resolver problemas de desempenho do app móvel antes que eles frustrem os usuários e prejudiquem a reputação do app. É possível monitorar a contagem de travamentos e a taxa de travamento do console de analítica, além de priorizar travamentos que estão afetando a maioria dos usuários. É possível configurar alertas para enviar notificações ou executar ações automatizadas quando os travamentos excedem um determinado limite e solucionar problemas realizando drill down em instâncias de travamento, para ver logs de dispositivo e rastreios de pilha do app.</dd>
	<dt>Preciso de habilidades de analista de dados para usar o Mobile Analytics?</dt>
		<dd>Não, o {{site.data.keyword.mobileanalytics_short}} oferece um console de analítica pronto para usar para partes interessadas nos negócios e para desenvolvedores de app. Não são necessárias qualificações de consulta.</dd>
	<dt>Posso executar consultas customizadas em meus dados de analítica?</dt>
		<dd>O {{site.data.keyword.mobileanalytics_short}} beta não permite consultas customizadas, mas há consideração para este recurso no futuro.</dd>
	<dt>Como conecto meu app ao {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Faça download de nosso software livre SDK for iOS ou Android](install-client-sdk.html) ou use a [API REST](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/) do {{site.data.keyword.mobileanalytics_short}} para outras plataformas. </dd>
	<dt>Em quais regiões do Bluemix o {{site.data.keyword.mobileanalytics_short}} está disponível?</dt>
		<dd>No momento dessa composição, o Mobile Analytics está disponível no sul dos EUA e no Reino Unido. A disponibilidade em outras regiões está planejada, mas o período ainda não foi determinado.</dd>
	<dt>Quanto custa esse serviço?</dt>
		<dd>O serviço é gratuito para beta.</dd>
	<dt>Quanto tempo meus dados de analítica são mantidos?</dt>
		<dd>Para beta, os dados são mantidos por pelo menos 30 dias.</dd>
	<dt>Quanto tempo leva para que os dados sejam exibidos no console do {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Os dados no console do {{site.data.keyword.mobileanalytics_short}} são quase em tempo real, o que significa que são exibidos com diferença de segundos dos eventos reais.</dd>
	<dt>Qual é a diferença entre o {{site.data.keyword.mobileanalytics_full}} e a analítica móvel localizada no MobileFirst Platform Foundation?</dt>
		<dd>Usuário e sessão são muito semelhantes nesses dois consoles, mas a analítica que vem com o MobileFirst Platform Foundation contém métricas adicionais e configurações que permitem que os clientes gerenciem seus próprios clusters de analítica no local. Além disso, o console de analítica do MobileFirst Platform Foundation divide as métricas para adaptadores e procedimentos do adaptador, enquanto que no serviço {{site.data.keyword.mobileanalytics_short}}, estamos planejando integrar essas métricas em gráficos e tabelas de solicitação de rede no serviço {{site.data.keyword.mobileanalytics_short}} (pós-beta).</dd>
	<dt>Estou usando o MobileFirst Platform Foundation no local para desenvolver meus apps, mas não quero hospedar meu próprio cluster de analítica. Posso usar o {{site.data.keyword.mobileanalytics_full}} no lugar?</dt>
		<dd>Sim. Você tem duas opções aqui: se estiver usando o MobileFirst Platform Foundation 7.x ou 8.0 e seus apps forem instrumentados com os SDKs do MobileFirst Platform, será possível configurar seu servidor MobileFirst para relatar dados de analítica para o {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}. Leia a postagem do blog [Configurando os serviços Mobile Analytics e Mobile Foundation do Bluemix](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/) para obter detalhes. Como alternativa, é possível instrumentar seus apps usando o {{site.data.keyword.mobileanalytics_short}} SDK do {{site.data.keyword.Bluemix_notm}} e relatar diretamente para o serviço {{site.data.keyword.mobileanalytics_short}}.</dd>
	<dt>Estou tentando usar o {{site.data.keyword.mobileanalytics_short}} e vejo um espaço em branco onde meus gráficos deveriam estar. O que está havendo?</dt>
		<dd>Provavelmente você está usando a interface de visualização Clássica do {{site.data.keyword.Bluemix_notm}}. A visualização Clássica foi descontinuada, portanto o {{site.data.keyword.mobileanalytics_short}} beta é executado na nova interface do {{site.data.keyword.Bluemix_notm}}. Se estiver na visualização Clássica, você verá um link no cabeçalho do {{site.data.keyword.Bluemix_notm}} dizendo "Tente o novo {{site.data.keyword.Bluemix_notm}}!". Clique nesse link para usar a nova interface.</dd>
</dl>


# rellinks
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
