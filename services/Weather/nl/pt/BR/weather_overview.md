---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sobre o {{site.data.keyword.weather_short}}
{: #about_weather}

Use o
{{site.data.keyword.weatherfull}}
para incorporar dados de clima da The Weather Company (TWC) para seus
aplicativos do
{{site.data.keyword.Bluemix}}.
{:shortdesc}

É possível incluir observações e previsões de clima no aplicativo {{site.data.keyword.Bluemix_notm}}
e exibir os dados de clima para uma área especificada por uma
localização geográfica usando as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window}.
O Weather Company é o provedor de dados de clima históricos e previstos
mais abrangente. Dados para todas as formas de clima,
incluindo precipitação, pressão barométrica, vento e raios são capturados.

É possível usar as APIs REST para recuperar as informações a seguir:

* Uma previsão climática de hora em hora para as próximas 48 horas que inicia a partir do horário atual para uma determinada localização geográfica.
* Uma previsão diária para cada um dos próximos 3, 5, 7 ou 10 dias, iniciando a partir do dia atual, que inclui previsões para os segmentos diurnos e noturnos para uma localização geográfica especificada. Esta previsão inclui a sequência de caracteres de texto narrativo da previsão, de até 256 caracteres, com unidades apropriadas de medida para a localização, e no idioma solicitado.
* Uma previsão diária para cada um dos próximos 3, 5, 7 ou 10 dias, a partir do dia atual, que divide cada previsão diária nos segmentos manhã, tarde e noite.
* Os dados de clima atuais observados para uma localização
geográfica especificada. Estes dados de clima incluem temperatura, precipitação, direção e velocidade do vento, umidade, pressão
barométrica, ponto de condensação, visibilidade e radiação
ultravioleta (UV).
* Os dados de clima observados para uma localização geográfica especificada até e incluindo as 24 horas anteriores. Estes dados são originados a
partir de estações de observação físicas.
* Alertas de clima emitidos pelo Governo, incluindo weather watches, avisos, declarações e avisos emitidos pelo National Weather Service (EUA), Environment Canada e MeteoAlarm (Europa).
* Serviços de almanaque que fornecem dados históricos de clima diários ou mensais provenientes de estações de observações do Serviço Nacional de Meteorologia a partir de um período que vai de 10 a 30 anos ou mais.
* Serviços de mapeamento de localização que fornecem a capacidade de procurar um nome ou uma localização geográfica do local (latitude e longitude) para recuperar um conjunto de locais que correspondem à sua
solicitação.

## Modelo de precificação
{: #pricing_models}

O modelo de precificação é baseado no número de chamadas por minuto para as APIs
REST. O cliente é cobrado mensalmente. Os planos Gratuito e Básico permitem que você
faça um máximo de 10 chamadas API por minuto. Os planos Padrão e Premium
permitem que você faça 150 e 375 chamadas API por minuto, respectivamente. Cada plano tem
um número máximo de chamadas API permitidas.

É possível testar os dados
de clima em seus aplicativos para qualquer área geográfica, tipo de
previsão ou observações de séries temporais com apenas uma restrição
quanto ao número de chamadas. Os planos Gratuito, Básico e Premium podem ser adquiridos
sem um contrato. O plano Gratuito permite que o seu aplicativo faça 10.000 chamadas. Os
planos restantes permitem que o seu aplicativo faça 150.000, 2 milhões
ou 5 milhões de chamadas API por mês, respectivamente.

Múltiplos planos pagos também podem ser comprados para cada instância de serviço implementada
durante o período de faturamento. Se o seu aplicativo usa mais de 10.000 chamadas,
é necessário um contrato com a IBM para a provisão contínua de serviços.

Quando o seu aplicativo atinge o limite de chamadas API por minuto que ele tem permissão para
fazer com base no plano que você selecionou, a próxima chamada API que for feita
não será bem-sucedida até que o seu aplicativo tenha permissão para solicitar mais chamadas API.

Por exemplo, se você estiver usando o plano Padrão, o seu aplicativo *poderá* fazer 500 chamadas API
em um minuto, mesmo se ele exceder o limite do plano (150 chamadas por minuto),
mas a próxima chamada API não será permitida até 5 minutos depois. Portanto, um usuário poderá observar um atraso na atualização de dados de clima em seu app.
Deve-se garantir que você desenvolva o seu app para manipular esses limites e não solicitar bursts de chamadas
API. Em vez disso, é possível
monitorar o uso de chamadas API de seu app.
É possível verificar se o seu app atinge
o limite de seu plano verificando o número de itens retornados pela chamada API.

Quando o seu aplicativo atinge o limite de chamadas API por mês que ele tem permissão para fazer
com base no plano que você selecionou, as próximas chamadas API serão cobradas a uma taxa
média de US$1,70 por 10.000 chamadas API.

## Feedback e suporte
{: #feedback_support}

É possível obter ajuda procurando informações ou fazendo uma pergunta em um fórum. Também é possível abrir um chamado de suporte.

Ao usar os fóruns para fazer uma pergunta, identifique-a para que ela possa ser vista pelas equipes de desenvolvimento do {{site.data.keyword.Bluemix_notm}}.

* Se você tiver questões técnicas sobre o desenvolvimento ou a implementação de um app com o {{site.data.keyword.weather_short}}, poste sua pergunta no [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window} e identifique-a com **ibm-bluemix** e **weather**.
* Se você tiver problemas com esse serviço ou com as instruções de introdução, use o [fórum do IBM developerWorks Answers](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}. Inclua as tags **bluemix** e **weather**.
* Se você tiver dúvidas sobre a migração de seu aplicativo do Insights for Weather para o {{site.data.keyword.weather_short}},
entre em contato conosco em [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

Consulte [Obtendo ajuda](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window} para obter mais detalhes sobre como usar os fóruns.

Consulte [Entrando em contato com o suporte](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window} para obter informações sobre como abrir um chamado de suporte IBM ou sobre os níveis de suporte e as severidades dos chamados.
