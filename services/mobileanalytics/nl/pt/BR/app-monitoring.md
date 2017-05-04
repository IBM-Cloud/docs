---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoramento de aplicativos com o {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}

O {{site.data.keyword.mobileanalytics_full}} fornece monitoramento e análise para seus aplicativos móveis. É possível registrar logs do aplicativo e monitorar dados com o SDK do cliente {{site.data.keyword.mobileanalytics_short}}. Os desenvolvedores podem controlar quando enviar esses dados para o serviço {{site.data.keyword.mobileanalytics_short}}. Quando os dados forem entregues para o {{site.data.keyword.mobileanalytics_short}}, será possível usar o console do {{site.data.keyword.mobileanalytics_short}} para obter insights analíticos sobre seus aplicativos, dispositivos e logs do aplicativo.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts notoc}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs notoc}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data notoc}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom notoc}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## Configurando alertas
{: #alerts}

É possível configurar limite nas definições de alerta no console do {{site.data.keyword.mobileanalytics_short}} para monitorar melhor suas atividades.

É possível configurar limites que, se excedidos, acionarão alertas para notificar o monitor do console do {{site.data.keyword.mobileanalytics_short}}. Os alertas acionados podem ser visualizados no console ou os alertas podem ser manipulados por um webhook customizado. <!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> Esse recurso fornece um meio proativo de detectar erros de log do aplicativo e erros de log do servidor de travamentos de aplicativo. Limites e alertas reativos evitam que você filtre seus dados e configure limites em um amplo espectro de granularidade.

### Criando uma definição de alerta para logs do aplicativo
{: #alert-def-client-logs notoc}

É possível criar uma definição de alerta que é baseada em logs do aplicativo.

Neste exemplo, você usa os dados do log do aplicativo para criar uma definição de alerta. O alerta monitora todos os logs do aplicativo que foram recebidos nos últimos cinco minutos e continua a verificação a cada cinco minutos, até que a definição de alerta seja desativada ou excluída. Um alerta é acionado para cada dispositivo que enviou três ou mais logs de erro de aplicativo com o mesmo nome e versão do aplicativo.

1. No console do {{site.data.keyword.mobileanalytics_short}}, clique em **Definições** para acessar a página Definições de alerta.
2. Clique em **Criar alerta** para criar um alerta.
3. Forneça os seguintes valores:
	* Nome do alerta: alerta para logs de app
	* Mensagem: alerta de mensagem de erro
	* Frequência de consulta: 5 minutos
	* Tipo de evento: logs de app
		* Propriedade: nível de log
			* Valor: erro
			* Tipo de Limite
				* Tipo de limite: total para instância do aplicativo

					**Nota**: se você escolher a opção Média para o aplicativo, será feita uma média dos logs de app pelo número de dispositivos. Por exemplo, se você tem dois dispositivos e um dispositivo envia seis logs de app enquanto o outro dispositivo envia três logs de app, a média é de 4,5 logs de app.
				* Operador: é maior que ou igual a 3
	<!-- insert alert definition tab image? -->

4. Clique em **Avançar** e forneça o valor a seguir:
	* Método: somente console de análise

		**Nota**: escolha a opção Console de analítica e Post de rede se também desejar enviar uma mensagem POST com uma carga útil JSON para sua URL customizada. Os campos a seguir estarão disponíveis se você escolher essa opção:
		* URL para autoteste inicial da rede
        * Cabeçalhos
        * Tipo de Autenticação
5. Clique em **Salvar (Save)**.

Você criou uma definição de alerta para acionar um alerta no término de cada intervalo de 5 minutos se o número de logs de app atingir seu limite de 3 ou mais logs de erro.

### Criando uma definição de alerta para travamentos de aplicativo
{: #alert-def-app-crash notoc}

É possível criar uma definição de alerta baseada em travamentos de aplicativo.

Neste exemplo, você usa os dados de travamento de aplicativo para criar uma definição de alerta. O alerta monitora todos os travamentos de aplicativo nos últimos dois minutos e continua a verificação a cada dois minutos, até que a definição de alerta seja desativada ou excluída. Um alerta é acionado para cada aplicativo que travou cinco ou mais vezes. Para obter mais informações sobre travamentos de aplicativo, veja [Travamentos de aplicativo](#app_crash).

1. No console do {{site.data.keyword.mobileanalytics_short}}, clique em **Definições** para exibir a página Definições de alertas.
2. Clique em **Criar alerta**.
3. Forneça os seguintes valores:
	* Nome do alerta: alerta para travamentos de aplicativo
	* Mensagem: alerta de travamento de aplicativo
	* Frequência de consulta: travamentos de aplicativo
		* Frequência de consulta: 2 minutos
	* Tipo de evento: travamentos do aplicativo
		* Nome do aplicativo: qualquer aplicativo
		* Versão do aplicativo: qualquer versão
    * Tipo de Limite
      * Tipo de limite: contagem de travamentos
      * Operador: é maior que ou igual a 5
4. Clique na guia **Método de distribuição** e forneça o valor a seguir:
  * Método: somente console de análise

    **Nota**: escolha a opção **Console de análise e post de rede** se desejar também enviar uma mensagem POST com uma carga útil JSON para sua URL customizada. Os campos a seguir estarão disponíveis se você escolher essa opção:
      * URL de post de rede (obrigatório)
      * Cabeçalhos (opcional)
      * Tipo de autenticação (obrigatório)
5. Clique em **Salvar (Save)**.

### Gerenciando definições de alerta
{: #managing-alert-definitions notoc}

Neste exemplo, você gerencia suas definições de alerta a partir da página Gerenciamento de alerta.

1. No console do {{site.data.keyword.mobileanalytics_short}}, clique em **Logs**. Essa ação abre a página Logs de alerta.
2. Opcional: alterne a caixa de seleção sob a coluna **Ativado** para ativar ou desativar uma definição de alerta específica.
3. Opcional: clique no ícone **Duplicar** se desejar criar uma cópia de uma definição de alerta e mudar alguns valores.
4. Opcional: clique no ícone **Lápis** se desejar editar uma definição de alerta.
5. Opcional: clique no ícone **Lixeira** se desejar excluir uma definição de alerta.

### Visualizando Detalhes de Alerta
{: #viewing-alert-details notoc}

Neste exemplo, você visualiza os detalhes de seus alertas acionados a partir da página Log de alerta.

1. No console do {{site.data.keyword.mobileanalytics_short}}, clique em **Logs**. Essa ação abre a página Log de alerta.
2. Clique no ícone **+** para qualquer um dos alertas. Essa ação exibe as seções **Definição de alerta** e **Instâncias de alerta**.

    **Nota**: se a definição de alerta correspondente não foi excluída nem modificada, será possível editar a definição de alerta clicando em **Editar alerta**. Caso contrário, o botão **Editar alerta** estará indisponível e a mensagem a seguir será exibida:

    `Essa definição de alerta foi modificada ou excluída.`

3. Opcional: selecione um alerta e clique no ícone **Lixeira** para excluir o alerta.

## Monitoramento de travamentos de aplicativo
{: #monitor-app-crash}

É possível visualizar informações sobre travamentos do seu aplicativo no console do {{site.data.keyword.mobileanalytics_short}} para monitorar melhor e solucionar problemas de seus aplicativos.

### Monitoramento de travamento de aplicativo
{: #app-crash notoc}

Na página **Travamentos**, a tabela **Visão geral de travamento** mostra as colunas de dados a seguir:

* Aplicativo: nome do aplicativo
* Travamentos: número total de travamentos para esse aplicativo
* Total de usos: número total de vezes que um usuário abre e fecha esse aplicativo
* Taxa de travamento: porcentagem de travamentos por uso

É possível ver rapidamente as informações sobre os travamentos de seu aplicativo na tabela **Travamentos**.
<!--In the **Overview** page of the **Dashboard** section,--> O gráfico de barras **Travamentos** mostra um histograma de travamentos ao longo do tempo.

É possível exibir dados de travamento de duas maneiras:

1. Exibir taxa de travamento: taxa de travamento ao longo do tempo
2. Exibir total de travamentos: total de travamentos ao longo do tempo

### Resolução de problemas de travamento de aplicativo
{: #app-crash-troubleshooting notoc}

A página **Resolução de problemas** no console do <!-- **Applications** section of the --> {{site.data.keyword.mobileanalytics_short}} oferece uma visualização granular dos travamentos do seu app, usando a tabela **Resumo do travamento**.

A tabela **Resumo de travamento** é classificável e inclui as colunas de dados a seguir:

* Travamentos
* Dispositivos
* Último travamento
* Aplicativo
* OS
* Message

Clique no ícone + próximo a qualquer entrada para exibir a tabela **Detalhes do travamento**, que inclui as colunas a seguir:

* Horário do travamento
* Versão de Aplicativo
* Versão do Sistema Operacional
* Modelo de dispositivo
* ID do dispositivo
* Download: link para fazer download dos logs que levaram ao travamento

Expanda qualquer entrada na tabela **Detalhes do travamento** para obter mais detalhes, incluindo um rastreio de pilha.

**Nota**: os dados da tabela **Resumo de travamento** são preenchidos consultando os logs de app de nível fatal. Se o seu aplicativo não coletar logs do aplicativo fatais, nenhum dado estará disponível.

## Monitorando solicitações de rede
{: #monitor-network-requests}


Visualize os dados da solicitação de rede para seus aplicativos no console do {{site.data.keyword.mobileanalytics_short}}. 

Os dados estão disponíveis para as medidas a seguir:
	
* Tempo de roundtrip - define o período de tempo, medido em ms, que é necessário para o seu app para fazer solicitações de rede.
* Contagem de solicitações - exibe com que frequência um app faz solicitações de rede. Os dados também são exibidos como uma média.

## Exportando dados para o dashDB
{: #dashdb}

As métricas que você vê no console do {{site.data.keyword.mobileanalytics_short}} são apenas uma amostra dos insights que podem ser obtidos de seus dados móveis. É possível canalizar automaticamente seus dados móveis para o data warehouse do {{site.data.keyword.IBM}} dashDB, no qual é possível customizar suas análises, agregar seus dados com outras fontes de dados públicas e privadas e aplicar analítica de ponta para derivar insights profundos, detalhados e sofisticados para ajudá-lo a entender e impulsionar seus negócios.

Configure o dashDB no console do {{site.data.keyword.mobileanalytics_short}} clicando em **DashDB** na página **Exportar**. Após concluir a configuração, novos dados enviados para o {{site.data.keyword.mobileanalytics_short}} também serão encaminhados para o dashDB dentro de uma a duas horas. 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

