---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_local_notm}}
{: #local}


O {{site.data.keyword.Bluemix_local}} traz a eficiência e a agilidade da plataforma baseada em nuvem do {{site.data.keyword.Bluemix_notm}} para seu datacenter. Com o {{site.data.keyword.Bluemix_local_notm}}, é possível proteger suas cargas de trabalho mais sensíveis no firewall de sua empresa, enquanto permanece estavelmente conectado e em sincronia com o {{site.data.keyword.Bluemix_notm}} Public.
{:shortdesc}

A IBM® utiliza operações em nuvem como um serviço para monitorar e manter seu ambiente, para que você possa se concentrar na construção de apps e serviços que são executados no topo do ambiente. O {{site.data.keyword.IBM_notm}} também manipula atualizações de plataforma, para que você possa se concentrar nos negócios.

Os ambientes do {{site.data.keyword.Bluemix_local_notm}} possuem as mesmas normas de segurança que o {{site.data.keyword.Bluemix_notm}} público em termos de segurança operacional. Você fornece o hardware e a infraestrutura, que fornece controle sobre a [segurança](/docs/security/index.html#localplatformsecurity) física de infraestrutura. O acesso do desenvolvedor ao ambiente local do {{site.data.keyword.Bluemix_notm}} é controlado por suas políticas de LDAP, que podem ser configuradas pela equipe {{site.data.keyword.Bluemix_notm}} quando configuram seu ambiente. No ambiente local, usando a página Administração, é possível [gerenciar usuários e permissões](/docs/admin/index.html#oc_useradmin).

O {{site.data.keyword.Bluemix_local_notm}} é fornecido com todos os tempos de execução do {{site.data.keyword.Bluemix_notm}} incluídos e 64 GB de memória de cálculo.

Além disso, há um conjunto de serviços que estão disponíveis como serviços do {{site.data.keyword.Bluemix_local_notm}}. Revise a tabela a seguir para ver o que está incluído e o que está disponível para compra.

| **Tipo** | **Nome** | **Descrição** |
|----------|----------|-----------------|
|Incluído | [Tempos de execução do {{site.data.keyword.Bluemix_notm}}](/docs/cfapps/runtimes.html) | Use tempos de execução para colocar seu app funcionando rapidamente, sem necessidade de configurar e gerenciar as máquinas e os sistemas operacionais. Todos os tempos de execução do {{site.data.keyword.Bluemix_notm}} estão disponíveis para uso em sua instância do {{site.data.keyword.Bluemix_notm}} Local.|
|Incluído | [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html)| Aumentar ou diminuir dinamicamente a capacidade de cálculo do aplicativo com base em políticas. Com esse serviço, você tem uso ilimitado em seu ambiente do {{site.data.keyword.Bluemix}} Local.|
|Opcional | [{{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect/index.html) | O {{site.data.keyword.apiconnect_long}} integra o {{site.data.keyword.APIM}} e o IBM StrongLoop em uma única oferta que fornece uma solução abrangente para criar, executar, gerenciar e impingir APIs e microsserviços. |
|Opcional | [{{site.data.keyword.containershort}}](/docs/containers/container_index.html) | Execute os contêineres do Docker no {{site.data.keyword.Bluemix_notm}} Local. Contêineres são objetos de software virtuais que incluem todos os elementos que um aplicativo precisa executar. Um contêiner tem os benefícios do isolamento e da alocação de recursos, mas é mais móvel e eficiente do que, por exemplo, uma máquina virtual. Para obter informações sobre requisitos de hardware, consulte [IBM {{site.data.keyword.containershort}} em {{site.data.keyword.Bluemix_notm}} Dedicated e Bluemix Local](/docs/containers/container_dl.html). |
|Opcional | [{{site.data.keyword.datacshort}}](/docs/services/DataCache/index.html#data_cache) | Esse serviço fornece uma grade de dados da memória que suporta cenários de armazenamento em cache distribuído para seus apps. Inclui 50 GB de cache na memória. |
| Opcional (Beta) | [Registro de log](/docs/monitoringandlogging/cfapps_ml_logs_dedicated_ov.html#container_ml_logs_dedicated_ov) | Fornece logs para os aplicativos Cloud Foundry em sua interface com o usuário do {{site.data.keyword.Bluemix_notm}} e logs pesquisáveis e painéis em Kibana. |
|Opcional | [{{site.data.keyword.mobilepush}}](/docs/services/mobilepush/index.html) | O {{site.data.keyword.mobilepush}} é um serviço que você pode usar para enviar notificações para iOS e dispositivo Android. É possível direcionar notificações para todos os usuários do aplicativo ou para um conjunto específico de usuários e dispositivos usando tags. É possível administrar dispositivos, tags e assinaturas. É possível também usar um SDK (kit de desenvolvimento de software) e interfaces de programação de aplicativo (APIs) Representational State Transfer (REST) para desenvolver ainda mais seus aplicativos cliente. |
|Opcional | [{{site.data.keyword.sescashort}}](/docs/services/SessionCache/index.html#session_cache) | Para maior redundância, o {{site.data.keyword.sescashort}} fornece uma réplica de uma sessão armazenada no cache. Portanto, no caso de uma indisponibilidade de energia, seu aplicativo cliente manterá acesso à sessão no cache. O serviço suporta cenários de armazenamento em cache de sessão para aplicativos móveis e da web. |
|Opcional | [{{site.data.keyword.iot_short}}](/docs/services/IoT/index.html) | Esse serviço permite que os apps se comuniquem e consumam dados coletados por seus dispositivos conectados, sensores e gateways. A oferta de base local inclui um ambiente inicial que permite executar uma versão privada do IBM {{site.data.keyword.iot_short}} dentro do ambiente local com uma capacidade de 100.000 dispositivos ou aplicativos conectados simultaneamente e 1.6 TB de troca de dados. |
{: caption="Table 1. Local services and runtimes" caption-side="top"}
{: #table01}


Há componentes opcionais que estão disponíveis para você comprar para escalar e ampliar a capacidade de seus recursos e serviços. É possível comprar qualquer um desses componentes entrando em contato com a equipe de vendas; acesse [Contate-nos](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs) para obter informações sobre como contatar um representante de vendas. Para aumentar seu plano para um serviço, é possível selecionar o plano a partir do ladrilho do serviço em seu catálogo.

| **Nome** | **Descrição** |
|----------|-----------------|
|{{site.data.keyword.Bluemix_notm}} Local {{site.data.keyword.apiconnect_short}} Professional 5 milhões de Chamadas API | Um ambiente que permite executar uma versão privada do {{site.data.keyword.apiconnect_short}} com uma capacidade de 5 milhões de Chamadas API por mês, destinadas para projetos de API do departamento. |
|{{site.data.keyword.Bluemix_notm}} Local {{site.data.keyword.apiconnect_short}} Professional aumento de 100 mil Chamadas API| Uma extensão do ambiente do {{site.data.keyword.apiconnect_short}} Professional, para fornecer capacidade adicional de 100 mil chamadas API por mês. |
|{{site.data.keyword.Bluemix_notm}} Local {{site.data.keyword.apiconnect_short}} Enterprise 25 milhões de Chamadas API | Um ambiente que permite executar uma versão privada do {{site.data.keyword.apiconnect_short}} com uma capacidade de 25 milhões de Chamadas API por mês, destinadas para projetos de API em toda a empresa. |
|{{site.data.keyword.Bluemix_notm}} Local {{site.data.keyword.apiconnect_short}} Enterprise aumento de 100 mil Chamadas API | Uma extensão do ambiente do {{site.data.keyword.apiconnect_short}} Enterprise, para fornecer capacidade adicional de 100 mil Chamadas API por mês. |
|Aumento de capacidade de 50 GB de Dados e Sessão do {{site.data.keyword.Bluemix_notm}} | Um ambiente que permite implementar e executar as instâncias de Cache de Dados e Cache de Sessão até uma capacidade acumulativa de 50 GB. |
|Aumento incremental do {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.iot_short}} Local | Um ambiente adicional para a oferta de serviço de base do {{site.data.keyword.iot_short}} Local, que permite executar uma versão privada do {{site.data.keyword.iot_short}} dentro do ambiente local com uma capacidade de 100.000 dispositivos ou aplicativos conectados simultaneamente e 0.5 TB de troca de dados. |
|{{site.data.keyword.IBM_notm}} Instância de complemento do {{site.data.keyword.mobilepush}} Local | Um ambiente que permite a implementação e execução da instância do {{site.data.keyword.mobilepush}} com a capacidade para aceitar 300 solicitações adicionais por segundo. |
{: caption="Table 2. Optional services components for purchase" caption-side="top"}
{: #table02}

| **Nome** | **Descrição** |
|----------|-----------------|
|Tempos de execução do Cloud Foundry local com 64 GB de capacidade  | Ambiente dos tempos de execução do Cloud Foundry com 64 GB de capacidade de tempo de execução. |
|Tempos de execução do Cloud Foundry local com aumento de 16 GB de capacidade  | Uma extensão do ambiente dos tempos de execução do Cloud Foundry para fornecer uma capacidade extra de 16 GB de tempo de execução. |
|Aumento de capacidade de 16 GB do {{site.data.keyword.containerlong}} local  | Uma extensão do ambiente do {{site.data.keyword.containerlong}} para fornecer uma capacidade extra de 16 GB. |
|{{site.data.keyword.containerlong}} local de 64 GB de capacidade  | Ambiente do {{site.data.keyword.containerlong}} com 64 GB de capacidade. |
{: caption="Table 3. Optional platform add-on components for purchase" caption-side="top"}
{: #table03}

**Nota**: Os componentes do {{site.data.keyword.Bluemix_notm}} Local podem indicar uma capacidade configurada específica, como gigabytes ou transações por segundo. Como a capacidade real na prática para qualquer configuração do serviço de nuvem varia dependendo de vários fatores, a capacidade real pode ser mais ou menos que a capacidade configurada.

### Catálogo organizado
{: #cataloglocal}

O {{site.data.keyword.Bluemix_local_notm}} inclui um catálogo privado que reúne serviços aprovados em suas implementações públicas e locais. É possível publicar e gerenciar o acesso aos seus próprios serviços através do catálogo do {{site.data.keyword.Bluemix_notm}}. Você tem a opção de decidir quais serviços públicos atendem as necessidades de seus negócios, com base em sua privacidade de dados e nos critérios de segurança.

Se você tiver uma instância privada de um serviço do {{site.data.keyword.Bluemix_notm}} para seu ambiente local, verá uma tag "Local" com os nomes do serviço em sua visualização de administração do catálogo. Da mesma forma, se ela for um serviço customizado, significando que você usou um broker de serviço para criá-la, você verá "Customizado" listado com o nome do serviço. Todos os outros serviços listados que não possuem uma tag "local" ou "customizado" estão disponíveis usando a organização do {{site.data.keyword.Bluemix_notm}} Public. Serviços organizados fornecem a função para criar aplicativos híbridos que consistem em serviços públicos e privados.

|Serviço	|Disponível na região sul dos EUA	|Disponível na região do Reino Unido na Europa |Disponível na região de Sydney, na Austrália|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|Sim	   	|Sim  		|Sim|
|{{site.data.keyword.alertnotificationshort}}	|Sim		|Sim		|Sim	|
|{{site.data.keyword.apiconnect_short}}         |Sim            |Sim            |Sim  |
|{{site.data.keyword.appseccloudshort}}		|Sim		|Sim		|Sim |
|{{site.data.keyword.apiconnect_short}} 	|Sim   	 	|Sim  	 	|Sim   |
|Verificador de acessibilidade automatizado |Sim       |Sim    |Sim   |
|{{site.data.keyword.rules_short}}		|Sim		|Sim		|Sim |
|{{site.data.keyword.iotmapinsights_short}}    |Sim  |Sim  |Sim  |
|{{site.data.keyword.conversationshort}}  |Sim  |Sim  |Sim  |
|{{site.data.keyword.dashdbshort}}		|Sim		|Sim		|Sim |
|{{site.data.keyword.dataworks_short}}		|Sim		|Sim		|Não|
|{{site.data.keyword.DB2OnCloud_short}}		|Sim		|Sim		|Sim |
|Verificador de conteúdo digital |Sim  |Sim  |Sim  |
|{{site.data.keyword.documentconversionshort}}	|Sim		|Sim		|Sim|
|{{site.data.keyword.iotdriverinsights_short}}  |Sim |Sim  |Sim  |
|{{site.data.keyword.geospatialshort_Geospatial}}	|Sim	|Sim		|Sim |
|{{site.data.keyword.GlobalizationPipeline_short}}	|Sim		| Sim		| Sim |
|{{site.data.keyword.identitymixershort}}		|Sim		|Sim		|Sim|
|{{site.data.keyword.iot4auto_short}} |Sim   |Sim  |Sim  |
|{{site.data.keyword.iotelectronics}}  |Sim  |Sim  |Não |
|{{site.data.keyword.iotinsurance_short}} |Não   |Não   |Sim  |
|{{site.data.keyword.twittershort}}		|Sim		|Sim		|Sim|
|{{site.data.keyword.languagetranslationshort}}	|Sim		|Sim		|Sim |
|{{site.data.keyword.languagetranslatorshort}} |Sim  |Sim  |Sim  |
|{{site.data.keyword.dwl_short}}  |Sim  |Sim  |Não  |
|{{site.data.keyword.eventhubshort}}		|Sim		|Não		|Não|
|{{site.data.keyword.messagehub}}		|Sim		|Sim		|Não|
|{{site.data.keyword.manda}}			|Sim		|Sim		|Sim |
|{{site.data.keyword.amashort}}			|Sim		|Sim		|Sim |
|{{site.data.keyword.mqa}}			|Sim		|Sim		|Sim |
|{{site.data.keyword.mql}}			|Não		|Não		|Sim |
|{{site.data.keyword.nlclassifierlshort}} 	|Sim 		|Sim 		|Sim|
|{{site.data.keyword.personalityinsightsshort}}	|Sim		|Sim		|Sim|
|{{site.data.keyword.pm_short}}			|Sim		|Sim		|Não |
|{{site.data.keyword.mobilepush}}		|Sim		|Sim		|Sim |
|{{site.data.keyword.retrieveandrankshort}}	|Sim 		|Sim 		|Sim|
|{{site.data.keyword.runbook_short}}		|Sim		|Sim		|Sim|
|{{site.data.keyword.SecureGateway}}		|Sim		|Sim		|Sim |
|{{site.data.keyword.ssofull}}			|Sim		|Não		|Não|
|{{site.data.keyword.speechtotextshort}}	|Sim 		|Sim	 	|Sim|
|{{site.data.keyword.streaminganalyticsshort}}	|Sim		|Sim		|Sim |
|{{site.data.keyword.texttospeechshort}} 	|Sim 		|Sim	 	|Sim|
|{{site.data.keyword.toneanalyzershort}} 	|Sim 		|Sim 		|Sim|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Sim		|Sim		|Sim|
|{{site.data.keyword.visualrecognitionshort}}	|Sim 		|Sim	 	|Sim|
|{{site.data.keyword.iot_short}}		|Sim		|Sim		|Não|
|{{site.data.keyword.weather_short}}		|Sim		|Sim		|Sim|
|{{site.data.keyword.workloadscheduler}}	|Sim		|Sim		|Sim |
{: caption="Table 4. Services available for syndication from {{site.data.keyword.Bluemix_notm}} Public by region" caption-side="top"}
{: #table04}

**Observação**: os serviços de terceiros não são incluídos na tabela. Verifique seu catálogo para obter as opções de serviço de terceiros.


## Arquitetura do {{site.data.keyword.Bluemix_local_notm}}
{: #localarch}

O {{site.data.keyword.Bluemix_local_notm}} fica em uma infraestrutura virtualizada que está atrás do firewall Corporativo, fornecendo a infraestrutura em nuvem mais segura e com maior desempenho. A {{site.data.keyword.IBM_notm}} instala, monitora remotamente e gerencia o {{site.data.keyword.Bluemix_local_notm}} em seu datacenter por meio da tecnologia de [Retransmissão](#localrelay) da {{site.data.keyword.IBM_notm}}. A arquitetura lógica na [Figura 1](#figure01) descreve como o {{site.data.keyword.Bluemix_notm}} está configurado em seu ambiente local e como a {{site.data.keyword.IBM_notm}} mantém sua instância local:

![Arquitetura do {{site.data.keyword.Bluemix_local_notm}}.](images/bmlocal_arch.png "Diagrama de arquitetura do Bluemix Local") 

Figura 1. Arquitetura do {{site.data.keyword.Bluemix_local_notm}}
{: #figure01}

A máquina virtual de concepção (VM de concepção) é executada na infraestrutura virtualizada corporativa sob o firewall corporativo. A VM de concepção cria uma conexão de rede de saída para o centro de Operações da {{site.data.keyword.IBM_notm}} por meio da tecnologia de retransmissão da {{site.data.keyword.IBM_notm}}. A retransmissão executa várias funções e é descrita na seção [Retransmissão](#localrelay) a seguir.

Os componentes da plataforma do {{site.data.keyword.Bluemix_notm}} e os recursos principais que suportam os componentes da plataforma são executados em uma rede local virtual (VLAN) privada e isolada. O {{site.data.keyword.Bluemix_local_notm}} usa uma VLAN para a sub-rede privada. O uso de uma sub-rede privada em vez de uma VLAN pública é mais seguro e pode ajudar a evitar problemas de roteamento. O conjunto de recursos principais que constituem e suportam a plataforma inclui o seguinte:

<dl>
<dt>Plataforma</dt>
<dd>No mínimo, a plataforma consiste em componentes do Cloud Foundry e alguns serviços de aplicativos locais. O {{site.data.keyword.Bluemix_notm}} fornece o Cloud Foundry e ambientes de cálculo baseado no {{site.data.keyword.containerlong}}. Uma empresa pode ter um ou ambos os ambientes de cálculo configurados.<br>
Uma empresa também pode incluir serviços de aplicativos locais adicionais.<br>
<p>Consulte [Componentes opcionais para compra: complementos de serviços](#table02) e [Componentes opcionais para compra: complementos de plataforma](#table03) para serviços e recursos de cálculo adicionais que podem ser incluídos.</p>
</dd>
<dt>{{site.data.keyword.Bluemix_notm}} Public</dt>
<dd>
Um ambiente do {{site.data.keyword.Bluemix_local_notm}} pode ter uma conexão de saída para uma região do {{site.data.keyword.Bluemix_notm}} Public. Uma conexão para público ativa a organização de serviços públicos no catálogo local. A organização do serviço {{site.data.keyword.Bluemix_notm}} Public fornece um método conveniente para os desenvolvedores construírem aplicativos hospedados no ambiente do {{site.data.keyword.Bluemix_local_notm}} da empresa, bem como acesso a serviços em execução no {{site.data.keyword.Bluemix_notm}} Public. Veja a lista de serviços {{site.data.keyword.IBM_notm}} que podem ser organizados a partir do {{site.data.keyword.Bluemix_notm}} na seção [Catálogo organizado](#cataloglocal).
</dd>
<dt>Operações da {{site.data.keyword.IBM_notm}}</dt>
<dd>
A {{site.data.keyword.IBM_notm}} gerencia, monitora e mantém a plataforma local e os serviços locais, para que seja possível concentrar-se nos aplicativos inovadores. A equipe de Operations Support Services (OSS) da {{site.data.keyword.IBM_notm}} executa operações usando uma conexão de túnel VPN da VM de concepção para a rede de Operações da {{site.data.keyword.IBM_notm}}.
</dd>
<dt>Corporativo</dt>
<dd>
O ambiente de rede corporativa tem um link de rede bidirecional para o {{site.data.keyword.Bluemix_local_notm}}. Isso permite que os aplicativos hospedados no {{site.data.keyword.Bluemix_local_notm}} acessem serviços e recursos na empresa, incluindo origens de dados e serviços corporativos. O link de rede também permite que o {{site.data.keyword.Bluemix_local_notm}} use LDAP para autenticação de seus desenvolvedores e administradores.
</dd>
<dt>Serviços Locais</dt>
<dd>Um conjunto de serviços está disponível para ser usado privativamente no ambiente do {{site.data.keyword.Bluemix_local_notm}}. Geralmente, você decide quais serviços deseja para seu ambiente antes da implementação pela equipe do {{site.data.keyword.IBM_notm}}. Para obter uma lista de serviços disponíveis, acesse [Serviços e tempos de execução locais](#table01).
</dd>
<dt>DataPower
Gateway</dt>
<dd>
Os dispositivos do {{site.data.keyword.IBM_notm}} DataPower Gateway fornecem acesso a domínios de aplicativos do {{site.data.keyword.Bluemix_notm}}. Esses dispositivos se conectam à sua rede intranet e à rede privada do {{site.data.keyword.Bluemix_notm}}, fornecendo um gateway seguro para a implementação do {{site.data.keyword.Bluemix_notm}}. Os desenvolvedores, que estão implementando apps e serviços, obtêm acesso de sua intranet por meio desse gateway. Os usuários dos aplicativos obterão acesso por meio dos dispositivos DataPower, bem como seus administradores.
</dd>
<dt>Inteligência de segurança</dt>
<dd><p>A {{site.data.keyword.IBM_notm}} usa a QRadar Security Intelligence Platform para fornecer uma arquitetura unificada para integrar diversos componentes chave. Esses componentes incluem gerenciamento de informações e eventos de segurança, gerenciamento de log, detecção de anomalias, perícia de incidentes e gerenciamento de configuração vulnerabilidade. O {{site.data.keyword.Bluemix_notm}} também usa o {{site.data.keyword.IBM_notm}} QRadar Security Information and Event Management (SIEM) para monitorar as ações de usuário privilegiado e as tentativas de login bem-sucedidas e malsucedidas de desenvolvedores de aplicativos. Os relatórios do QRadar fornecem visibilidade ao cliente, usando a seção Relatórios e Logs na página Administração. Para obter informações sobre relatórios de segurança, consulte [Visualizando relatórios](/docs/admin/index.html#oc_report).</p>
<p>O {{site.data.keyword.IBM_notm}} BigFix assegura que as correções para sistemas operacionais sejam aplicadas em frequências apropriadas. O processo de correção é automatizado e o planejamento é acordado entre o Cliente e a IBM. Para obter informações sobre manutenção e upgrades, consulte [Mantendo sua instância local](index.html#maintainlocal).</p>
</dd>
</dl>

Seus apps são implementados dentro de contêineres virtuais que são executados em máquinas virtuais do Cloud Foundry. Todos os componentes do Cloud Foundry, como controladores de nuvem, gerenciadores de funcionamento, roteadores e Droplet Execution Agents (DEAs) são implementados quando o {{site.data.keyword.Bluemix_notm}} for configurado. Os vários componente de gerenciamento do {{site.data.keyword.Bluemix_notm}} também são incluídos na implementação do {{site.data.keyword.Bluemix_notm}}.

Para obter informações sobre as especificações de rede e os requisitos de infraestrutura, acesse [Requisitos de infraestrutura do {{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#localinfra).

### Retransmitir
{: #localrelay}

A retransmissão é o link seguro entre a rede corporativa e as Operações em nuvem da {{site.data.keyword.IBM_notm}}. O tráfego por meio da conexão de retransmissão é uma atividade automatizada para serviço e manutenção da plataforma, dos recursos de cálculo e dos serviços do {{site.data.keyword.Bluemix_local_notm}} para suas instâncias. O tráfego por meio da conexão de retransmissão pode ser categorizado conforme a seguir:

* monitoramento e eventos
* inteligência de segurança
* implementações e atualizações
* determinação de problema e correções
* manutenção emergencial

<dl>
<dt>
Monitoramento e eventos
</dt>
<dd>
Os recursos de monitoramento e de evento são implementados em seu datacenter. Os dados do aplicativo permanecem em seu datacenter.<br>
O tráfego por meio da conexão de retransmissão inclui o recurso de monitoramento que é usado por Operações da {{site.data.keyword.IBM_notm}} para executar o monitoramento de funcionamento e para concluir a determinação de problema quando necessário.<br>
<p>Os dados sensíveis não são incluídos nas informações de monitoramento, significando nenhuma senha, nenhum dado do aplicativo, nenhum log do aplicativo e nenhuma chave. O tráfego por meio da retransmissão inclui fluxos da VM de concepção para o centro de Operações da {{site.data.keyword.Bluemix_notm}}.</p>
</dd>
<dt>
Security Intelligence
</dt>
<dd>
A {{site.data.keyword.IBM_notm}} usa a QRadar Security Intelligence Platform para fornecer uma arquitetura unificada para integrar diversos componentes chave. Esses componentes incluem gerenciamento de informações e eventos de segurança, gerenciamento de log, detecção de anomalias, perícia de incidentes e gerenciamento de configuração vulnerabilidade.<br>
<p>O {{site.data.keyword.Bluemix_notm}} também usa o {{site.data.keyword.IBM_notm}} QRadar Security Information and Event Management (SIEM) para monitorar as ações de usuário privilegiado e as tentativas de login bem-sucedidas e malsucedidas.</p>
<p>Os relatórios do QRadar fornecem visibilidade ao administrador do {{site.data.keyword.Bluemix_notm}} sobre eventos e dados do evento usando a seção Relatórios e Logs da página Administração. Os relatórios do QRadar são gerados em uma base regular, diária ou mensal dependendo do tipo de relatório. Todos os relatórios são retidos por 90 dias no console de administração para a sua recuperação. Após esses 90 dias, os relatórios estarão disponíveis por solicitação a partir do {{site.data.keyword.IBM_notm}} por 9 meses. No total, os relatórios estarão disponíveis para recuperação por até 1 ano.</p>
<p>Os dados do aplicativo não são incluídos no tráfego consumido pelo QRadar. Os únicos dados que podem potencialmente ser considerados como sensíveis são os IDs de usuário para os relatórios de tentativas de login e os endereços IP de alguns componentes do {{site.data.keyword.Bluemix_notm}}.
O tráfego por meio da retransmissão inclui os fluxos entre o QRadar Event Processor no {{site.data.keyword.Bluemix_local_notm}} e um QRadar Console no centro de Operações da {{site.data.keyword.IBM_notm}}.</p>
</dd>
<dt>
Atualizações de implementação e manutenção
</dt>
<dd>
Exceto para a instalação inicial da VM de concepção que é instalada no estágio inicial do processo de implementação, a implementação da maioria dos outros componentes é automatizada usando o UrbanCode Deploy.<br>
<p>Para a atividade de implementação, o UrbanCode Deploy depende do [BOSH ![Ícone de link externo](../icons/launch-glyph.svg)](https://bosh.cloudfoundry.org/){:new_window}, com os componentes do BOSH estando entre os primeiros componentes implementados a partir da VM de concepção. O recurso de entrega contínua do UrbanCode Deploy é usado para entregar atualizações de plataforma por meio de um processo de teste e validação consistente.</p>
<p>Os scripts e pacotes são transferidos do centro de Operações da {{site.data.keyword.IBM_notm}} para a plataforma local do {{site.data.keyword.Bluemix_notm}} por meio da Retransmissão.</p>
</dd>
<dt>
Correções
</dt>
<dd>
O {{site.data.keyword.IBM_notm}} BigFix assegura que as atualizações de segurança para sistemas operacionais sejam aplicadas em frequências apropriadas. O processo de correção é automatizado e o planejamento é acordado entre o Cliente e a IBM.
</dd>
<dt>
Determinação de problema e manutenção emergencial
</dt>
<dd>
A {{site.data.keyword.IBM_notm}} fornece uma lista dos usuários e IDs aprovados a partir de Operações da {{site.data.keyword.IBM_notm}} que podem acessar seu ambiente. É possível auditar qualquer acesso a seu ambiente por meio da página Administração para o ambiente do {{site.data.keyword.Bluemix_local_notm}}.<br>
<p>Os usuários de Operações da {{site.data.keyword.IBM_notm}} somente acessarão o ambiente do {{site.data.keyword.Bluemix_local_notm}} para um insight melhor do status da plataforma. A equipe de Operações nunca tem acesso ao seu código do aplicativo ou dados e somente executa os comandos necessários para determinação de problema para verificar configurações ou parâmetros em casos emergenciais para conduzir operações não automatizadas. Nenhum desses comandos transfere quaisquer dados sensíveis por meio da retransmissão.</p>
<p>O acesso a seu ambiente local é assegurado usando a autenticação com dois fatores durante múltiplas etapas no processo de conexão. Gerando um relatório de segurança, é possível descobrir quem acessou seu ambiente, incluindo quando e por que foi acessado.</p>
<p>O tráfego por meio da retransmissão para a determinação de problema e manutenção emergencial é tráfego SSH, bem como tráfego LDAP e Kerberos que é usado para autenticar os usuários da {{site.data.keyword.IBM_notm}}.<br>
O ambiente está completamente visível para você, como administrador, para gerenciamento de incidente, problema, mudança, capacidade e segurança. É possível acessar as informações sobre seu ambiente usando a página Administração. A tecnologia de retransmissão mantém a página Administração atualizada com os dados do evento da plataforma mais recentes do QRadar. </p>
</dd>
</dl>

### inspeção de SSL
{: #sslinspection}

Os aplicativos do Cloud Foundry e do {{site.data.keyword.Bluemix_notm}} podem trabalhar com certificados de inspeção de SSL ao acessar origens fora do ambiente local. A inspeção de conteúdo SSL estará disponível para seu ambiente, se você fornecer um certificado raiz que será usado para assinar fluxos inspecionados de SSL. 

A equipe de implementação do {{site.data.keyword.Bluemix_notm}} carrega o certificado raiz para ativar a inspeção de SSL no ambiente durante o processo de implementação para seu ambiente local. A ativação da inspeção de SSL durante o processo de configuração do ambiente não inclui tempo adicional para a implementação. Se essa capacidade não for ativada durante a implementação inicial, será possível solicitar sua implementação, no entanto, poderá haver um custo adicional associado, podendo levar de dois a quatro dias para a conclusão, dependendo das janelas de manutenção disponíveis.


## Configurando sua instância do {{site.data.keyword.Bluemix_local_notm}}
{: #setuplocal}

O {{site.data.keyword.Bluemix_local_notm}} fornece uma versão privada da oferta {{site.data.keyword.Bluemix_notm}} Public que é hospedada no hardware de sua preferência. As duas opções normalmente suportadas são as seguintes:
* Você fornece o hardware VMware.
* Você pede o {{site.data.keyword.Bluemix_notm}} Local System, que é construído em um dispositivo PureApplication pré-configurado que pode ser pedido por meio da {{site.data.keyword.IBM_notm}}. Para obter mais informações sobre as opções do dispositivo PureApplication, veja os modelos W3500 e W3550 do [IBM {{site.data.keyword.Bluemix_notm}} Local System executarem os serviços nativos de nuvem, o middleware ativado e as cargas de trabalho de padrão aberto simultaneamente ![Ícone de link externo](../icons/launch-glyph.svg)](https://www-01.ibm.com/common/ssi/rep_ca/5/897/ENUS216-325/){: new_window}.

Para o {{site.data.keyword.Bluemix_local_notm}}, é possível usar os serviços e os tempos de execução do {{site.data.keyword.Bluemix_notm}} para suportar suas necessidades de computação em um ambiente em nuvem seguro, hospedado pelo cliente e gerenciado. A {{site.data.keyword.IBM_notm}} fornece a você o acesso ao {{site.data.keyword.Bluemix_local_notm}} usando um login assegurado por senha. É possível acessar os serviços, os tempos de execução e os recursos associados e implementar e remover apps do {{site.data.keyword.Bluemix_notm}}. Revise as etapas a seguir para trabalhar com seu representante {{site.data.keyword.IBM_notm}} para configurar sua instância local do {{site.data.keyword.Bluemix_notm}}.

**Nota**: se você hospedar o {{site.data.keyword.Bluemix_local_notm}} no hardware {{site.data.keyword.Bluemix_notm}} Local System, o processo de configuração poderá ser diferente - será necessário fornecer menos informações para o representante IBM. Além disso, o escopo de suas funções e responsabilidades durante as fases de concepção e progressão poderá ser reduzido, em razão do modelo de manutenção "call home" do dispositivo PureApplication, em comparação com o modelo de gerenciamento que é necessário para usar o VMware de propriedade do cliente.

Para configurar sua versão privada do {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Revise os <a href="index.html#localinfra" title="Abre em uma nova janela">{{site.data.keyword.Bluemix_local_notm}}requisitos de infraestrutura</a> para configurar sua instância local.</li>
<li>Entre em contato com o representante de conta designado da {{site.data.keyword.IBM_notm}} ou <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">entre em contato com o {{site.data.keyword.Bluemix_notm}} <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"> </a> para iniciar.</li>
<li>Estabeleça seu contrato do {{site.data.keyword.Bluemix_local_notm}} com a {{site.data.keyword.IBM_notm}} que inclui datas de acontecimento para entrega.
	<ol type="a">
	<li>Trabalhe com a IBM em sua configuração única e taxas mensais recorrentes para sua instância do {{site.data.keyword.Bluemix_notm}} Local. A taxa de recorrência mensal baseia-se nos serviços locais que você deseja usar, mais uma assinatura para todos os serviços públicos do {{site.data.keyword.Bluemix_notm}}. Em seguida, você receberá uma fatura para tudo o que usar além desse contrato de assinatura.</li>
	<li>Identifique os prazos finais para cada fase de configuração da instância do {{site.data.keyword.Bluemix_local_notm}}.</li>
	</ol>
	</li>
<li>Depois que sua plataforma e conta forem criadas, identifique as pessoas em sua organização para as funções que são necessárias para que sua instância local esteja ativa e executando. Para obter mais informações sobre as funções designadas, veja <a href="/docs/local/index.html#rolesresponsibilities">Funções e responsabilidades do {{site.data.keyword.Bluemix_notm}} Local</a>.
</li>
<li>Você fornece o hardware e a {{site.data.keyword.IBM_notm}} ajuda a definir e estabelecer a conectividade de rede entre sua rede corporativa e sua instância do {{site.data.keyword.Bluemix_local_notm}}. Para obter mais informações sobre os requisitos de infraestrutura, veja <a href="index.html#localinfra">Requisitos de infraestrutura do {{site.data.keyword.Bluemix_local_notm}}</a>.
	<ol type="a">
	<li>A {{site.data.keyword.IBM_notm}} configura acesso à rede e o LDAP com base no que foi fornecido. É fornecido acesso administrativo aos contatos designados. Deve-se também designar um contato para suporte e faturamento.</li>
	<li>A {{site.data.keyword.IBM_notm}} configura um catálogo organizado em seu ambiente local para mostrar os serviços locais e vários dos serviços públicos do {{site.data.keyword.Bluemix_notm}}.</li>
	<li>Você valida a configuração de rede e de firewall, do terminal LDAP, e acessa.</li>
	</ol>
</li>
</ol>

É possível esperar um processo semelhante à lista a seguir para a implementação e configuração iniciais do seu ambiente. Para obter detalhes sobre quem é responsável por cada uma das tarefas, veja [Funções e responsabilidades](/docs/local/index.html#rolesresponsibilities).

**Nota**: se você optar por hospedar sua instância local na opção de hardware {{site.data.keyword.Bluemix_notm}} Local System, será possível ignorar as etapas 1 a 3 na lista a seguir.

<ol>
<li>Forneça a configuração do VMware que atenda às especificações para recursos de cálculo, configuração de redes e armazenamento. Para obter mais informações sobre os requisitos de infraestrutura, consulte <a href="/docs/local/index.html#localinfra">Requisitos de infraestrutura local do {{site.data.keyword.Bluemix_notm}}</a>.</li>
<li>Forneça as credenciais do cluster do vCenter a serem usadas pela máquina virtual de concepção. Você deve fornecer as seguintes informações:
<ul>
<li>Nome do cluster do VMware</li>
<li>Credenciais do cluster do vCenter, incluindo o ID do usuário e a senha</li>
<li>Nome ou nomes do armazenamento de dados (nome do LUN de armazenamento)</li>
<li>ID da VLAN/grupo de portas do VMware</li>
<li>Nome do conjunto de recursos</li>
</ul>
</li>
<li>Você e a {{site.data.keyword.IBM_notm}} trabalham juntos para validar as credenciais fornecidas na tarefa anterior.</li>
<li>Forneça 7 endereços IP em sua rede. Se houver um proxy da web seguro que permita acesso de saída para a Internet para componentes internos do {{site.data.keyword.Bluemix_notm}}, então deve-se fornecer as credenciais para conectar a ele.
<p>**Nota**: se o seu proxy da web não for seguro, então não será necessário fornecer as credenciais. Além disso, observe que nem todos os clientes do {{site.data.keyword.Bluemix_local_notm}} usam um proxy da web.</p></li>
<li>A {{site.data.keyword.IBM_notm}} fornece uma lista de desbloqueio de URLs à qual você deve ser permitido por meio do proxy da web antes de iniciar a implementação.<br />
<p>**Nota**: Para assegurar que seus aplicativos existentes ou novos possam acessar os recursos necessários, você poderá ter de executar etapas adicionais para empacotar os recursos com o buildpack ou trabalhar com sua equipe de segurança para criar listas de desbloqueio das URLs necessárias para executar seus aplicativos. Para obter mais informações sobre como trabalhar com os buildpacks node.js e Liberty for Java, consulte <a href="../runtimes/nodejs/offlineMode.html">Modo off-line para node.js</a> e <a href="../runtimes/liberty/offlineMode.html">Modo off-line para Liberty for Java</a>.</p>
</li>
<li>Especifique os nomes de domínio para a implementação e os IDs que deseja usar. Você obtém dois domínios definidos parcialmente ao configurar sua instância local e selecione o prefixo para os dois domínios. Por exemplo, selecione o prefixo para <code>*mycompany*.bluemix.net</code> e <code>*mycompany*.mybluemix.net</code>.<br />
<br />
Também é possível definir um domínio customizado completo, como mycustombmx.mycompany.com e application.mycompany.com. É necessário fornecer o certificado SSL, a chave do certificado e o certificado raiz antes da implementação do ambiente. O certificado raiz fornecido também pode ser usado para configurar a <a href="index.html#sslinspection">inspeção de SSL</a> para seu ambiente, mediante solicitação. <br />
<br />
É possível escolher tantos domínios customizados quantos desejar para seus aplicativos, contanto que você forneça os certificados para os domínios customizados. Para obter informações sobre como criar seu domínio customizado, veja <a href="../manageapps/updapps.html#domain">Criando e usando um domínio customizado</a>.</li>
<li>Você escolhe qual tecnologia, túnel IPSec ou OpenVPN, usar para configurar a Retransmissão para conectar novamente ao centro de operações da {{site.data.keyword.IBM_notm}}.</li>
<li>A {{site.data.keyword.IBM_notm}} instala e inicializa a máquina virtual de concepção dentro do cluster do {{site.data.keyword.Bluemix_notm}}. Se você fornecer seu próprio VMware, um representante {{site.data.keyword.IBM_notm}} ajudará seu representante de serviços a concluir esta tarefa. Se você tiver solicitado a opção de hardware {{site.data.keyword.Bluemix_notm}} Local System, um representante IBM concluirá esta tarefa.</li>
<li>A {{site.data.keyword.IBM_notm}} configura a Retransmissão para se comunicar novamente com o centro de operações da {{site.data.keyword.IBM_notm}}.</li>
<li>O repositório de máquina virtual de concepção puxa os artefatos de construção atualizados.</li>
<li>Você fornece as credenciais para que a {{site.data.keyword.IBM_notm}} se conecte à instância do diretório LDAP corporativo.</li>
<li>A {{site.data.keyword.IBM_notm}} usa a automação para implementar a plataforma principal do {{site.data.keyword.Bluemix_notm}}.</li>
<li>A {{site.data.keyword.IBM_notm}} implementa a plataforma principal que inclui os tempos de execução elásticos, o console, o recurso de administração e o monitoramento.</li>
<li>A {{site.data.keyword.IBM_notm}} vincula seu catálogo organizado a partir da implementação local a uma instância pública do {{site.data.keyword.Bluemix_notm}} para uso de serviços públicos. Um conjunto de serviços públicos está disponível em sua instância local por padrão. É possível usar a página de administração para gerenciamento de catálogos para ativar ou desativar os serviços para sua instância local.</li>
<li>A {{site.data.keyword.IBM_notm}} configura o acesso administrativo para o ambiente.</li>
<li>É possível começar a usar sua instância local que é monitorada pela equipe de operações da {{site.data.keyword.IBM_notm}} para responder aos alertas.</li>
</ol>

Depois que a instância do {{site.data.keyword.Bluemix_notm}} estiver configurada, será possível monitorar e gerenciar sua instância do {{site.data.keyword.Bluemix_notm}} usando a página Administração. Para obter mais informações, consulte [Gerenciando o {{site.data.keyword.Bluemix_local_notm}} e Dedicated](../admin/index.html#mng). Para obter informações sobre upgrades e manutenção, veja [Mantendo sua instância local](index.html#maintainlocal).

##Funções e Responsabilidades
{: #rolesresponsibilities}

Se você configurar uma conta do {{site.data.keyword.Bluemix_local_notm}}, identificará as pessoas em sua organização para as funções necessárias para que sua instância funcione.

###Funções

A lista a seguir mostra as funções e as responsabilidades designadas ao cliente:

<dl>
<dt>**Focal em compras**</dt>
<dd>Trabalha com o representante {{site.data.keyword.IBM_notm}} no estabelecimento do ambiente do {{site.data.keyword.Bluemix_local_notm}}, incluindo a identificação das pessoas certas em sua organização para trabalhar em qualquer aspecto do projeto. A pessoa designada a essa função supervisiona a seleção padrão, acordos comerciais e a disposição de acesso aos recursos do cliente. O focal em compras é o contato geral para configurar a instância local.</dd>
<dt>**Executivo de conformidade**</dt>
<dd>Trabalha com o representante {{site.data.keyword.IBM_notm}} para selecionar uma opção de topologia e de implementação que atenda aos requisitos de segurança. A pessoa designada a essa função trabalha com o consultor de conformidade da {{site.data.keyword.IBM_notm}} para determinar quais padrões de implementação alcançam os objetivos de conformidade.</dd>
<dt>**Especialista em rede**</dt>
<dd>Trabalha com o representante {{site.data.keyword.IBM_notm}} nos planos de rede para a implementação do {{site.data.keyword.Bluemix_notm}}. A pessoa designada a essa função revisa as especificações de rede requeridas pela {{site.data.keyword.IBM_notm}} e trabalha junto com a {{site.data.keyword.IBM_notm}} em um plano de implementação. No término da fase de instalação e verificação, a pessoa designada a essa função aprovará que a configuração de rede está em conformidade com os padrões corporativos.</dd>
<dt>**DevOps focal**</dt>
<dd>Trabalha com o representante {{site.data.keyword.IBM_notm}} para planejar e aplicar as atualizações de manutenção que são necessárias para a plataforma, os serviços e os tempos de execução do {{site.data.keyword.Bluemix_notm}}. A pessoa designada a essa função também trabalha com o representante {{site.data.keyword.IBM_notm}} na configuração da instância do {{site.data.keyword.Bluemix_local_notm}}.</dd>
<dt>**Especialista em IaaS**</dt>
<dd>Trabalha com os representantes {{site.data.keyword.IBM_notm}} no plano de implementação para o VMware. Geralmente, é alguém que é um administrador do VMware no datacenter. A pessoa designada para essa função revisa os requisitos de infraestrutura do <a href="../local/index.html#localinfra">{{site.data.keyword.Bluemix_local_notm}}</a> e trabalha junto com a {{site.data.keyword.IBM_notm}} em um plano de implementação. No término da implementação, a pessoa designada a essa função aprovará que a implementação está em conformidade com os padrões corporativos na camada IaaS.</dd>
<dt>**Focal de operações**</dt>
<dd>Trabalha com a equipe de suporte {{site.data.keyword.IBM_notm}}, conforme necessário, quando o ambiente estiver funcionando. Este é alguém com acesso de **Superusuário** ao console de Administração que pode aprovar e planejar as atualizações de manutenção console para o ambiente do {{site.data.keyword.Bluemix_notm}} e estar disponível sempre no evento de um incidente crítico. A pessoa designada a essa função deve ter conhecimento técnico do ambiente do {{site.data.keyword.Bluemix_notm}} e estar em uma posição para alcançar outras pessoas na empresa que tenham qualificações de especialista em uma área que possa ser afetada, incluindo rede ou segurança, por exemplo.
</dd>
</dl>

Seus representantes de serviços trabalham com especialistas {{site.data.keyword.IBM_notm}}, que trabalham juntos para assegurar que você sempre tenha o suporte necessário. É possível fazer upgrade para a camada de suporte Premium, para trabalhar com um Client Success Manager (CSM) dedicado para a sua conta. Para obter mais informações sobre as camadas de suporte diferentes, consulte [Entrando em contato com o suporte](../support/index.html#contacting-support). O CSM conclui os tipos de tarefas a seguir:

<ul>
<li>Fornece coordenação técnica entre você e a IBM.</li>
<li>Coordena atualizações, upgrades, ajuda de especialistas da IBM, além de ativação inicial de um engenheiro de suporte do {{site.data.keyword.Bluemix_notm}}.</li>
<li>Fornece informações sobre os tipos de suporte que estão disponíveis.</li>
<li>Agirá como um ponto de escalada inicial, se necessário.</li>
</ul>

O suporte e a equipe de operações do {{site.data.keyword.Bluemix_notm}} que trabalham com você em sua instância do {{site.data.keyword.Bluemix_notm}} podem acessar seu ambiente local, mas faz isso apenas pelos motivos a seguir.

<ul>
<li>Para responder a alertas e executar manutenção operacional</li>
<li>Para tentar reproduzir um problema relatado em um chamado de suporte</li>
</ul>

###Responsabilidades

Da configuração de seu ambiente até a manutenção contínua, você e a IBM devem concluir uma variedade de tarefas. As tabelas a seguir descrevem as tarefas necessárias e os proprietários para concluir a tarefa durante as fases de concepção, progressão e conclusão.

A fase de concepção é usada para estabelecer o ambiente do {{site.data.keyword.Bluemix_local_notm}}. Neste momento, você já revisou os [Requisitos de infraestrutura local](../local/index.html#localinfra). Os objetivos principais dessa fase incluem os itens a seguir:

- Revisar o contrato financeiro e estabelecer as datas do acontecimento para entrega.
- Criar a plataforma {{site.data.keyword.Bluemix_notm}} e fornecer acesso aos tempos de execução e serviços.
- Definir e estabelecer conectividade de rede entre a rede corporativa e as operações do {{site.data.keyword.Bluemix_notm}}.
- Identificar e designar funções para sua equipe administrativa.

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Configurar padrões de conformidade | Identificar padrões corporativos do governo, da indústria e proprietários que são necessários para o ambiente. | Cliente |
|Criar plano de integração de segurança e conformidade | Criar plano de segurança e integração que inclui custos, planejamento e recursos que são necessários para atingir conformidade de segurança. | {{site.data.keyword.IBM_notm}} |
|Aprovação do plano de conformidade | Aprovar o plano de conformidade. | Cliente |
|Criar dimensionamento para o ambiente |  	Criar dimensionamento de ambiente com base nas opções predefinidas que consideram a alta disponibilidade e os objetivos de recuperação de desastre, bem como o DEA inicial e o fornecimento de serviço que são necessários para suportar os apps criados com a plataforma. Você e a {{site.data.keyword.IBM_notm}} trabalham juntos para definir, por exemplo, quais bancos de dados são necessários, quais serviços são oferecidos no catálogo organizado do cliente e muito mais. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Selecionar arquitetura | Selecione a arquitetura com base nas opções predefinidas que consideram a alta disponibilidade e os requisitos de recuperação de desastre. | {{site.data.keyword.IBM_notm}} |
|Definir objetivos de recuperação de desastre | Definir os requisitos de recuperação de desastre para o ambiente. | Cliente |
|Criar plano de recuperação de desastres | Consultar e definir o plano de recuperação de desastres. A {{site.data.keyword.IBM_notm}} cria um modelo de recuperação de desastre e consulta você sobre fornecimento de feedback e aprovação do plano. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Criar plano de backup e recuperação | Criar um plano de backup e recuperação que defina a frequência e os requisitos para distribuição ocasional do backup pelo site. A {{site.data.keyword.IBM_notm}} faz backup de componentes de plataforma, serviços {{site.data.keyword.IBM_notm}}, metadados de serviços que incluem funções de usuário e muito mais. Você faz backup de todos os dados específicos do aplicativo pelos quais é responsável. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Identificar ferramentas para detecção de eventos e determinação de problemas | Identificar ferramentas da {{site.data.keyword.IBM_notm}} e de terceiros usadas para detecção de eventos e determinação de problema no nível da plataforma {{site.data.keyword.Bluemix_notm}}. | {{site.data.keyword.IBM_notm}} |
|Definir plano de escalada | Definir o plano de escalada para fazer triagem e resolver eventos detectados a partir dos componentes de monitoramento. | {{site.data.keyword.IBM_notm}} |
|Assinar contratos de infraestrutura, de plataforma e de suporte | Assinar o contrato de assinatura, incluindo os termos financeiros e as condições para o ambiente. Assine a assinatura de suporte. | Cliente |
|Comprar ambiente | Comprar recursos de cálculo, de rede e de armazenamento. Para obter mais informações sobre os requisitos de infraestrutura para o ambiente, consulte [Requisitos de infraestrutura local](../local/index.html#localinfra). | Cliente |
|Instalar solução de VPN | Instalar solução de VPN bidirecional. | {{site.data.keyword.IBM_notm}} |
|Instalar componentes de plataforma, de aplicativo e de monitoramento e gerenciamento | Instale, configure e verifique componentes da plataforma, como BOSH Director, Cloud Controller, Health Manager, sistema de mensagens, roteadores, DEAs e provedores de serviço, além dos componentes de monitoramento definidos no plano de escalada e de detecção de problema. | {{site.data.keyword.IBM_notm}} |
|Instalar e configurar componentes de segurança | Instalar e configurar componentes de segurança que são ligados ao plano de monitoramento e escalada, incluindo {{site.data.keyword.IBM_notm}} QRadar, área segura de credenciais, sistema de prevenção de intrusão, {{site.data.keyword.IBM_notm}} BigFix e {{site.data.keyword.IBM_notm}} Security Privileged Identity Management. | {{site.data.keyword.IBM_notm}} |
|Configurar servidor de login | Configurar o servidor de login para uso com o LDAP corporativo. | {{site.data.keyword.IBM_notm}} |
|Instalar e configurar componentes customizados |  	Instalar e configurar componentes customizados que residem fora do escopo do produto e serviços {{site.data.keyword.Bluemix_notm}}. | Cliente |
|Conectar pipeline do {{site.data.keyword.Bluemix_notm}} | Conectar pipeline de integração contínua e de entrega contínua do {{site.data.keyword.Bluemix_notm}} com repositórios da {{site.data.keyword.IBM_notm}}. | {{site.data.keyword.IBM_notm}} |
|Customizar componentes de solução externa | Customizar balanceadores de carga para cenários de recuperação de desastre. | Cliente |
|Rastrear status para controles de segurança, de conformidade e de auditoria  | Rastrear status até o ponto em que todas as ferramentas e processos estiverem adequados para atingir a conformidade identificada. | Cliente |
|Revisar a infraestrutura física | Revisar instalações físicas que hospedam os componentes da solução para ameaças e revisão de controles de segurança para proteger o datacenter. | Cliente |
|Inspecionar software de monitoramento | Inspecionar componentes de monitoramento e gerenciamento, conforme definido no plano de escalada e de determinação de problema. | Cliente |
|Inspecionar sistema operacional | Inspecionar para assegurar-se de que a imagem do sistema operacional atenda aos padrões de conformidade. A {{site.data.keyword.IBM_notm}} fornece acesso à imagem do OS. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
{: caption="Table 5. Inception phase tasks" caption-side="top"}

A fase seguinte é a de progressão. A fase de progressão descreve o relacionamento colaborativo em andamento, entre você e a IBM. Os objetivos principais dessa fase incluem os itens a seguir:

- Revisar a capacidade e coordenar os ajustes necessários.
- Revisar as melhorias de manutenção e plataforma.
- Coordenar as atividades para resolução de problemas e análise de causa raiz.

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Revisar relatórios de capacidade semanal | Revisar os relatórios de capacidade semanal e executar a ação corretiva, se necessário. | Cliente |
|Criar projeções mês a mês | Coletar informações e criar uma projeção mês a mês da capacidade e do consumo. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Revisar projeções de capacidade | Revisar as projeções de capacidade, visto que estão relacionadas a eventos externos que podem causar impacto na capacidade, bem como novas implementações previstas de apps. Trabalhe com a {{site.data.keyword.IBM_notm}} para revisar as projeções e planejar adequadamente. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Ajustar a capacidade |  Incluir ou remover capacidade conforme suas necessidades mudarem. | {{site.data.keyword.IBM_notm}} |
|Publicar atualizações e manutenção futuras | Criar documentação para a manutenção necessária de componentes da {{site.data.keyword.IBM_notm}}. | {{site.data.keyword.IBM_notm}} |
|Executar manutenção | Trabalhe com a {{site.data.keyword.IBM_notm}} para planejar a manutenção necessária dentro de uma janela de 21 dias. É possível fornecer datas que podem não funcionar para você na janela de 21 dias e a {{site.data.keyword.IBM_notm}} trabalha para planejar a manutenção adequadamente. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Tratar de falhas de fornecimento | Corrigir falhas de fornecimento, se ocorrerem, para serviços criados pelo cliente que estejam implementados no Catálogo. | {{site.data.keyword.IBM_notm}} |
|Executar varreduras de rede e de IP | Executar varreduras diárias e mensais de rede e de IP. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Fornecer acesso aos logs de auditoria | Fornecer acesso a todos os logs de auditoria de segurança e administrativos.   | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Conduzir teste | Conduzir teste periódico de Controles de chave sobre operações e teste de penetração de terceiros. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Relato de status, coordenação de auditoria e reuniões de conformidade  | Concluir relato de status, coordenação de auditoria externa e representação em reuniões de status de revisão de conformidade. | {{site.data.keyword.IBM_notm}} |
|Verificação de emprego e de necessidade de negócios | Verificação completa do emprego trimestralmente e verificação da necessidade contínua de negócios para representantes {{site.data.keyword.IBM_notm}} que possuem acesso ao ambiente do cliente. | {{site.data.keyword.IBM_notm}} |
|Resolução de vulnerabilidades de segurança | Resolver vulnerabilidades de segurança relatadas na plataforma. | {{site.data.keyword.IBM_notm}} |
{: caption="Table 6. Progression phase tasks" caption-side="top"}

O estágio final da conclusão representa o término do relacionamento entre você e a {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}. As tarefas principais dessa fase incluem os itens a seguir:

* Término do contrato financeiro
* Remoção de todas as conexões de rede
* Infraestrutura de reciclagem

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Terminar o contrato financeiro | Discutir e concordar com um término para o contrato financeiro. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Ambiente de desatribuição | Encerrar o acesso e as credenciais para o ambiente. | A {{site.data.keyword.IBM_notm}} e o cliente compartilham a responsabilidade |
|Encerrar a retransmissão | Finalizar a conexão de retransmissão. | {{site.data.keyword.IBM_notm}} |
|Reciclar a infraestrutura | Reciclar sua infraestrutura de acordo com as diretrizes da empresa. | Cliente |
{: caption="Table 7. Completion phase tasks" caption-side="top"}


## Requisitos de infraestrutura do {{site.data.keyword.Bluemix_local_notm}}
{: #localinfra}

Para {{site.data.keyword.Bluemix_local_notm}}, você possui a segurança física e a infraestrutura para hospedar a instância local. Os requisitos de infraestrutura serão os mesmos se você optar por usar e gerenciar seu próprio VMware ou comprar o {{site.data.keyword.Bluemix_local_notm}} System que inclui um dispositivo PureApp pedido da IBM. No entanto, há duas opções de dispositivo PureApp dos quais escolher ao pedir e o processo de ajuste de escala de seu ambiente difere para o VMware e o {{site.data.keyword.Bluemix_local_notm}} System. Para obter mais informações sobre as opções do dispositivo PureApp, veja os modelos W3500 e W3550 do [IBM {{site.data.keyword.Bluemix_notm}} Local System executarem os serviços nativos de nuvem, o middleware ativado e as cargas de trabalho de padrão aberto simultaneamente ![Ícone de link externo](../icons/launch-glyph.svg)](https://www-01.ibm.com/common/ssi/rep_ca/5/897/ENUS216-325/){: new_window}.

A {{site.data.keyword.IBM_notm}} configura os requisitos mínimos a seguir para configurar o {{site.data.keyword.Bluemix_local_notm}}.

### Hardware

Embora existam requisitos para o tipo e o tamanho do hardware disponível, é possível escolher qualquer combinação para atender os requisitos totais do recurso.

<dl>
<dt>**Hardware do VMware ESXi**</dt>
<dd>
ESXi é uma camada de virtualização que é executada em servidores físicos e que abstrai o processador, a memória, o armazenamento e os recursos em múltiplas máquinas virtuais. Escolha qualquer combinação que atenda aos totais de recurso a seguir, sob a condição de que a contagem núcleo física mínima por ESXi é oito. As seguintes especificações são apenas para o tempo de execução principal do {{site.data.keyword.Bluemix_notm}}.
<ul>
<li>32 núcleos físicos a 2.0 GHz ou mais cada</li>
<li>512 GB de RAM física</li>
<li>Tamanho total de armazenamento de dados de 7.5 TB
<ul>
<li>Armazenamento de dados de 7 TB para manter {{site.data.keyword.Bluemix_notm}}</li>
<li>500 GB de armazenamento de dados para suspender a máquina virtual de concepção</li>
</ul>
</li>
</ul>
<p><strong>Nota:</strong> Se você usar diversos armazenamentos de dados, use o mesmo prefixo para cada um.</p>
</dd>
<dt>**Alta disponibilidade**</dt>
<dd>
Para suportar uma única falha de nó, deve-se ter n+1 ESXi. Por exemplo, se o núcleo 32 e 512 GB de memória for encontrado usando dois núcleos de 16x com servidores ESXi de 256 GB, você precisará de três desses servidores para suportar uma falha completa de um único nó.
<p><strong>Nota:</strong> O administrador do VMware do cliente pode decidir forçar o failover de alta disponibilidade rigorosa no cluster para garantir os recursos. Se você optar por continuar sem failover de alta disponibilidade, poderá atender ao requisito mínimo de recurso de 32 núcleos e 512 GB.</p>
</dd>
<dt>**Rede**</dt>
<dd>
Os requisitos recomendados incluem um grupo de portas acessível ao cliente com sete endereços IP de rede do cliente que possuem acesso à Internet de saída na mesma sub-rede. Duas portas são usadas pela máquina virtual de concepção, três portas são endereços IP virtuais usados para os domínios e as duas finais são endereços IP públicos para os DataPowers. Em seguida, você define uma segunda VLAN privada somente dos ESXis que estão sendo usados para o {{site.data.keyword.Bluemix_local_notm}}. Essa VLAN é mostrada como um grupo da porta em VMware. O {{site.data.keyword.Bluemix_local_notm}} usa isso para sub-rede privada, que é mais segura e pode ajudar a evitar problemas de roteamento.<br />
<p>As portas a seguir são usadas:</p>
<ul>
<li>Porta 443 para a conexão de Retransmissão
<p>**Nota**: se você optar por usar um túnel IPSec em vez de um OpenVPN, então abra uma porta do cliente para essa conexão.</p></li>
<li>Porta 389 ou SSL 636 para a conexão LDAP ou Active Directory</li>
</ul>
<p>**Nota**: a {{site.data.keyword.IBM_notm}} pode detectar se a conexão de rede foi perdida. No evento de perda de conexão de rede, a {{site.data.keyword.IBM_notm}} entra em contato com você e trabalha com seu especialista de rede para resolver o problema.</p>
</dd>
<dt>**Uplinks de rede**</dt>
<dd>Use duas ou mais interfaces que variam de 1 a 10 Gbps, dependendo da carga de trabalho desejada para o sistema.</dd>
</dl>

### Configuração do servidor vCenter

Revise os requisitos a seguir de versão, de datacenter, de conjunto de recursos e de armazenamento de dados.

<dl>
<dt>**Versões suportadas de VMware**</dt>
<dd>vCenter e ESXi 5.1, 5.5 e 6.0</dd>
<dt>**Tipos de VMware suportados**</dt>
<dd>vSphere Enterprise<br />
Enterprise vSphere plus, se você planeja usar os comutadores virtuais distribuídos</dd>
<dt>**Datacenter**</dt>
<dd>Crie um datacenter, se não existir um.</dd>
<dt>**Pasta do Datacenter**</dt>
<dd>Crie uma pasta de MV com o mesmo nome que o cluster, se não planeja conceder acesso de Administrador que seja propagado do datacenter.</dd>
<dt>**Cluster**</dt>
<dd>Crie um cluster especificamente para uso do {{site.data.keyword.Bluemix_local_notm}}. Um exemplo para o nome do cluster é `bluemix`.</dd>
<dt>**Conjunto de recursos**</dt>
<dd>Crie um conjunto de recursos sob o cluster do {{site.data.keyword.Bluemix_local_notm}}. Um exemplo para o nome do conjunto de recursos é `local`.</dd>
</dt>**Armazenamento de dados**</dt>
<dd>Requer 7.5 TB para a implementação inicial de {{site.data.keyword.Bluemix_notm}}.<br />
<br />
**Nota**: Ao usar mais de um armazenamento de dados, assegure-se de que cada um deles comece com o mesmo prefixo. Os exemplos de múltiplos nomes de armazenamento de dados com o mesmo prefixo são `bluemix_datastore_01` e `bluemix_datastore_02`.</dd>
<dt>**Rede**</dt>
<dd>Deve-se ter uma rede acessível para o cliente com capacidade de acesso à Internet de saída. A VLAN hospeda a sub-rede privada em que os componentes do Bluemix Local são executados. Todo o tráfego é roteado a partir da sub-rede privada para a sub-rede do cliente. Um IP de sub-rede do cliente é usado para todo o acesso ao Bluemix Local. Em seguida, é possível definir uma segunda VLAN privada entre somente os ESXis sendo usados para o Bluemix Local. Essa VLAN é mostrada como um grupo da porta em VMware. O Bluemix Local a usa para a sub-rede privada, que é mais segura e pode ajudar a evitar problemas de roteamento.
<p>Se estiver usando comutadores vSphere distributed switches (vDS), crie uma pasta para conter os vDS e coloque os vDS dentro da pasta.</p>
</dl>

### Largura da banda da rede para Retransmissão

O rendimento recomendado é 5 Mbps para cima e 5 Mbps para baixo e é possível esperar um uso de dados mensal de 10 GB. A {{site.data.keyword.IBM_notm}} estabelece janelas acordadas quando grandes pacotes configuráveis de dados são entregues, que podem ser tão grandes quanto 4 GB.

### Permissões de VMware

Configure as funções e as permissões a seguir. A propagação é configurada para cada permissão. Se a permissão for propagada, a permissão será aprovada na hierarquia de objeto. No entanto, as permissões para um objeto-filho sempre substituem as permissões que são propagadas de um objeto pai.

<dl>
<dt>**vCenter Server**</dt>
<dd>Configure a função como somente leitura e não propagada.<br />
<br />
**Nota**: Essa função é necessária para recuperar o status de tarefa para operações de disco específicas.</dd>
<dt>**Datacenter**</dt>
<dd>Crie a função "{{site.data.keyword.Bluemix_notm}}" e conceda as permissões a seguir:
<ul>
<li>Para o **Armazenamento de dados**, configure **Operações de arquivo de nível baixo** e **Atualizar arquivos da máquina virtual**.</li>
<li>Para **vApp**, configure **Importar**.</li>
<li>Para o grupo **dvPort**, configure **Modificar**. Essa é para somente para uso de vDS.</li>
</ul>
**Nota**: Esta função é necessária para suportar posts de arquivos para os armazenamentos de dados.</dd>
<dt>**Cluster**</dt>
<dd>Configure a função como administrador e propagado.</dd>
<dt>**Armazenamento de dados**</dt>
<dd>Configure o administrador de função e propagado para cada armazenamento de dados do {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>**Rede**</dt>
<dd><ul>
<li>Para vSwitch, configure grupos de portas públicas e privadas com a função de administrador, não propagados.</li>
<li>Para a pasta pai de vDS, configure como somente leitura e propagada.</li>
<li>Para vDS, configure grupos de portas públicas e privadas com a função de administrador, não propagados.</li>
</ul>
</dd>
</dl>

### Ajustando a escala de seu ambiente

#### Opção VMware

Se você tiver escolhido fornecer sua própria opção de hardware VMware com base nas especificações mínimas, você será configurado com 64 GB de memória disponível. Caso queira incluir 16 ou 32 GB, deve-se trabalhar com a sua equipe de hardware para fornecer a memória disponível ou incluir um servidor ESXi, se necessário, conforme descrito no exemplo a seguir. Quando a capacidade de hardware estiver disponível, trabalhe com seu gerenciador de sucesso do cliente que pode trabalhar com a equipe da IBM para gerenciar o aumento de memória de cálculo.

Para aumentar o conjunto de DEA, cada DEA é configurado com:

- 16 ou 32 GB de RAM
- vCPU de 2x ou 4x
- 150 ou 300 GB de armazenamento

Por exemplo, se o tamanho do host ESXi for 256 GB de memória com 16x núcleos, então serão incluídos oito DEAs. Se o tamanho do host ESXi for 64 GB de memória com 8x núcleos, dois ESXis e quatro DEAs precisarão ser incluídos. É necessário um adicional de 1,5 TB de armazenamento para cada um dos quatro DEAs. Esse exemplo é baseado em um DEA configurado com 32 GB de RAM, 4x vCPU e 300 GB de armazenamento.


#### Opção Bluemix Local System

Caso você opte por pedir o hardware PureApplication por meio da {{site.data.keyword.IBM_notm}} para hospedar sua instância do {{site.data.keyword.Bluemix_notm}} Local, deverá pedir outro nó de cálculo no tamanho de especificação comprado anteriormente. É possível pedir outro nó por meio do gerenciador de sucesso do cliente que trabalha com a equipe da IBM para que o hardware atualizado seja enviado diretamente a você. Quando o hardware é entregue e instalado, a IBM é notificada e a equipe de implementação inclui um adicional de 64 GB. Dependendo do tamanho do nó de cálculo pedido, é possível que você tenha capacidade adicional disponível para futuros upgrades. Nesse caso, você só precisará entrar em contato com a IBM e a equipe poderá incluir incrementos adicionais de 64 GB de memória de cálculo disponível, conforme necessário.

## Mantendo sua instância local
{: #maintainlocal}

A {{site.data.keyword.IBM_notm}} mantém e instala atualizações e correções para os tempos de execução e serviços do {{site.data.keyword.Bluemix_notm}}, conforme a {{site.data.keyword.IBM_notm}} julga adequado. Os serviços podem não estar disponíveis durante as janelas de manutenção. Além disso, a {{site.data.keyword.IBM_notm}} trabalha com você para planejar atualizações de manutenção para a plataforma do {{site.data.keyword.Bluemix_notm}}.

### Manutenção do {{site.data.keyword.Bluemix_notm}}

Os tipos de manutenção a seguir são necessários para o {{site.data.keyword.Bluemix_local_notm}}:

<dl>
<dt>**Manutenção padrão para serviços**</dt>
<dd>Os serviços utilizam janelas de manutenção predefinidas padrão, o que pode fazer com que os serviços fiquem indisponíveis. A {{site.data.keyword.IBM_notm}} não requer aprovação do cliente para executar manutenção de serviço, mas tenta minimizar o impacto nos serviços.<br />
<br />
A {{site.data.keyword.IBM_notm}} envia mensagens transmitidas que detalham as mudanças que estão planejadas para cada janela de manutenção na página Status.<br />
<br />
**Importante**: alguns serviços podem não ficar disponíveis durante o período de manutenção.</dd>

<dt>**Manutenção padrão para a plataforma do {{site.data.keyword.Bluemix_notm}}**</dt>
<dd>As atualizações de manutenção são aplicadas com base na coordenação entre você e a {{site.data.keyword.IBM_notm}} dentro de uma janela de 21 dias. Você fornece à {{site.data.keyword.IBM_notm}} janelas de manutenção pré-aprovadas e datas ou horas específicas que podem não funcionar para você e a {{site.data.keyword.IBM_notm}} trabalha para planejar atualizações durante ou em torno das datas selecionadas.<br />
<p>Acesse **ADMINISTRAÇÃO > INFORMAÇÕES DO SISTEMA**, para visualizar atualizações de manutenção planejadas e pendentes. Para obter mais informações sobre como configurar as suas janelas pré-aprovadas, as datas indisponíveis e visualizar ou aprovar atualizações de manutenção, consulte <a href="../admin/index.html#oc_schedulemaintenance">Atualizações de manutenção</a>.</p></dd>
</dl>

**Importante**: a {{site.data.keyword.IBM_notm}} se reserva o direito de interromper os serviços para aplicar manutenção emergencial, conforme necessário. A {{site.data.keyword.IBM_notm}} pode mudar as horas de manutenção planejada, mas o notificará sobre essas mudanças, bem como sobre quaisquer informações de manutenção emergencial.

Se houver um problema relatado após uma atualização de manutenção, você concordará com o Suporte do {{site.data.keyword.Bluemix_notm}} se for de seu melhor interesse permitir que a {{site.data.keyword.IBM_notm}} retroceda a atualização. Em concordância, a {{site.data.keyword.IBM_notm}} retrocederá a atualização para restaurar o ambiente para o estado anterior.

### Manutenção da infraestrutura do cliente
{: #inframaintenance}

O {{site.data.keyword.Bluemix_local_notm}} é implementado no hypervisor ESXi e o aplicativo vCenter é usado para gerenciar centralmente máquinas virtuais e hosts ESXi. O {{site.data.keyword.Bluemix_notm}} suporta as três versões mais recentes de ESXi e vCenter, incluindo todas as atualizações e correções intermediárias. Sempre é possível localizar as versões mais recentes suportadas na documentação de [Requisitos de infraestrutura local](../local/index.html#localinfra).

**Importante**: com o {{site.data.keyword.Bluemix_local_notm}} sendo implementado no hypervisor ESXi, upgrades e correções para ESXi podem interromper a disponibilidade do ambiente local, incluindo todos os aplicativos e serviços em execução dentro do ambiente. Deve-se notificar o {{site.data.keyword.Bluemix_notm}} usando um chamado de suporte anterior à conclusão de um upgrade ou de uma correção, para assegurar que a interrupção não alerte a equipe de operações por engano. Se você tiver um gerenciador de sucesso do cliente designado (CSM), será possível trabalhar com o CSM para comunicar o planejamento de upgrade.

Para assegurar que a sua instância local seja compatível com as versões mais recentes suportadas, a equipe de Operações do {{site.data.keyword.Bluemix_notm}} monitora o ambiente para versões não suportadas que podem não corresponder às últimas atualizações do ambiente do {{site.data.keyword.Bluemix_notm}} Local. Algumas atualizações do {{site.data.keyword.Bluemix_notm}}, como atualizações de versão do Cloud Foundry, requerem que você atualize o software ESXi ou vCenter. O suporte do {{site.data.keyword.Bluemix_notm}} irá alertá-lo sobre o que deve ser atualizado e quando. É fornecida uma janela de tempo para concluir esta atualização.

O {{site.data.keyword.Bluemix_notm}} faz todos os esforços para manter os ambientes locais compatíveis com as versões mais recentes do ESXi e do vCenter. No entanto, pode haver curtos períodos de tempo nos quais as versões mais recentes do ESXi e do vCenter não são suportadas. Consulte a documentação de [Requisitos de infraestrutura local](/docs/local/index.html#localinfra) para as versões compatíveis mais recentes, antes de aplicar qualquer atualização.


## Resposta e suporte de incidente para o {{site.data.keyword.Bluemix_local_notm}}
{: #incidentresponse}

### Problemas detectados pelo cliente

Se você identificar um problema que precisa de atenção do suporte e operações da {{site.data.keyword.IBM_notm}}, será possível entrar em contato com o suporte usando alguns métodos diferentes. Para obter informações sobre como entrar em contato com o suporte, consulte [Contatando o suporte](../support/index.html#contacting-bluemix-support-local). Dependendo do problema, você, a IBM ou ambos trabalham juntos para corrigir o problema.

### Incidentes críticos detectados pela IBM

Os incidentes críticos são indisponibilidades de serviço urgentes e inesperadas e problemas de estabilidade que afetam seu ambiente ou seus usuários. Se a {{site.data.keyword.IBM_notm}} detectar um incidente crítico em seu ambiente, você será notificado por uma notificação na página **Status**. Também é possível verificar a página Status para quaisquer problemas conhecidos da plataforma ou de seus serviços. Para obter mais informações sobre a página Status, veja [Visualizando o status](../admin/index.html#oc_status).

Se deseja integrar suas notificações a um serviço da web que suporta o ganchos da web, consulte [Notificações e inscrições de eventos](/docs/admin/index.html#oc_eventsubscription) para obter informações sobre como estender seus recursos de notificação.

![Processo de resposta de incidente](images/incidentresponseprocess.png "Processo de resposta de incidente")

Figura 2. Processo de resposta de incidente

Dependendo do problema, você, a IBM ou ambos trabalham juntos para corrigir o problema. Se você tiver uma pergunta sobre o incidente ou se precisar de um representante {{site.data.keyword.IBM_notm}} para ajudá-lo a resolver o problema, será possível abrir um chamado de suporte. Para obter informações sobre como entrar em contato com o suporte, consulte [Contatando o suporte](../support/index.html#contacting-bluemix-support-local).

**Nota**: chamados de suporte de gravidade 1 são monitorados 24 horas por dia, sete dias por semana. Outros chamados são processados a partir de domingo às 22h GMT até sábado às 0h GMT. Para obter mais informações sobre gravidade de chamados de suporte e trabalhar com suporte, consulte <a href="/docs/support/index.html#contacting-bluemix-support-local">Contatando o suporte</a>.

## Recuperação de desastre para o {{site.data.keyword.Bluemix_local_notm}}
{: #dr}

A recuperação de desastre para o {{site.data.keyword.Bluemix_short}} Local pode ser configurada de forma semelhante à maneira que funciona quando você usa o {{site.data.keyword.Bluemix_short}} Public. O {{site.data.keyword.Bluemix_short}} Public fornece uma plataforma continuamente disponível para inovação com várias medidas à prova de falhas, a fim de assegurar que as suas organizações, os seus espaços e aplicativos estejam sempre disponíveis. Implementar apps em várias regiões geográficas permite disponibilidade contínua que protege contra perda simultânea não planejada de vários componentes de hardware ou software, ou a perda de um datacenter inteiro, para que, mesmo no caso de um desastre natural em uma localização geográfica, as instâncias de app distribuídas do {{site.data.keyword.Bluemix_notm}} Public em localizações geográficas alternativas fiquem disponíveis.
{: shortdesc}

A recuperação de desastre do {{site.data.keyword.Bluemix_short}} Local torna-se possível por meio de disponibilidade contínua para seus apps, da alta disponibilidade inerente da plataforma e da capacidade de restaurar sua instância no caso de uma falha. Você é responsável por ativar a disponibilidade contínua de seus apps implementando em várias regiões. A alta disponibilidade é construída no nível de plataforma por meio de tecnologias incluídas no Cloud Foundry e de outros componentes. Além disso, é possível trabalhar junto com a {{site.data.keyword.IBM_notm}} para assegurar que seus dados sejam submetidos adequadamente a backup no caso de você precisar restaurar sua instância a qualquer momento.

### Ativando a disponibilidade contínua para o {{site.data.keyword.Bluemix_local_notm}}
{: #enabling}

Por padrão, o {{site.data.keyword.Bluemix_notm}} Public é implementado em várias localizações geográficas. No entanto, deve-se fazer o seguinte para ativar instâncias do {{site.data.keyword.Bluemix_local_notm}} distribuídas globalmente:

* Assegure-se de que os desenvolvedores estejam implementando apps em mais de uma região, por meio de um processo manual ou automatizado. As regiões selecionadas devem ter uma separação de mais de 200 km umas das outras para assegurar que um desastre natural não possa afetar ambas as localizações geográficas.
* Configure um balanceador de carga global, como Akamai ou Dyn, para apontar para apps em pelo menos duas regiões diferentes.

**Nota**: nem todos os serviços do {{site.data.keyword.Bluemix_notm}} suportam distribuição regional. Ao construir um app, para atingir a distribuição geográfica, deve-se também certificar-se de que os serviços usados por esse app tenham a sincronização de dados como um recurso-chave.

#### Implementando apps do {{site.data.keyword.Bluemix_local_notm}} em múltiplas localizações geográficas
{: #deploying}

Para implementar em um segundo local ou em vários locais, deve-se seguir um processo semelhante ao usado para ativar sua localização geográfica primária:

1. Ative um novo ambiente local para hospedar instâncias adicionais de seus aplicativos. Para criar um novo ambiente, entre em contato com a equipe de vendas da {{site.data.keyword.IBM_notm}} para iniciar o processo. Para obter mais informações sobre a configuração de uma instância local, consulte [Configurando o {{site.data.keyword.Bluemix_local_notm}}](../local/index.html#setuplocal). Deve-se efetuar login separadamente para acessar cada ambiente. Cada local físico dos ambientes hospedados deve ter uma separação mínima de 200 km do local original para assegurar disponibilidade.
2. Obtenha o nome de domínio exclusivo no qual seu novo app implementado será hospedado. Por exemplo, se o domínio original for *mycompany.caeast.bluemix.net*, será possível criar um novo ambiente local com um novo domínio, como *mycompany.cawest.bluemix.net*, e implementar no novo domínio.
3. Implemente o novo local sempre que você implementar o seu app original. Para obter mais informações sobre a implementação, consulte [Fazendo upload de seu app](/docs/starters/upload_app.html).


#### Ativando um balanceador de carga global para o {{site.data.keyword.Bluemix_local_notm}}
{: #glb}

Um balanceador de carga global não apenas assegura disponibilidade contínua e é necessário para recuperação de desastre, como também possui diversos benefícios adicionais:

* Roteia usuários para a região mais próxima do {{site.data.keyword.Bluemix_notm}}, por padrão
* Roteia com base no desempenho
* Direciona seletivamente uma porcentagem de tráfego para uma nova versão do aplicativo
* Fornece failover do site com base na verificação de funcionamento da região
* Fornece failover do site com base na verificação de funcionamento do aplicativo
* Usa roteamento ponderado entre os terminais

É possível escolher um balanceador de carga global, como Akamai ou Dyn. Para obter mais informações sobre como usar o Akamai como um balanceador de carga global, veja [Gerenciamento de tráfego global ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Para obter mais informações sobre como usar o Dyn como um balanceador de carga global, veja [Quatro motivos pelos quais as empresas estão levando o balanceamento de carga global para a nuvem ![Ícone de link externo](../icons/launch-glyph.svg)](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Alta disponibilidade
{: #ha}

Além de permitir a disponibilidade contínua, o {{site.data.keyword.Bluemix_notm}} também fornece alta disponibilidade na plataforma usando tecnologias construídas no Cloud Foundry e outros componentes.

Essas tecnologias incluem os itens a seguir:

<dl>
<dt>Escalabilidade de DEA no Cloud Foundry</dt>
<dd>Um <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA) do Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Ícone de link externo">
</a> executa verificações de funcionamento nos apps nele executados. Se houver um problema com o app ou com o próprio DEA, ele implementará instâncias adicionais do app em um DEA alternativo para tratar do problema. Para obter mais informações, veja <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configurando o CF para alta disponibilidade com redundância <img src="../icons/launch-glyph.svg" alt="Ícone de link externo">
</a>.
<p>Para garantir a alta disponibilidade para seus aplicativos, é necessário calcular recursos suficientes para equilibrar a carga e você também pode requerer recursos de cálculo adicionais para suportar uma possível falha. Se precisar escalar seu ambiente aumentando o conjunto de DEA para ser preparado para uma falha ou direcionar um aumento na carga para suas instâncias de app, será possível trabalhar com seu representante IBM para pedir DEAs adicionais e que tenha o hardware apropriado para suportar os recursos incluídos.
</p>
</dd>
<dt>Backup de metadados</dt>
<dd>Os metadados são submetidos a backup em um local secundário, geralmente uma máquina virtual local. Se possível, convém replicar o backup para seu próprio ambiente com pelo menos 200 km de distância.</dd>
</dl>

## Restaurando sua instância local
{: #restorelocal}

É feito backup regularmente de definições, metadados e configurações do {{site.data.keyword.Bluemix_local_notm}} para se preparar para indisponibilidades não planejadas no ambiente. Os dados por cujo backup você é responsável incluem dados do aplicativo, dados de serviços do banco de dados em nuvem e armazenamentos de objeto.

Como parte do backup de dados, que inclui metadados e configurações do sistema, a {{site.data.keyword.IBM_notm}} conclui as tarefas a seguir:

<ul>
<li>Criptografa todas as cópias de backup e gerencia chaves de criptografia</li>
<li>Monitora e gerencia a atividade de backup</li>
<li>Fornece os arquivos de backup criptografados</li>
<li>Restaura os dados solicitados</li>
<li>Gerencia conflitos de planejamento entre as operações de gerenciamento de backup e correção</li>
</ul>

Como a proteção de dados privados é crítica, a {{site.data.keyword.IBM_notm}} precisa da sua colaboração ao lidar com o gerenciamento de arquivo de backup, de modo que os arquivos não sejam movidos para fora dos datacenters. Especificamente, a {{site.data.keyword.IBM_notm}} solicita que você conclua as tarefas a seguir:

<ul>
<li>Mova uma cópia dos dados de backup criptografados externos, exatamente como faria para quaisquer outros dados de backup gerenciados.</li>
<li>Forneça os arquivos de backup para o administrador da {{site.data.keyword.IBM_notm}} no caso de qualquer necessidade de restauração.</li>
</ul>

# rellinks
{: rellinks}
## general
{: general}
* [Descobrir: {{site.data.keyword.Bluemix_local_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/bluemix/hybrid/local/){: new_window}
* [O que há de novo no {{site.data.keyword.Bluemix_notm}}](/docs/whatsnew/index.html)
* [{{site.data.keyword.Bluemix_notm}} glossário](/docs/overview/glossary/index.html)
* [Gerenciando o {{site.data.keyword.Bluemix_local_notm}} e o {{site.data.keyword.Bluemix_notm}} Dedicated](/docs/admin/index.html#mng)
* [Entrando em contato com o suporte](/docs/support/index.html#getting-customer-support)
