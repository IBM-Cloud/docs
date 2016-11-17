---

copyright:
  years: 2016
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Agregação da API
{: #api_aggregation}

Algumas APIs do {{site.data.keyword.weather_short}} podem ser agregadas. É possível usar a
agregação para combinar duas ou mais chamadas API atômicas em uma
única solicitação de HTTP.
{: shortdesc}

Uma chamada API atômica faz referência a qualquer uma das APIs
que definem um alias para agregação. Cada documento do usuário da
API contém o alias para o nome da agregação na seção de formato de
URL se ela estiver disponível para agregação. Por exemplo, as APIs
de previsão diária padrão possuem um alias para agregação de
`v2fcstdaily10` que pode ser usado para recuperar a previsão
diária de 10 dias como parte de uma solicitação agregada.

A agregação possui as limitações a seguir:

* O tamanho total da resposta descompactada para a agregação
completa deve ser menos do que 1 megabyte.
* As URLs devem ser menores que aproximadamente 4,096 caracteres de
comprimento (incluindo protocolo, nome do host, caminho e
sequência de consultas).
* É possível agregar até 10 APIs atômicas.

**Nota:** Se sua solicitação ou resposta violar qualquer uma destas limitações, você receberá uma
resposta de erro com um código de Status HTTP 500 (normalmente 500 ou 502, embora outros possam ser
retornados).

## URLs da API agregada
A URL da API agregada inicia com `/v2/aggregate/` e é seguida por aliases que
são separados por pontos e vírgulas.
Por exemplo, para agregar a API de previsão diária de 10 dias (`v2fcstdaily10`) a
observações atuais (`v2obscurrent`), use o formato a seguir:

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Regras de parâmetro de consulta para APIs atômicas e
agregação
Parâmetros de consulta são necessários para todas as solicitações. Os parâmetros de consulta para agregação são passados da mesma
forma que para as chamadas API atômicas, com algumas regras
extras. As seções a seguir descrevem como
eles podem ser aplicados para formar diferentes agregações.

### Especificar os parâmetros de consulta que são aplicados a
todas as APIs atômicas

A forma mais simples de agregação é quando
os parâmetros de consulta são aplicados a todas as APIs atômicas. Neste caso, os parâmetros de consulta possuem o formato
padrão de `?param1=value1&amp;param2=value2`.

O exemplo a seguir aplica
`geocode=31.44,84.33&amp;language=en&amp;units=e` à solicitação para as APIs atômicas
`v2fcstdaily10` e `v2obscurrent`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Especificar quais APIs atômicas recebem quais parâmetros de
consulta

Se for necessário especificar parâmetros
para APIs atômicas específicas, os parâmetros de consulta poderão usar a notação posicional de
`?R1.param1=value1&amp;R2.param2=value2`. Esse formato usa `param1`
para a primeira API atômica e `param2` para a segunda API atômica.

O exemplo
a seguir aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` a
`v2fcstdaily10` e `geocode=44.44,50.23&amp;language=en&amp;units=e`
a `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Agrupar parâmetros de consulta para APIs atômicas específicas

É possível agrupar parâmetros usando a notação
posicional como um formato separado por vírgula de `?R1,R2.param1=value1&amp;param2=value2`.
Esse formato usa `param1` para a primeira e a segunda APIs atômicas e
`param2` para todas as APIs atômicas.

O exemplo a seguir aplica `geocode=34.06,84.21&amp;language=enUS&amp;units=e` a `v2fcstdaily10` e
`v2obscurrent`. Ele aplica `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` a
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Solicitar o mesmo recurso de várias maneiras

É possível
solicitar o mesmo recurso de várias maneiras, como em diferentes
idiomas ou com uma unidade de medida diferente. Com esse formato, a API atômica pode ser
repetida na solicitação: `/v2/aggregate/v2fcstdaily10;v2fcstdaily10` e a
notação posicional do parâmetro pode ser usada para indicar de que maneira solicitar qual API:
`?R1.param1=value1&amp;R2.param1=value2`. Neste
caso, o usuário recebe o mesmo recurso que é formatado ou
convertido em diferentes maneiras.

O exemplo a seguir aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` à primeira
`v2fcstdaily10` e `geocode=31.44,84.33&amp;language=fr&amp;units=m`
à segunda `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

O exemplo a seguir aplica `geocode=31.44,84.33&amp;language=en&amp;units=e` à
primeira `v2fcstdaily10` e
`geocode=33.54,85.43&amp;language=en&amp;units=e` à segunda
`v2fcstdaily10` para recuperar vários locais para os mesmos
dados:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




