---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Ações da web
{: #openwhisk_webactions}

As ações da web são ações do OpenWhisk anotadas para permitir que você construa rapidamente aplicativos baseados na web. Isso permite programar a lógica de backend que seu aplicativo da web pode acessar anonimamente sem requerer uma chave de autenticação do OpenWhisk. Cabe ao desenvolvedor de ação implementar sua própria autenticação e autorização desejada (ou seja, fluxo OAuth).
{: shortdesc}

As ativações de ação da web serão associadas ao usuário que criou a ação. Essa ação adia a custo de uma ativação de ação do responsável pela chamada ao proprietário da ação.

Vamos tomar a ação JavaScript `hello.js` a seguir,
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

Você pode criar uma *ação da web* `hello` no pacote `demo` para o namespace `guest` usando a anotação `web-export`:
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

A anotação `web-export` permite que a ação seja acessível como uma ação da web por meio de uma nova interface REST. A URL que é estruturada como a seguir: `https://openwhisk.ng.bluemix.net/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`. O nome completo de uma ação consiste em três partes: o namespace, o nome do pacote e o nome da ação.

*O nome completo da ação deverá incluir seu nome do pacote, que será `default` se a ação não estiver em um pacote nomeado.*

Um exemplo é `guest/demo/hello`. A última parte do URI chamado `extension` que é geralmente `.http`, embora outros valores sejam permitidos conforme descrito posteriormente. O caminho da API de ação da web pode ser usado com `curl` ou `wget` sem uma chave API. Ele pode até ser inserido diretamente em seu navegador.

Tente abrir [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane) em seu navegador da web. Ou tente chamar a ação por meio de `curl`:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

Aqui está um exemplo de uma ação da web que executa o redirecionamento de HTTP:
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}  

