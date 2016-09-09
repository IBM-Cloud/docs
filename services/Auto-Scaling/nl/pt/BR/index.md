{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao serviço {{site.data.keyword.autoscaling}}
{: #autoscaling}

*Última atualização: 18 de janeiro de 2015*

No {{site.data.keyword.Bluemix_notm}}, é possível gerenciar automaticamente a capacidade de seu aplicativo. Use o serviço {{site.data.keyword.autoscalingfull}} para aumentar ou diminuir automaticamente
a capacidade de cálculo de seu aplicativo. O número de instâncias do aplicativo é ajustado
dinamicamente com base na política do {{site.data.keyword.autoscaling}} que você define.
{:shortdesc} 

## Usando o serviço {{site.data.keyword.autoscaling}} no {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Para usar o serviço
{{site.data.keyword.autoscaling}},
conclua as etapas a seguir:

1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique em *Incluir um serviço ou API* e, em seguida, selecione o serviço {{site.data.keyword.autoscaling}} a partir da seção DevOps no catálogo de serviços. Uma nova janela é exibida para apresentar uma visão geral do serviço {{site.data.keyword.autoscaling}}.
2. Selecione o aplicativo ao qual deseja ligar o serviço {{site.data.keyword.autoscaling}} e clique em *Criar*. <br/>
*Lembre-se:* É possível ligar somente um serviço {{site.data.keyword.autoscaling}} a um aplicativo. Se o aplicativo já está vinculado a outro serviço {{site.data.keyword.autoscaling}}, não selecione o aplicativo nesta etapa. Caso contrário, você obterá o erro CWSCV2004E.<br/>A janela Remontar aplicativo é exibida.
3. Na janela Remontar aplicativo, clique em *Remontar* para remontar seu aplicativo antes de usar o novo serviço {{site.data.keyword.autoscaling}} recém-incluído. Depois que a nova preparação do aplicativo estiver concluída, é possível começar a configurar o
						serviço {{site.data.keyword.autoscaling}} para seu aplicativo.
4. Para configurar o {{site.data.keyword.autoscaling}} para um aplicativo, na interface com o usuário do
{{site.data.keyword.Bluemix_notm}}, clique em seu aplicativo ao qual o serviço do {{site.data.keyword.autoscaling}} está ligado.
5. Na seção de serviços no Painel, clique no
						ícone *Auto-Scaling*.
6. Caso ainda não tenha feito isso, defina a política de {{site.data.keyword.autoscaling}} para o aplicativo clicando em *Criar política de {{site.data.keyword.autoscaling}}*.

Agora, é possível configurar a política de {{site.data.keyword.autoscaling}},
ver as estatísticas de métrica ou visualizar o histórico de ajuste de escala para o aplicativo.
<dl>
<dt>Configuração de política</dt>
<dd>Use essa seção para criar ou editar as regras de ajuste de escala para especificar as condições nas quais determinadas atividades de ajuste de escala devem ser acionadas.<ul>
<li> Para aplicativos Liberty for Java™, é possível definir regras de ajuste de escala para Heap da JVM, Memória e Rendimento.
<li> Para aplicativos Node.js, é possível definir regras de ajuste de escala para Memória.
<li> Para
aplicativos Ruby, é possível definir regras de ajuste de escala para Memória.</ul>
*Nota:* É possível definir várias regras de ajuste de escala para mais de um tipo de métrica. No entanto, o serviço {{site.data.keyword.autoscaling}} não detecta conflitos entre as políticas de ajuste de escala. Ao definir a política de ajuste de escala, devem-se assegurar que
							as múltiplas regras de ajuste de escala não entrem em conflito umas com as outras. Caso contrário, você pode ver o número total de instâncias flutuar porque o aplicativo diminui a escala em um minuto e aumenta a escala no minuto seguinte.<br/><br/>
Se a carga de trabalho de seu aplicativo muda dramaticamente durante o horário de pico e o horário sobressalente, é possível criar um planejamento de ajuste de escala para manipular os	diferentes requisitos de ajuste de escala para os diferentes períodos de tempo. Use o parâmetro Minimum Instance Count especificado em um planejamento para definir a linha de base do número de instâncias do aplicativo, embora as regras de ajuste dinâmico de escala ainda se apliquem ao planejamento para acionar as ações para diminuir a escala e aumentar a escala.</dd>
<dt>Estatísticas de métrica</dt>
<dd>Exibe as estatísticas de métrica para as instâncias de seu aplicativo. É possível ver a média de estatísticas e selecionar uma instância específica para
ver sua estatística.</dd>
<dt>Histórico de ajuste de escala</dt>
<dd>Exibe o histórico de ajuste de escala de seus aplicativos.<ul>
<li> Semana passada:
Exibe o histórico de ajuste de escala para a semana passada.
<li> Mês passado:
Exibe o histórico de ajuste de escala para o mês passado.
<li> Intervalo
customizado: é possível configurar o período.</ul>
*Nota:* É possível filtrar o registro de histórico selecionando Status de ajuste de escala ou Aumento/diminuição de ajuste de escala.</dd>
</dl>


## Campos de política para o serviço {{site.data.keyword.autoscaling}}
{: #policyfields}

| Nome do campo  | Descrição |
|-------------|----------------------|
|*Contagem máxima permitida de
instâncias* |	O número máximo das instâncias do aplicativo que podem ser
iniciadas. Se o número atual das instâncias do aplicativo for igual a esse valor, o serviço {{site.data.keyword.autoscaling}} não aumentará mais a escala do aplicativo. Contagem mínima de instâncias padrão. O número mínimo de instâncias do aplicativo que podem ser iniciadas. Se o número das instâncias for igual a esse valor, o serviço
{{site.data.keyword.autoscaling}} não diminuirá mais a escala do aplicativo. |
| *Tipo de métrica*	| 	Os tipos de métrica suportados que podem ser
monitorados. Para obter informações adicionais, veja a Tabela 2. |
| *Ampliar escala* | 	Especifica o limite que aciona uma ação de aumento de escala e quantas instâncias são aumentadas quando a ação de aumento de escala é acionada. |
| *Reduzir escala* |	Especifica um limite que aciona uma ação de diminuição de escala e quantas instâncias são
diminuídas quando a ação de diminuição de escala é acionada. |
| *Janela de estatística* |	A duração do período passado quando os valores da métrica recebidos são reconhecidos como válidos. Os valores da métrica
são válidos somente se os registros de data e hora estiverem dentro desse período. A unidade do parâmetro Statistic Window é segundo. |
| *Duração da violação*	| A duração do período passado quando uma ação de ajuste de escala pode ser acionada. Uma ação de ajuste de escala é acionada quando os valores da métrica coletados estão acima do
limite superior ou abaixo do limite inferior maior que o tempo especificado. A unidade do parâmetro Breach Duration é segundo. |
| *Período de espera para diminuir o ajuste de escala* | Depois que uma ação de diminuição de ajuste de escala ocorre, outras solicitações de ajuste de escala são ignoradas durante o período especificado pelo parâmetro Cooldown period for scaling in. A unidade desse parâmetro é segundo. |
| *Período de espera para aumentar o ajuste de escala*	| Depois que uma ação de aumento de ajuste de escala ocorre, outras solicitações de ajuste de escala são ignoradas durante o período especificado pelo parâmetro Cooldown period for scaling. A unidade desse parâmetro é segundo. |
| *Fuso horário*	| O fuso horário em que o planejamento se aplica. |
| *Horário de início*  |	O horário de início de um planejamento recorrente. |
| *Horário de encerramento*    |	O horário de encerramento de um planejamento recorrente.	|
| *Repetir em*	|	O dia da semana em que se aplica um planejamento recorrente. |
| *Contagem mínima de instâncias* |	O número mínimo de instâncias que podem ser iniciadas para o aplicativo
durante o período de tempo especificado no planejamento. |
| *Data e hora de início* |	A data e hora de início do planejamento configurado em uma data
específica. |
| *Data e hora de encerramento* |	A data e hora de encerramento do planejamento configurado em uma data específica.	|

Tabela 1. Campos de política na política de ajuste de escala

| Nome da métrica | Descrição | Tipo de aplicativo
suportado |
|-------------|----------------------| ------------------- |
| *Heap JVM* |	A porcentagem de uso da memória heap da JVM.	| Liberty for Java |
| *Memória*   |	A porcentagem de uso da memória.	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *Rendimento* | O número das solicitações processadas por
segundo.| Liberty for Java |
| *Tempo de resposta* |	O tempo de resposta das
solicitações processadas.	| Liberty for Java |

Tabela 2. Nomes de métricas suportados

## Mensagens de erro
{: #errmsgs}
Esta seção lista as mensagens de aviso e erro que são produzidas pelo serviço {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Outro serviço {{site.data.keyword.autoscaling}} já está vinculado
ao aplicativo.
**É possível ligar somente um serviço {{site.data.keyword.autoscaling}} a um aplicativo. Esse erro ocorre quando você deseja ligar o serviço {{site.data.keyword.autoscaling}} a um aplicativo que já está ligado a outro serviço {{site.data.keyword.autoscaling}}.**

Selecione outro aplicativo sem qualquer outro serviço {{site.data.keyword.autoscaling}} vinculado e vincule o serviço {{site.data.keyword.autoscaling}} de destino a esse aplicativo.
Se você encontrar esse erro em todos os outros casos, entre em contato com o suporte IBM.

### CWSCV6001E O servidor de API não pode analisar as sequências JSON de entrada para API: {0}.
**O problema ocorre ao analisar sequências JSON de entrada.**

Verifique o documento JSON de entrada com API e corrija o erro contido nele.

### CWSCV6002E O servidor API não pode analisar as sequências JSON de saída para API: {0}.
**O problema ocorre ao analisar sequências JSON de entrada.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6003E Erro do formato de sequências JSON de entrada: {0} no JSON de entrada para API: {1}.
**Erro de formatação localizado ao analisar as sequências JSON de entrada.**

Verifique o documento JSON de entrada com API e corrija o erro contido nele.

### CWSCV6004E Erro do formato de sequências JSON de saída: {0} no JSON de saída para API: {1}.
**Erro de formatação localizado ao analisar as sequências JSON de saída.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6005E Ocorreu um erro interno do servidor durante {0}.
**Ocorre o erro interno de servidor ao processar a solicitação.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6006E Falha ao chamar APIs CloudFoundry: {0}
**Ocorreu um erro ao chamar as APIs CloudFoundry.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6007E O aplicativo não foi localizado: {0}
**O aplicativo não foi localizado.**

Verifique as informações do aplicativo para obter mais informações.

### CWSCV6008E Ocorreu o erro a seguir ao recuperar as informações para o aplicativo {0}: {1}
**A recuperação de informações do aplicativo falhou com certos erros.**

Verifique as informações do aplicativo para obter mais informações.

### CWSCV6009E Serviço: {0} para App {1} não foi localizado.
**O serviço para esse aplicativo não pode ser localizado.**

Verifique a ligação de serviços para este aplicativo para obter mais informações.

### CWSCV6010E A política para App {0} não foi localizada
**A política para esse aplicativo não pode ser localizada.**

Verifique a configuração de aplicativo para obter mais informações.

### CWSCV6011E A Autenticação Interna falhou durante {0}
**Falha na autenticação interna.**

Entre em contato com o Administrador em nuvem para obter mais informações.


# rellinks
## SAMPLEs
* [Tutorial: Torne seu aplicativo elástico no {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Laboratórios da Arquitetura Cloud Foundry](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [API REST do IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## gerais
* [{{site.data.keyword.Bluemix_notm}}  Folha de precificação](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}}  Pré-requisitos](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}}CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

