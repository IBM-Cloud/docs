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

## Visualizando dados com gráficos customizados
{: #custom-charts}

É possível visualizar os dados de análise coletados em seu repositório de análise. Essa visualização é uma maneira poderosa de inspecionar dados para casos de uso específicos. É possível criar gráficos com dados que já estão coletados pelo Operational Analytics, além de dados customizados que você relatar.

### Criando gráficos customizados para logs do cliente
{: #custom-charts-client-logs}

É possível criar um gráfico customizado para logs do cliente que contêm informações de log que são enviadas com a API do Criador de logs para a plataforma. As informações de log também incluem informações contextuais sobre o dispositivo, incluindo ambiente, nome do aplicativo e versão do aplicativo.

Neste exemplo, você usa dados do log do cliente para criar um fluxograma. O gráfico final mostra a distribuição de níveis de log em um aplicativo específico. Você também tem os dados a seguir disponíveis para mostrar em um gráfico:

* Dados específicos
  * Nível de Registro
* Dados da Mensagem
  * Registro de Data e Hora
* Dados contextuais do S.O. do dispositivo
  * Nome do Aplicativo
  * Versão do aplicativo
  * Sistema Operacional do Dispositivo
* Dados contextuais do dispositivo
  * ID do dispositivo
  * Modelo do dispositivo
  * Versão do S.O. do dispositivo


1. Certifique-se de que você tenha um aplicativo que está coletando logs do dispositivo ou reunindo análise.
2. No console do {{site.data.keyword.mobileanalytics_short}}, clique na guia **Gráficos customizados** na página **Painel**. É possível criar um gráfico baseado nas mensagens de análise que foram enviadas para o servidor.
3. Clique em **Criar gráfico** para criar um novo gráfico customizado e forneça os valores a seguir:
  * Título do gráfico: níveis de aplicativo e de log
  * Tipo de evento: logs do cliente
  * Tipo de gráfico: fluxograma
5. Clique na guia **Definição de gráfico** e forneça os valores a seguir:
  * Origem: nome do aplicativo
  * Destino: nível de log
  * Propriedade: seu nome do aplicativo
7. Clique em**Salvar**

### Exportando dados customizados
{: #export-custom-data}

É possível exportar os dados de cada gráfico customizado no formato JSON, XML ou CSV.

A estrutura dos dados exportados depende do gráfico que está sendo exportado. Para exportar dados, clique no ícone de exportação na parte superior direita do gráfico customizado.



### Exportando e importando definições de gráfico customizadas
{: #export-import-custom}

É possível importar e exportar definições de gráfico customizadas programaticamente ou manualmente no Painel do {{site.data.keyword.mobileanalytics_short}}.

Assegure-se de que você tenha pelo menos um gráfico customizado no Painel do {{site.data.keyword.mobileanalytics_short}}.
Neste exemplo, você exporta e importa manualmente as definições de gráfico customizadas.

1. No console do {{site.data.keyword.mobileanalytics_short}}, clique na guia **Gráficos customizados** na página **Painel**.
2. Para exportar as definições de gráfico customizadas, clique em **Exportar gráficos**. Essa ação exibe um diálogo para salvar um arquivo `customChartsDefinition.json`.
3. Escolha um local para salvar o arquivo.
4. Clique no ícone **Excluir gráfico** próximo a cada gráfico customizado para excluir todos os gráficos customizados.
5. Para importar uma definição de gráfico customizada, clique em **Importar gráficos**. Essa ação exibe um diálogo para escolher um arquivo.
6. Escolha o arquivo `customChartsDefinition.json` que você exportou anteriormente para abrir.

Também é possível exportar e importar definições de gráfico customizadas programaticamente usando sua opção de cliente HTTP (por exemplo, CURL ou postman):
* O terminal GET para exportação é `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* O terminal POST para importação é `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Nota**: se você importar uma definição de gráfico customizada existente, acabará com definições duplicadas, o que também significa que o Painel do {{site.data.keyword.mobileanalytics_short}} mostra gráficos customizados duplicados.

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