Ou configura um cookie:
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>olá</h3></body></html>' }
}
```
{: codeblock}

Ou retorna um `image/png`:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

It is important to be aware of the [response size limit](./openwhisk_reference.html) para ações, pois uma resposta que excede os limites do sistema predefinidos falhará. Objetos grandes não devem ser enviados sequencialmente por meio do OpenWhisk, mas, em vez disso, adiados para um armazenamento de objeto, por exemplo.

## Manipulando solicitações de HTTP com ações
{: #openwhisk_webactions_http}

Uma ação do OpenWhisk que não é uma ação da web requer a autenticação e deve responder com um objeto JSON. Por outro lado, as ações da web podem ser chamadas sem autenticação e podem ser usadas para implementar manipuladores de HTTP que respondem com conteúdo de *cabeçalhos*, *statusCode* e *corpo* de diferentes tipos. A ação da web deve ainda retornar um objeto JSON, mas o sistema OpenWhisk (ou seja, o `controlador`) tratará uma ação da web de forma diferente se seu resultado incluir uma ou mais das seguintes como propriedades JSON de nível superior:

- `headers`: um objeto JSON no qual as chaves são nomes de cabeçalho e os valores são valores de sequência para esses cabeçalhos (o padrão é sem cabeçalhos).
- `statusCode`: um código de status de HTTP válido (o padrão é 200 OK).
- `body`: uma sequência que é um texto simples ou uma sequência codificada em base64 (para dados binários).

O controlador passará adiante os cabeçalhos especificados pela ação, se houver, para o cliente HTTP quando finalizar a solicitação/resposta. Da mesma forma, o controlador responderá com o código de status especificado quando presente. Por último, o corpo é passado adiante como o corpo da resposta. A menos que um `content-type header` seja declarado no `headers` do resultado da ação, o corpo será passado adiante no estado em que se encontra se for uma sequência (caso contrário, resultará em um erro). Quando o `content-type` for definido, o controlador determinará se a resposta é dados binários ou texto simples e decodificará a sequência usando um decodificador base64 conforme necessário. Se o corpo não for decodificado corretamente, um erro será retornado para o responsável pela chamada.

*Nota*: um objeto ou matriz JSON é tratado como dados binários e deve ser codificado em base64 como mostrado no exemplo acima.

## Contexto de HTTP

Todas as ações da web, quando chamadas, recebem detalhes de solicitação de HTTP adicionais como parâmetros para o argumento de entrada da ação. São elas:

- `__ow_method` (tipo: sequência). O método de HTTP da solicitação.
- `__ow_headers` (topo: mapear sequência para sequência): os cabeçalhos da solicitação.
- `__ow_path` (tipo: sequência): o caminho não correspondido da solicitação (a correspondência para depois de consumir a extensão de ação).
- `__ow_user` (tipo: sequência): o namespace que identifica o assunto autenticado do OpenWhisk
- `__ow_body` (tipo: sequência): a entidade de corpo da solicitação, como uma sequência codificada com base64 quando o conteúdo é binário ou sequência simples, caso contrário
- `__ow_query` (tipo: sequência): os parâmetros de consulta da solicitação como uma sequência não analisada

Uma solicitação não pode substituir nenhum dos parâmetros `__ow_` nomeados acima; fazer isso resultará em uma solicitação com falha com status igual a 400 Solicitação inválida.

O `__ow_user` estará presente apenas quando a ação da web for [anotada para requerer autenticação](./openwhisk_annotations.html#openwhisk_annotations_webactions) e permitirá que uma ação da web implemente sua própria política de autorização. O `__ow_query` estará disponível apenas quando uma ação da web optar por manipular a [solicitação de HTTP "bruto"](#raw-http-handling). É uma sequência contendo os parâmetros de consulta analisados do URI (separados por `&`). A propriedade `__ow_body` estará presente ao manipular solicitações de HTTP "bruto" ou quando a entidade de solicitação de HTTP não for um objeto JSON ou dados de formulário. De qualquer outra forma, as ações da web recebem parâmetros de consulta e corpo como propriedades de primeira classe nos argumentos de ação com parâmetros de corpo tendo precedência sobre parâmetros de consulta que, por sua vez, têm precedência sobre os parâmetros de ação e de pacote.

## Recursos adicionais

As ações da web trazem alguns recursos adicionais que incluem:

- `Extensões de conteúdo`: a solicitação deve especificar seu tipo de conteúdo desejado como um de `.json`, `.html`, `.http`, `.svg` ou `.text`. Isso é feito incluindo uma extensão no nome da ação no URI, para que uma ação `/guest/demo/hello` seja referenciada como `/guest/demo/hello.http`, por exemplo, para receber uma resposta de HTTP de volta. Por conveniência, a extensão `.http` é assumida quando nenhuma extensão é detectada.
- `Projetando campos do resultado`: o caminho que segue o nome da ação é usado para projetar um ou mais níveis da resposta. Por exemplo, 
`/guest/demo/hello.html/body`. Isso permite a uma ação que retorna um dicionário `{body: "..." }` projetar a propriedade `body` e retornar diretamente seu valor de sequência. O caminho projetado segue um modelo de caminho absoluto (como em XPath).
- `Parâmetros de consulta e corpo como entrada`: a ação recebe parâmetros de consulta, bem como parâmetros no corpo da solicitação. A ordem de precedência para mesclar parâmetros é: parâmetros de pacote, parâmetros de ação, parâmetro de consulta, parâmetros de corpo com cada um desses substituindo quaisquer valores anteriores no caso de sobreposição. Como um exemplo, `/guest/demo/hello.http?name=Jane` passará o argumento `{name: "Jane"}` para a ação.
- `Dados de formulário`: além do `application/json` padrão, as ações da web podem receber URL codificada de dados `application/x-www-form-urlencoded data` como entrada.
- `Ativação por meio de múltiplos verbos de HTTP`: uma ação da web pode ser chamada por meio de qualquer um destes métodos de HTTP: `GET`, `POST`, `PUT`, `PATCH` e `DELETE`, bem como `HEAD` e `OPTIONS`.
- `Corpo não JSON e manipulação de entidade HTTP bruto`: uma ação da web pode aceitar um corpo de solicitação de HTTP diferente de um objeto JSON e pode optar por sempre receber esses valores como valores opacos (texto simples, quando não binário ou sequência codificada com base64, caso contrário).

O exemplo abaixo esboça rapidamente como você pode usar esses recursos em uma ação da web. Considere uma ação `/guest/demo/hello` com o corpo a seguir:
```javascript
function main(params) { 
    return { response: params };
}
```

Quando essa ação é chamada como uma ação da web, é possível alterar a resposta da ação da web projetando caminhos diferentes do resultado.
Por exemplo, para retornar o objeto inteiro e ver quais argumentos a ação recebe:

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
     {
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

e com um parâmetro de consulta:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
     {
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

ou dados de formulário:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
     {
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

ou objeto JSON:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
     {
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

e para projetar apenas o nome (como texto):
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Janete
```

Você vê acima que, por conveniência, parâmetros de consulta, dados do formulário e entidades do corpo de objeto JSON são todos tratados como dicionários, pois seus valores são diretamente acessíveis como propriedades de entrada de ação. Este não é o caso para ações da web que optam, como alternativa, por manipular entidades de solicitação de HTTP mais diretamente ou quando a ação da web recebe uma entidade que não é um objeto JSON.

