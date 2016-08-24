---

copyright:
  years: 2015, 2016

---
# Monitorando aplicativos com o {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}
*Última atualização: 6 de maio de 2016*
{: .last-updated}

O {{site.data.keyword.mobileanalytics_full}} fornece monitoramento e análise para seus aplicativos móveis. É
possível registrar logs de clientes e monitorar dados com o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}. Os desenvolvedores podem controlar quando enviar esses dados para o serviço {{site.data.keyword.mobileanalytics_short}}. Quando os dados são entregues no {{site.data.keyword.mobileanalytics_short}}, é possível usar o painel do {{site.data.keyword.mobileanalytics_short}} para obter insights de análise sobre os aplicativos móveis, dispositivos e logs do cliente.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for client logs
{: #custom-charts-client-logs}

You can create a custom chart for client logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use client log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

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
  * Event Type: Client Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your app name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

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

Você pode configurar limites em definições de alerta no {{site.data.keyword.mobileanalytics_short}} Console para monitorar melhor suas atividades.

É possível configurar limites que, se excedidos, acionarão alertas para notificar o monitor do Console do {{site.data.keyword.mobileanalytics_short}}. Os alertas acionados podem ser visualizados no console ou os alertas podem ser manipulados por um webhook customizado. Esse recurso fornece um meio proativo de detectar erros de log do cliente, erros de log do servidor, longos períodos de latência de rede e falhas de autenticação. Limites e alertas reativos evitam que você filtre seus dados e configure limites em um amplo espectro de granularidade.

### Criando uma definição de alerta para logs do cliente
{: #alert-def-client-logs}

É possível criar uma definição de alerta que é baseada em logs do cliente.

Neste exemplo, você usa os dados do log do cliente para criar uma definição de alerta. O alerta monitora todos os logs do cliente que foram recebidos nos últimos 5 minutos e continua a verificação a cada 5 minutos, até que a definição de alerta seja desativada ou excluída. Um alerta é acionado para cada dispositivo que enviou 3 ou mais logs de erro do cliente com o mesmo nome e versão de aplicativo.

1. No Console do {{site.data.keyword.mobileanalytics_short}}, clique no ícone de sino para acessar a página **Log de alerta**.
2. Acesse a página **Gerenciamento de alerta** e clique em **Criar alerta**.
3. Forneça os seguintes valores:
	* Nome do alerta: alerta para logs do cliente
	* Mensagem: alerta de mensagem de erro
	* Frequência de consulta: 5 minutos
	* Tipo de evento: logs do cliente
		* Propriedade: nível de log
			* Valor: erro
			* Tipo de Limite
				* Tipo de limite: total para instância do aplicativo

					**Nota**: se você escolher a opção Média para o aplicativo, os logs do cliente serão calculados pelo número de dispositivos. Por exemplo, se você tiver dois dispositivos, e um dispositivo enviar seis logs do cliente enquanto o outro dispositivo enviar três logs do cliente, a média será 4,5 logs do cliente.
				* Operador: é maior que ou igual a 3
	<!-- insert alert definition tab image? -->

4. Clique em **Avançar** ou na guia **Método de distribuição** e forneça o valor a seguir:
	* Método: somente console de análise

		Nota: escolha a opção Console de análise e post de rede se desejar também enviar uma mensagem POST com uma carga útil JSON para sua URL customizada. Os campos a seguir estarão disponíveis se você escolher essa opção:
		* URL para autoteste inicial da rede
        * Cabeçalhos
        * Tipo de Autenticação
5. Clique em **Salvar (Save)**.

Você criou uma definição de alerta para acionar um alerta no término de cada intervalo 5 minutos se o número de logs do cliente atingiu seu limite de 3 ou mais logs de erro.

### Criando uma definição de alerta para travamentos de aplicativo
{: #alert-def-app-crash}

É possível criar uma definição de alerta baseada em travamentos de aplicativo.

Neste exemplo, você usa os dados de travamento de aplicativo para criar uma definição de alerta. O alerta monitora todos os travamentos de aplicativo nos últimos 2 minutos e continua a verificação a cada 2 minutos, até que a definição de alerta seja desativada ou excluída. Um alerta é acionado para cada aplicativo que travou 5 ou mais vezes. Para obter mais informações sobre travamentos de aplicativo, veja [Travamentos de aplicativo](app_crash/c_op_analytics_crashes.html).

1. No Console do {{site.data.keyword.mobileanalytics_short}}, clique no ícone **Alertas**. Essa ação abre a página Log de alerta.
2. Clique na guia **Gerenciamento de alerta** e clique em **Criar alerta**.
3. Forneça os seguintes valores:
	* Nome do alerta: alerta para travamentos de aplicativo
	* Mensagem: alerta de travamento de aplicativo
	* Frequência de consulta: travamentos de aplicativo
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
{: #managing-alert-definitions}

Neste exemplo, você gerencia suas definições de alerta a partir da página Gerenciamento de alerta.

1. No Console do {{site.data.keyword.mobileanalytics_short}}, clique no ícone **Alertas**. Essa ação abre a página Log de alerta.
2. Clique na guia **Gerenciamento de alertas**.
3. Opcional: alterne a caixa de seleção sob a coluna **Ativado** para ativar ou desativar uma definição de alerta específica.
4. Opcional: clique no ícone **Duplicar** se desejar criar uma cópia de uma definição de alerta e mudar alguns valores.
5. Opcional: clique no ícone **Lápis** se desejar editar uma definição de alerta.
6. Opcional: clique no ícone **Lixeira** se desejar excluir uma definição de alerta.

### Visualizando Detalhes de Alerta
{: #viewing-alert-details}

Neste exemplo, você visualiza os detalhes de seus alertas acionados a partir da página Log de alerta.

1. No Console do {{site.data.keyword.mobileanalytics_short}}, clique no ícone **Alertas**. Essa ação abre a página Log de alerta.
2. Clique no ícone **+** para qualquer um dos alertas. Essa ação exibe as seções **Definição de alerta** e **Instâncias de alerta**.

    **Nota**: se a definição de alerta correspondente não foi excluída nem modificada, será possível editar a definição de alerta clicando em **Editar alerta**. Caso contrário, o botão **Editar alerta** estará indisponível e a mensagem a seguir será exibida:

    `Essa definição de alerta foi modificada ou excluída.`

3. Opcional: selecione um alerta e clique no ícone **Lixeira** para excluir o alerta.

## Travamentos de aplicativo
{: #monitor-app-crash}

É possível visualizar informações sobre travamento de aplicativo no Console do {{site.data.keyword.mobileanalytics_short}} para monitorar melhor e solucionar problemas de seus aplicativos.

### Monitoramento de travamento de aplicativo
{: #app-crash}

É possível ver rapidamente as informações sobre travamentos de aplicativo na seção **Painel** do Console do {{site.data.keyword.mobileanalytics_short}}.

Na página **Visão Geral** da seção **Painel**, o gráfico de barras **Travamentos** mostra um histograma de travamentos ao longo do tempo.

É possível exibir dados de duas maneiras:

1. Exibir taxa de travamento: taxa de travamento ao longo do tempo
2. Exibir total de travamentos: total de travamentos ao longo do tempo


### Resolução de problemas de travamento de aplicativo
{: #app-crash-troubleshooting}

É possível visualizar a página **Travamentos** na seção **Aplicativos** do Console do {{site.data.keyword.mobileanalytics_short}} administrar melhor seus aplicativos.

A tabela **Visão geral de travamento** mostra as colunas de dados a seguir:

* Aplicativo: nome do aplicativo
* Travamentos: número total de travamentos para esse aplicativo
* Total de usos: número total de vezes que um usuário abre e fecha esse aplicativo
* Taxa de travamento: porcentagem de travamentos por uso

A tabela **Resumo de travamento** é classificável e inclui as colunas de dados a seguir:

* Travamentos
* Dispositivos
* Último travamento
* Aplic.
* OS
* Message

É possível clicar no ícone + próximo a qualquer entrada para exibir a tabela **Detalhes do travamento**, que inclui as colunas a seguir:

* Horário do travamento
* Versão do Aplicativo
* Versão do Sistema Operacional
* Modelo de dispositivo
* ID do dispositivo
* Download: link para fazer download dos logs que levaram ao travamento

É possível expandir qualquer entrada na tabela **Detalhes do travamento** para obter mais detalhes, incluindo um rastreio de pilha.

**Nota**: os dados para a tabela **Resumo de travamento** é preenchida consultando os logs do cliente de nível fatal. Se seu aplicativo não coletar logs do cliente fatais, nenhum dado estará disponível.


