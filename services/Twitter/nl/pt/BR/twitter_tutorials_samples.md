---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Exemplos de Insights for Twitter
{: #examples}

Para introduzir o serviço {{site.data.keyword.twittershort}}, use as amostras fornecidas para entender como aproveitar o
serviço.
{: shortdesc}

## Demo de Insights for Twitter
{: #insights_twitter_demo}

Um aplicativo de amostra está disponível para procurar fluxos de dados do Twitter que usam o serviço {{site.data.keyword.twittershort}}. O aplicativo é acessível navegando para [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window}. O aplicativo é aberto em seu navegador e exibe um campo de procura, com os botões **Procura do Twitter** e **Contagem do Twitter**. 

![Imagem da interface com o usuário com o campo de procura.](images/sample1_UI.jpg "Imagem da interface com o usuário com o campo de procura.")

A partir do aplicativo de amostra, é possível procurar tweets usando os parâmetros e os operadores suportados descritos em [Linguagem de consulta](twitter_rest_apis.html#querylanguage){: new.window}. Por exemplo, inserir "IBM Twitter" (com um espaço para denotar uma operação booleana AND) e clicar em **Procura do Twitter** retorna tweets contendo ambos os termos.

![Imagem do termo de consulta e dos resultados de procura.](images/sample1_tweet_search.jpg "Imagem do termo de consulta e dos resultados de procura retornados.")

Com "IBM Twitter" especificado no campo de procura, clicar em **Contagem do Twitter** retorna o número de tweets que contêm ambos os termos.

![Imagem do termo de consulta e dos resultados de contagem.](images/sample1_tweet_count.jpg "Imagem do termo de consulta e dos resultados de contagem retornados.")

## Criando uma faixa de regra
{: #creating_rule_track}

Como um usuário do Plano de Entrada, é possível criar faixas baseadas em regras para filtrar tweets coletados no
fluxo de dados do PowerTrack. Os exemplos em seções posteriores demonstram como editar e excluir faixas, bem como executar uma chamada API de procura ou de contagem no fluxo do PowerTrack. Para criar uma faixa de regra, emita uma solicitação **POST** com a operação /api/v1/tracks, especifique o tipo de faixa (**Regra**), indique uma 'EndDate' e inclua pelo menos uma regra. O fragmento a seguir é uma solicitação de exemplo que inclui duas regras:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"}
    ]
}
```

O `nome do usuário` e
`senha` são exclusivos para seu aplicativo
e instância de serviço. Estas informações podem ser obtidas a partir das variáveis de ambiente
**VCAP_SERVICES**. Para obter mais informações, consulte
[Introdução ao {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

O corpo da resposta aparece semelhante ao fragmento a seguir:

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
    "id": "66ff1961-51fe-4475-8bcd-c02f071d6fd1",
    "type": "Rule",
    "state": "Active",
    "createdDate": "2015-08-06T20:38:28.940Z",
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "rules": [
        {
          "id": "06497963-4fe3-47e8-90cd-aaef25f31314"
          "value": "Canada"
        },
        {
          "id": "d021165d-85e2-456a-af16-b9c026d76208",
          "value": "sport hockey"
        }
    ]
}
```

A resposta inclui o ID exclusivo que está associado à faixa recém-criada. Além disso,
a cada regra é designado um ID exclusivo. A endDate indica quando a faixa para de coletar mensagens e deve estar em conformidade com o formato UTC (`YYYY-MM-DD` ou `YYYY-MM-DDTHH:MM:SSZ`). A propriedade de tipo deve ser especificada como **Regra** ou **Agregada**. Visto que este exemplo demonstra a
criação de uma faixa baseada em regras, o tipo **Regra** foi especificado.

Se a propriedade de estado não for especificada na solicitação, a faixa será criada e ficará **Ativa**, por padrão. A propriedade de nome é opcional e não é necessário que seja exclusiva. Para melhor gerenciar os filtros, recomenda-se selecionar um nome exclusivo e
descritivo.

Para obter informações mais detalhadas sobre a sintaxe de regras, consulte a [Linguagem de consulta](twitter_rest_apis.html#querylanguage){: new.window} do {{site.data.keyword.twittershort}}.

## Criando uma faixa agregada
{: #creating_aggregated_track}

Como um usuário do Plano de Entrada, é possível criar faixas agregadas que combinam duas ou mais faixas existentes. As faixas agregadas podem incluir faixas baseadas em regras e outras faixas agregadas. Procurar tweets de uma faixa agregada retorna resultados de suas faixas constituintes. Para criar uma faixa agregada, emita uma solicitação **POST** com a operação /api/v1/tracks, especifique o tipo de faixa (**Agregado**) e inclua dois ou mais trackIds. O fragmento a seguir é uma solicitação de exemplo que inclui duas faixas:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "name": "My Aggregated Track",
    "type": "Aggregated",
    "trackIds": [
       {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
       {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"}
     ]
}
```
O `nome do usuário` e
`senha` são exclusivos para seu aplicativo
e instância de serviço. Estas informações podem ser obtidas a partir das variáveis de ambiente
**VCAP_SERVICES**. Para obter mais informações, consulte
[Introdução ao {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

O corpo da resposta aparece semelhante ao fragmento a seguir:

```
HTTP/1.1 201 Created 
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
  "id": "9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6",
  "type": "Aggregated",
  "createdDate": "2015-08-07T17:05:51.214Z",
  "name": "My Aggregated Track",
  "trackIds": [
    {
      "id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"
    },
    {
      "id": "180356df-9a78-491e-b070-f3ffbe00bdf2"
    }
  ]
}
```

A resposta inclui o ID exclusivo que está associado à faixa agregada. Ao contrário das faixas baseadas em regras, as faixas agregadas não incluem propriedades endDate ou de estado, visto que essas propriedades são gerenciadas nas faixas baseadas em regras individuais.

## Editando faixas
{: #editing_tracks}

As faixas de regra e agregadas podem ser editadas para refinar como os dados são filtrados no fluxo do PowerTrack. Quando as regras são incluídas (ou modificadas) em faixas existentes, as mensagens que foram recuperadas com base em regras anteriores persistem na faixa. Para assegurar-se de que os resultados da procura retornem dados para o conjunto de regras mais recente, exclua a faixa e crie uma faixa nova com o conjunto de regras desejado.

O exemplo em [Criando uma faixa de regra](#creating_rule_track){: new.window} incluiu duas regras com um ID de faixa de `66ff1961-51fe-4475-8bcd-c02f071d6fd1`. Para incluir uma nova regra com um valor "Champions", use a operação POST /api/v1/tracks/{track Id} e anexe a nova regra.

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"},
        {"value": "Champions"}
    ]
}
```
De forma semelhante, é possível remover regras de uma faixa existente emitindo uma operação GET /api/v1/tracks/{track Id} e remover regras indesejadas.

O exemplo em [Criando uma faixa agregada](#creating_aggregated_track) incluiu duas faixas. Outra faixa, com ID `c4562594-1eeb-4a95-8fac-255428d74bce`, poderia ser incluída na faixa agregada existente emitindo a operação a seguir:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6
HTTP/1.1 Content-Type: application/json
{
  "trackIds": [
    {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
    {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"},
    {"id": "c4562594-1eeb-4a95-8fac-255428d74bce"}
  ]
}
```

## Excluindo faixas
{: #deleting_tracks}

É possível excluir faixas que não são mais necessárias emitindo uma operação DELETE /api/v1/tracks/{trackId}. Essa ação pode ser aplicada a faixas baseadas em regras e
agregadas. As faixas incluídas em uma faixa agregada não podem ser excluídas até que a faixa
seja removida de todas as faixas agregadas. O exemplo a seguir demonstra como excluir uma faixa com o ID `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88`:

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

Como alternativa, é possível parar a coleção de tweets de uma faixa específica mudando seu estado para Inativo. Em vez de excluir a faixa, o exemplo a seguir desativa a faixa:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## Procurando tweets
{: #searching_tweets}

É possível emitir uma operação GET em seu aplicativo para recuperar tweets de um dos fluxos de dados. Por exemplo, a procura de tweets do Decahose é implementada como: `/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`. Para usuários do Plano de entrada, a procura de tweets do fluxo do PowerTrack é implementada como: `/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`.

O parâmetro "size" especifica o número de mensagens a serem retornadas em uma resposta de consulta, enquanto o parâmetro "from" indica a mensagem inicial a ser retornada no conjunto de resultados completo. A referência {trackId} é o identificador exclusivo de uma faixa específica.
Ao usar cURL, é possível procurar no fluxo do Decahose tweets que contêm "IBM", digitando:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

O envio
da mesma consulta com relação ao fluxo do PowerTrack seria inserido como: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

O `nome do usuário` e
`senha` são exclusivos para seu aplicativo
e instância de serviço. Estas informações podem ser obtidas a partir das variáveis de ambiente
**VCAP_SERVICES**. Para obter mais informações, consulte
[Introdução ao {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

O serviço retorna respostas em formato JSON. A seguinte tabela lista os possíveis códigos
de resposta.

| **Código de Status HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Propriedades de carga útil de solicitação inválidas ou ausentes.                   	|
| 401              	| Autenticação com falha. Nome de usuário e senha válidos são requeridos. 	|
| 403              	| Proibido, limite atingido.                                        	|
| 500              	| Ocorreu um erro interno.                                  	|

** Tabela 1. Mensagens de resposta

O corpo da resposta pode aparecer como:

```
{
    "search": {
        "results": 16283624
    },
    "tweets": [{
        "message": {
            ...
            "body": "this is a nice tweet",
            "actor": {
                "followersCount”: 456,
                "displayName": "IBM Tweeter"
                ...
            },
            "cde": {
                "sentiment": {"polarity": "POSITIVE"...
                },
                "author": {"gender": "male"...
                },
                ...
            }
        }
    }]
}
```

A expressão de consulta codificada por URL a seguir recupera tweets em um filme, com base em um prazo e um número de ocorrências especificados. Este exemplo poderia ser usado para determinar o nível de interesse ou reações a um trailer de filme.

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

Ao decodificar a URL, a sintaxe e a operação de consulta tornam-se "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5".

## Contando o número de Tweets
{: #counting_tweets}

É possível aplicar uma operação GET em seu aplicativo para
recuperar o número de tweets que correspondem a uma consulta
especificada. As consultas ao Decahose são emitidas como: `/api/v1/messages/count?q=QUERY`, enquanto as chamadas no fluxo do PowerTrack usam o formato a seguir: 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

Ao usar cURL, é possível localizar o número de tweets no Decahose, que contêm "IBM", usando:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

A mesma
consulta pode ser emitida com relação à origem de dados do PowerTrack como: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

O `nome do usuário` e
`senha` são exclusivos para seu aplicativo
e instância de serviço. Estas informações podem ser obtidas a partir das variáveis de ambiente
**VCAP_SERVICES**. Para obter mais informações, consulte
[Introdução ao {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

O serviço retorna respostas em formato JSON. A tabela a seguir
lista as possíveis mensagens de resposta.

| **Código de Status HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Propriedades de carga útil de solicitação inválidas ou ausentes.                   	|
| 401              	| Autenticação com falha. Nome de usuário e senha válidos são requeridos. 	|
| 403              	| Proibido, limite atingido.                                        	|
| 500              	| Ocorreu um erro interno.                                  	|

**Tabela 2. Mensagens de resposta**

O corpo da resposta pode aparecer como:
```
{
  "related": {
      "search": {
          "href": "https://server.bluemix.net/api/v1/messages/search?q=ibm" 
      }
  },
  "search": {
      "results": 21695
  }
}
```

A expressão de consulta a seguir recupera o número de tweets positivos que contêm ambos, "IBM" e "Bluemix". Nesse caso, os tweets do Decahose são retornados na
resposta.

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

A expressão de consulta codificada por URL a seguir recupera o número de tweets que contêm "IBM" em um período especificado. Esta consulta de amostra pode ajudar a medir a popularidade de um
assunto e determinar se está se tornando tendência. Os tweets do fluxo do PowerTrack são retornados
neste exemplo.

`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

Ao decodificar a URL, a sintaxe e a operação de consulta tornam-se "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)".