Aqui está um exemplo de uso de um tipo de conteúdo "texto" com o mesmo exemplo mostrado acima:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
     {
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## Extensões de Conteúdo
{: #openwhisk_webactions_extensions}

Uma extensão de conteúdo geralmente é necessária ao chamar uma ação da web; a ausência de uma extensão assume `.http` como o padrão. As extensões `.json` e `.http` não requerem um caminho de projeção. As extensões `.html`, `.svg` e `.text` requerem, no entanto, por conveniência; o caminho padrão é assumido para corresponder ao nome da extensão. Portanto, para chamar uma ação da web e receber uma resposta `.html`, a ação deve responder com um objeto JSON que contenha uma propriedade de nível superior chamada `html` (ou a resposta deve estar no caminho explicitamente especificado). Ou seja, `/guest/demo/hello.html` é equivalente a projetar a propriedade `html` explicitamente, como em `/guest/demo/hello.html/html`. O nome completo da ação deverá incluir seu nome do pacote, que é `default` se a ação não estiver em um pacote nomeado.


## Parâmetros protegidos
{: #openwhisk_webactions_protected}

Os parâmetros de ação também podem ser protegidos e tratados como imutáveis. Para finalizar os parâmetros e tornar uma ação da web acessível, duas [anotações](openwhisk_annotations.html) devem ser anexadas à ação: `final` e `web-export`, ambas devem ser configuradas como `true` para que tenham efeito. Revisitando a implementação da ação anterior, incluímos as anotações conforme a seguir:

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

O resultado dessas mudanças é que o `name` está ligado a `Jane` e não pode ser substituído por parâmetros de consulta ou corpo devido à anotação final. Isso assegura a ação com relação aos parâmetros de consulta ou corpo que tentam mudar esse valor, seja por acidente ou intencionalmente. 

## Desativando ações da web
{: #openwhisk_webactions_disable}

Para desativar a chamada de uma ação de web por meio da nova API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/web/`), é suficiente remover a anotação ou configurá-la como `false`.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```

## Manipulação de HTTP bruto
{: #raw-http-handling}

Uma ação da web pode optar por interpretar e processar um corpo HTTP recebido diretamente, sem a promoção de um objeto JSON para as propriedades de primeira classe disponíveis para a entrada de ação (por exemplo, `args.name` versus a análise de `args.__ow_query`). Isso é feito por meio de [anotações](openwhisk_annotations.html) `raw-http`. Usando o mesmo exemplo anterior, mas agora como uma ação da web de HTTP "bruto" recebendo `name` como um parâmetro de consulta e como um valor JSON no corpo da solicitação de HTTP:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
     {
  "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

Observe neste caso que o conteúdo JSON é codificado com base64 porque é tratado como um valor binário. A ação deve decodificar com base64 e analisar por JSON esse valor para recuperar o objeto JSON. O OpenWhisk usa a estrutura [Spray](https://github.com/spray/spray) para [determinar](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282) quais tipos de conteúdo são binários e quais são texto simples.


### Ativando a manipulação de HTTP bruto

As ações da web de HTTP bruto são ativadas por meio de [anotações](openwhisk_annotations.html) `raw-http` com um valor de `true`.

```
wsk action create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http true
```
{: pre}

**Nota:** uma vez que `raw-http` implica em `web-export`, planejamos melhorar a CLI para fornecer uma maneira mais conveniente de incluir (e remover) essas anotações no futuro.


### Desativando a manipulação de HTTP bruto

A desativação de HTTP bruto é realizada configurando o valor de [anotações](openwhisk_annotations.html) `raw-http` como `false`.

```
wsk update create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http false
```
{: pre}

**Nota:** todas as anotações para uma única ação devem ser configuradas ao mesmo tempo, ao criar ou atualizar a ação. Isso se deve a uma limitação atual na API e na CLI. Se houver falha ao fazer isso, o resultado será a remoção de quaisquer anotações anexadas anteriormente.


## Identificação de Erros
{: #openwhisk_webactions_errors}

Quando uma ação do OpenWhisk falha, há dois modos de falha diferentes. O primeiro é conhecido como um *erro de aplicativo* e é análogo a uma exceção de captura: a ação retorna um objeto JSON contendo uma propriedade `error` de nível superior. O segundo é um *erro de desenvolvedor* que ocorre quando a ação falha catastroficamente e não produz uma resposta (isso é semelhante a uma exceção de não captura). Para ações da web, o controlador manipula erros de aplicativo conforme a seguir:

- Qualquer projeção de caminho especificada é ignorada e o controlador projeta a propriedade `error` em seu lugar.
- O controlador aplica a manipulação de conteúdo subentendida pela extensão de ação ao valor da propriedade `error`.

Os desenvolvedores devem estar cientes de como as ações da web podem ser usadas para gerar respostas de erros adequadamente. Por exemplo, uma ação da web que é usada com a extensão `.http`
deve retornar uma resposta de HTTP, por exemplo: `{error: { statusCode: 400 }`. A falha em fazer isso resultará em uma incompatibilidade entre o tipo de conteúdo implícito da extensão e o tipo de conteúdo da ação na resposta de erro. Consideração especial deve ser dada a ações da web que são sequências, para que os componentes que compõem uma sequência possam gerar erros adequados quando necessário.

