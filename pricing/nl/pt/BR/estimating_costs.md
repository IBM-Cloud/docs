---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Estimando seus custos
{: #cost}

É possível usar diferentes métodos para saber quanto você precisa pagar para usar o {{site.data.keyword.Bluemix_notm}} para construir e hospedar seu app.

* Os estimadores de custo na {{site.data.keyword.pricing_sheet}} do {{site.data.keyword.Bluemix_notm}}
fornecem uma estimativa aproximada do custo com base no tamanho de seu app.
* A calculadora de custo na página Precificação do {{site.data.keyword.Bluemix_notm}} fornece preços de apps precisos com base em sua entrada de usos de tempo de execução e de serviço.
* Também é possível calcular seu custo manualmente.

## Usando os calculadores de custo
{: #calculator}

É possível precificar rapidamente seu app usando os calculadores de custo que são fornecidos pelo {{site.data.keyword.Bluemix_notm}}.

1. Acesse o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}.
2. Use um dos widgets de Infraestrutura ou clique em **Calculadora de precificação**.

Para usar a calculadora, digite seu uso mensal projetado dos recursos listados, por exemplo, o número de instâncias ou de notificações push. Clique dentro do campo **Uso mensal** para obter sugestões sobre as unidades esperadas no campo. A calculadora exibe o preço de sua entrada imediatamente. Também é possível ajustar a calculadora para exibir custos anuais, em vez de mensais.

## Calculando seus custos manualmente
{: #manual}

Talvez você mesmo queira estimar os custos do {{site.data.keyword.Bluemix_notm}}, para entender melhor como são calculados os custos do {{site.data.keyword.Bluemix_notm}}. É possível calcular o preço total do uso do {{site.data.keyword.Bluemix_notm}} para construir e hospedar seu app considerando os preços do tempo de execução e os serviços que ele usa. Os preços de tempos de execução e serviços às vezes mudam, de modo que deve-se consultar as últimas informações na planilha de precificação do {{site.data.keyword.Bluemix_notm}} ao calcular o preço total.

## Exemplo: Precificando um app de amostra
{: #sample}

Suponha que você tenha um app da web Node.js com recursos de escalabilidade e que o app use vários serviços que são fornecidos pelo {{site.data.keyword.Bluemix_notm}}. É possível aprender como o custo real de seu app é calculado neste exemplo. O app da web usa os serviços e itens do {{site.data.keyword.Bluemix_notm}} a seguir:

* Quatro instâncias de tempo de execução do Node.js de 256 MB
* Duas políticas de {{site.data.keyword.autoscaling}}, processador e memória
* 2 GB por mês de {{site.data.keyword.datacshort}}
* 150 GB por mês de banco de dados NoSQL, 100.000 chamadas API pesadas e 500.000 chamadas API leves
* 20 GB de tráfego de rede de entrada e saída

## Preços para recursos do Bluemix
{: #sample_resources}

Para manter o exemplo simples, suponha que os preços na tabela a seguir não flutuem dentro ou entre um prazo, por exemplo, um mês. Toda a precificação neste exemplo é em moeda dos EUA.

|Serviço |	Recursos |	Preço |
|--------|-----------|--------|
|SDK for Node.js |	375 GB/horas grátis por mês (compartilhados entre todos os tempos de execução) |	$0,07 USD/GB/hora|
|Ajuste automático de escala |	Plano de serviço grátis para o serviço de ajuste automático de escala |	Grátis|
|Data Cache - Iniciador |	1 GB de espaço em cache e uma réplica |	$55,00 USD/instância |
|Data Cache - Padrão |	5 GB de espaço em cache e uma réplica |	$155,00 USD/instância |
|Data Cache - Premium |	25 GB de espaço em cache e uma réplica |	$505,00 USD/instância|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2 GB de armazenamento de dados grátis<br/>50.000 chamadas API leves grátis por mês<br/>10.000 chamadas API pesadas grátis por mês | $1,00 USD/GB<br/>$0,03 USD/1000 chamadas API leves<br/>$0,15 USD/1000 chamadas API pesadas |
{:caption="Tabela 1. Folha de precificação" caption-side="top"}

## Calculando o preço do app

O preço do app pode ser calculado da maneira a seguir:

<dl>
<dt>Quatro instâncias de tempo de execução do Node.js de 256 MB</dt>
<dd>O Bluemix cobra por tempo de execução por GB/horas. O número de GB usado por mês é <code>4 x 256 = 1024 MB ou 1 GB por mês</code>. Suponha que haja <code>24 x 30 = 720 horas em um mês</code>, portanto, o aplicativo é cobrado por <code>1 x 720 = 720 GB/horas</code>.
<p>
375 GB/horas são incluídos em um abono grátis por mês, compartilhados entre todos os tempos de execução do {{site.data.keyword.Bluemix_notm}}. Assim, o custo total para o tempo de execução é <code>$0,07 x (720-375) = $24,15</code>.</p></dd>

<dt>Duas políticas de ajuste automático de escala (processador e memória)</dt>
<dd>As políticas de ajuste automático de escala são livres de encargos.</dd>

<dt>2 GB por mês de cache de dados</dt>
<dd>O plano de 50 MB que é fornecido pelo serviço de Cache de Dados é livre de encargos. Porém, o plano livre não cobriria o seu uso projetado de 2 GB por mês. O três planos pagos para o Cache de Dados custam uma quantia configurada para uma quantia de espaço específica, independentemente de quanto espaço você realmente usa. Portanto, você deseja escolher o plano mínimo que atenda ao seu uso projetado, que é o plano padrão de 5 GB. O custo total é de $155 por mês.</dd>

<dt>150 GB por mês no banco de dados NoSQL</dt>
<dd>Os encargos do serviço IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}} são baseados no armazenamento de dados e na capacidade de acessar esses dados por diferentes métodos de API. Os comandos <strong>PUT</strong> e <strong>POST</strong> são considerados como chamadas API pesadas, mas os comandos <strong>GET</strong> são considerados como chamadas API leves.
<p>
Inclua o número de GB e deduza um abono grátis de 2 GB. 148 GB é cobrado por mês. Subtraia o abono grátis de 50.000 para chamadas API leves e 10.000 para chamadas API pesadas. O preço total do armazenamento inclui as partes a seguir:</p>
<pre class="codeblock">
<codeblock>
    148 x 1 = $148
    (450.000 / 1000) x 0,03 = $13,5
    (90.000 / 1000) x 0,15 = $13,5
</codeblock>
</pre>
<p>
O preço total é 148 + 13,5 + 13,5 = $175.</p></dd>

<dt>20 GB de tráfego de rede de entrada e saída</dt>
<dd>O tráfego de rede de entrada e saída é livre de encargo.</dd>

</dl>

Quando todos os itens são incluídos, o preço total do aplicativo é de US$ 354,15.

## Moedas suportadas

Embora o dólar dos Estados Unidos (USD) seja usado nos exemplos de precificação, outras moedas também são suportadas no {{site.data.keyword.Bluemix_notm}}. A tabela a seguir lista as diferentes moedas que são suportadas.

|Código ISO 4217| Código ISO de Moedas (ex.: BRL = Real , USD = Dólar, EUR = Euro)|
|-------------|---------|
|AUD |	  Dólar australiano|
|BRL |	  Real brasileiro|
|CAD |	  Dólar canadense|
|CHF |	  Franco suíço|
|DKK |	  Coroas dinamarquesas|
|EUR |	  Euro|
|GBP |	  Libra Esterlina|
|INR |	  Rúpia Indiana|
|JPY |	  Iene japonês|
|KRW |	  Uon sul-coreano|
|NOK |	  Coroa Norueguesa|
|NZD |	  Dólar da Nova Zelândia|
|SEK |	  Coroa sueca|
|vermelho cereja |    Dólar americano|
|ZAR |	  Rand sul-africano|
{:caption="Tabela 2. Moedas suportadas" caption-side="top"}

**Observação:** se você vinculou suas contas {{site.data.keyword.Bluemix_notm}} e SoftLayer, a fatura única que você recebe será somente em dólares dos Estados Unidos (USD).
