---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sobre o Insights for Weather
{: #about_weather}

*Última atualização: 19 maio de 2016*

Use o
{{site.data.keyword.weatherfull}}
para incorporar dados de clima da The Weather Company (TWC) para seus
aplicativos do
{{site.data.keyword.Bluemix}}.
{:shortdesc}

É possível incluir observações e previsões de clima no aplicativo {{site.data.keyword.Bluemix_notm}} e exibir os dados de clima
para uma área especificada por uma localização geográfica usando as [APIs REST do Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window}.
O Weather Company é o provedor de dados de clima históricos e previstos
mais abrangente. Dados para todas as formas de clima,
incluindo precipitação, pressão barométrica, vento e raios são capturados.

É possível usar as APIs REST para recuperar as informações a seguir:

* Uma previsão climática de hora em hora para as próximas 24 horas, a partir do horário atual para uma determinada localização
geográfica.
* Uma previsão climática diária para os próximos 10 dias, que
inclui as previsões para os segmentos diurnos e
noturnos para uma determinada localização geográfica. Esta previsão inclui a sequência de caracteres de texto narrativo da previsão, de até 256 caracteres, com unidades apropriadas de medida para a localização, e no idioma solicitado.
* Os dados de clima atuais observados para uma localização
geográfica especificada. Estes dados de clima incluem temperatura, precipitação, direção e velocidade do vento, umidade, pressão
barométrica, ponto de condensação, visibilidade e radiação
ultravioleta (UV).
* Os dados de clima observados para uma localização geográfica especificada e um
intervalo de tempo especificado. Estes dados são originados a
partir de estações de observação físicas. Esta
API retorna observações de clima para as condições atuais e
observações passadas até e incluindo as 24 horas anteriores.

Para obter mais informações sobre frases e ícones de clima da The Weather Company, consulte [Código do Ícone, Frases e Imagens](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
Também é possível [fazer download de um conjunto de ícones](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} para usar em seu app.

## Modelo de precificação
{: #pricing_models}

O modelo de precificação baseia-se em chamadas diárias para as APIs do Insights for Weather que
são cobradas do cliente mensalmente. É possível testar os dados
de clima em seus aplicativos para qualquer área geográfica, tipo de
previsão ou observações de séries temporais com apenas uma restrição
quanto ao número de chamadas. Os planos Gratuito, Base e Premium
podem ser comprados sem um contrato. Esses planos permitem que o app faça 500, 5.000 ou 50.000
chamadas API por dia, respectivamente.

Diversos planos Premium também podem ser adquiridos para cada instância de serviço implementada durante o
período de faturamento. Se o seu app usa mais de 50.000 chamadas por dia ou mais de 1.000 chamadas por minuto,
é necessário um contrato com a IBM para a provisão contínua de serviços.

Quando o seu app atinge o limite de chamadas API que podem ser feitas com base no plano selecionado,
a próxima chamada API feita não será bem-sucedida até que o app tenha permissão para solicitar mais
chamadas API.

Por exemplo, se você estiver usando o plano Base, o app poderá fazer 500 chamadas de API em um
minuto, mesmo que exceda o limite do plano, mas a próxima chamada API não será permitida até 5 minutos
depois. Portanto, um usuário poderá observar um atraso na atualização de dados de clima em seu app. Deve-se garantir que você desenvolva o seu app para manipular esses limites e não solicitar bursts de chamadas
API. Em vez disso, é possível
monitorar o uso de chamadas API de seu app. É possível verificar se o seu app atinge
o limite de seu plano verificando o número de itens retornados pela chamada API.

## Feedback e suporte
{: #feedback_support}

Se você tiver questões técnicas sobre a criação de um app com o Insights for Weather,
poste sua pergunta no [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window}
e identifique-a com **bluemix** e **weather**.

Se você tiver problemas com esse serviço, use o [fórum do IBM developerWorks Answers](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Inclua as tags **insights-weather** e **bluemix** para permitir que a IBM ofereça o melhor suporte.

Para obter informações sobre resolução de problemas com o
Bluemix, consulte
[Resolução
de problemas](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Para obter detalhes sobre a procura de informações, realização de perguntas nos fóruns e entrar em contato com o suporte, consulte [Obtendo suporte ao cliente](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
