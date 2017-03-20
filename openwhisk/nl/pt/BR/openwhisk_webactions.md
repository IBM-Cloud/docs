---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Ações da web (experimental)
{: #openwhisk_webactions}

As ações da web são ações do OpenWhisk anotadas para permitir que você construa rapidamente aplicativos baseados na web. Isso permite programar a lógica de backend que seu aplicativo da web pode acessar anonimamente sem requerer uma chave de autenticação do OpenWhisk. Cabe ao desenvolvedor de ação implementar sua própria autenticação e autorização desejada (ou seja, fluxo OAuth).
{: shortdesc}

As ativações de ação da web serão associadas ao usuário que criou a ação. Essa ação adia a custo de uma ativação de ação do responsável pela chamada ao proprietário da ação. 

**Nota**: esse recurso é atualmente uma oferta experimental que permite aos usuários uma oportunidade antecipada para experimentar e fornecer feedback.

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

A anotação `web-export` permite que a ação seja acessível como uma ação da web por meio de uma nova interface REST. A URL que é estruturada como a seguir: `https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}`. O nome completo de uma ação consiste em três partes: o namespace, o nome do pacote e o nome da ação. Um exemplo é `guest/demo/hello`. A última parte do URI chamado `extension` que é geralmente `.http`, embora outros valores sejam permitidos conforme descrito posteriormente. O caminho da API de ação da web pode ser usado com `curl` ou `wget` sem uma chave API. Ele pode até ser inserido diretamente em seu navegador.

Tente abrir [https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane) em seu navegador. Ou tente chamar a ação por meio de `curl`:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
Aqui está um exemplo de uma ação da web que executa o redirecionamento de HTTP:
```javascript
function main() {
  return { 
    headers: { "location": "http://openwhisk.org" }, 
    code: 302 
  }
}
```
{: codeblock}

Ou configura um cookie:
```javascript
function main() {
  return { 
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>olá</h3></body></html" }
}
```
{: codeblock}

Ou retorna um `image/png`:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

It is important to be aware of the [response size limit](./openwhisk_reference.html) para ações, pois uma resposta que excede os limites do sistema predefinidos falhará. Objetos grandes não devem ser enviados sequencialmente por meio do OpenWhisk, mas, em vez disso, adiados para um armazenamento de objeto, por exemplo.

## Manipulando solicitações de HTTP com ações
{: #openwhisk_webactions_http}

Uma ação do OpenWhisk que não é uma ação da web requer a autenticação e deve responder com um objeto JSON. Em contraste, as ações da web podem ser chamadas sem autenticação e podem ser usadas para implementar manipuladores de HTTP que respondem com conteúdo *headers*, *status code* e *body* de diferentes tipos. A ação da web deve ainda retornar um objeto JSON, mas o sistema OpenWhisk (ou seja, o `controlador`) tratará uma ação da web de forma diferente se seu resultado incluir uma ou mais das seguintes como propriedades JSON de nível superior:

- `headers`: um objeto JSON no qual as chaves são nomes de cabeçalho e os valores são valores de sequência para esses cabeçalhos (o padrão é sem cabeçalhos).
- `code`: um código de status de HTTP válido (o padrão é 200 OK).
- `body`: uma sequência que é um texto simples ou uma sequência codificada em base64 (para dados binários).

O controlador passará adiante os cabeçalhos especificados pela ação, se houver, para o cliente HTTP quando finalizar a solicitação/resposta. Da mesma forma, o controlador responderá com o código de status especificado quando presente. Por último, o corpo é passado adiante como o corpo da resposta. A menos que um `content-type header` seja declarado no `headers` do resultado da ação, o corpo será passado adiante no estado em que se encontra se for uma sequência (caso contrário, resultará em um erro). Quando o `content-type` for definido, o controlador determinará se a resposta é dados binários ou texto simples e decodificará a sequência usando um decodificador base64 conforme necessário. Se o corpo não for decodificado corretamente, um erro será retornado para o responsável pela chamada.

*Nota*: um objeto ou matriz JSON é tratado como dados binários e deve ser codificado em base64 como mostrado no exemplo acima.

## Contexto de HTTP

Uma ação da web, quando chamada, recebe todas as informações de solicitação de HTTP disponíveis como parâmetros adicionais para o argumento de entrada da ação. São elas:

- `__ow_meta_verb`: o método de HTTP da solicitação.
- `__ow_meta_headers`: os cabeçalhos da solicitação.
- `__ow_meta_path`: o caminho não correspondido da solicitação (a correspondência para depois de consumir a extensão de ação).

A solicitação não pode substituir nenhum dos parâmetros `__ow_` nomeados acima; fazer isso resultará em uma solicitação com falha com status igual a 400 Solicitação inválida.

## Recursos adicionais
{: #openwhisk_webactions_extra}

As ações da web trazem alguns recursos adicionais que incluem:

- `Extensões de conteúdo`: a solicitação deve especificar seu tipo de conteúdo desejado como `.json`, `.html`, `.text` ou `.http`. Isso é feito incluindo uma extensão no nome da ação no URI, para que uma ação `/guest/demo/hello` seja referenciada como `/guest/demo/hello.http`, por exemplo, para receber uma resposta de HTTP de volta.
- `Projetando campos do resultado`: o caminho que segue o nome da ação é usado para projetar um ou mais níveis da resposta. Por exemplo, 
`/guest/demo/hello.html/body`. Isso permite a uma ação que retorna um dicionário `{body: "..." }` projetar a propriedade `body` e retornar diretamente seu valor de sequência. O caminho projetado segue um modelo de caminho absoluto (como em XPath).
- `Parâmetros de consulta e corpo como entrada`: a ação recebe parâmetros de consulta, bem como parâmetros no corpo da solicitação. A ordem de precedência para mesclar parâmetros é: parâmetros de pacote, parâmetros de ação, parâmetro de consulta, parâmetros de corpo com cada um desses substituindo quaisquer valores anteriores no caso de sobreposição. Como um exemplo, `/guest/demo/hello.http?name=Jane` passará o argumento `{name: "Jane"}` para a ação.
- `Dados de formulário`: além do `application/json` padrão, as ações da web podem receber URL codificada de dados `application/x-www-form-urlencoded data` como entrada.
- `Ativação por meio de múltiplos verbos de HTTP`: uma ação da web pode ser chamada por meio de um dos quatro métodos de HTTP: `GET`, `POST`, `PUT` ou `DELETE`.


O exemplo abaixo esboça rapidamente como você pode usar esses recursos em uma ação da web. Dada uma ação `/guest/demo/hello` com o corpo a seguir:
```javascript
function main(params) { 
    return { 'response': params};
}
```
{: codeblock}

e chamando a ação com um parâmetro de consulta `name`, usando a extensão `.json` para indicar uma resposta de JSON e projetando o campo `/response`, isso produzirá a resposta de HTTP a seguir:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
     {
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## Extensões de Conteúdo
{: #openwhisk_webactions_extensions}

Uma extensão de conteúdo é necessária ao chamar uma ação da web. As extensões `.json` e `.http` não requerem um caminho de projeção. No entanto, as extensões `.text` e `.html` o requerem por conveniência, o caminho padrão é assumido para corresponder ao nome da extensão. Portanto, para chamar uma ação da web e receber uma resposta `.html`, a ação deve responder com um objeto JSON que contenha uma propriedade de nível superior chamada `html` (ou a resposta deve estar no caminho explicitamente especificado). Ou seja, `/guest/demo/hello.html` é equivalente a projetar a propriedade `html` explicitamente, como em `/guest/demo/hello.html/html`. O nome completo da ação deverá incluir seu nome do pacote, que é `default` se a ação não estiver em um pacote nomeado.


## Parâmetros protegidos
{: #openwhisk_webactions_protected}

Os parâmetros de ação também podem ser protegidos e tratados como imutáveis. Para finalizar os parâmetros e tornar uma ação da web acessível, duas [anotações](/openwhisk_annotations.html) devem ser anexadas à ação: `final` e `web-export`, ambas devem ser configuradas como `true` para que tenham efeito. Revisitando a implementação da ação anterior, incluímos as anotações conforme a seguir:

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

Para desativar a chamada de uma ação de web por meio da nova API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`), é suficiente remover a anotação ou configurá-la como `false`.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## Identificação de Erros
{: #openwhisk_webactions_errors}

Quando uma ação do OpenWhisk falha, há dois modos de falha diferentes. O primeiro é conhecido como um *erro de aplicativo* e é análogo a uma exceção de captura: a ação retorna um objeto JSON contendo uma propriedade `error` de nível superior. O segundo é um *erro de desenvolvedor* que ocorre quando a ação falha catastroficamente e não produz uma resposta (isso é semelhante a uma exceção de não captura). Para ações da web, o controlador manipula erros de aplicativo conforme a seguir:

- Qualquer projeção de caminho especificada é ignorada e o controlador projeta a propriedade `error` em seu lugar.
- O controlador aplica a manipulação de conteúdo subentendida pela extensão de ação ao valor da propriedade `error`.

Os desenvolvedores devem estar cientes de como as ações da web podem ser usadas para gerar respostas de erros adequadamente. Por exemplo, uma ação da web que é usada com a extensão `.http`
deve retornar uma resposta de HTTP, por exemplo: `{error: { code: 400 }`. A falha em fazer isso resultará em uma incompatibilidade entre o tipo de conteúdo implícito da extensão e o tipo de conteúdo da ação na resposta de erro. Consideração especial deve ser dada a ações da web que são sequências, para que os componentes que compõem uma sequência possam gerar erros adequados quando necessário.
