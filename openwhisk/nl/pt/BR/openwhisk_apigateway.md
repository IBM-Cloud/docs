---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gateway de API
{: #openwhisk_apigateway}

As ações do OpenWhisk podem ter o benefício de serem gerenciadas pelo gerenciamento de API.

O API Gateway age como um proxy para [Ações da web](webactions.md) e fornece a elas recursos adicionais, incluindo roteamento de método de HTTP, ID/segredos do cliente, limitação de taxa, CORS, visualizar logs de uso e resposta da API e definir políticas de compartilhamento de API.
Para obter mais informações sobre o recurso API Gateway, é possível ler a [documentação de gerenciamento de API](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)

## Crie APIs de ações da web do OpenWhisk usando seu Navegador.

Com o API Gateway, é possível expor uma ação do OpenWhisk como uma API. Depois de definir a API, é possível aplicar as políticas de segurança e de limitação de taxa, visualizar os logs de uso e resposta da API e definir políticas de compartilhamento de API.
No Painel do OpenWhisk, clique na [Guia APIs](https://console.ng.bluemix.net/openwhisk/apimanagement).


## Criar APIs de ações da web do OpenWhisk usando a CLI

### Configuração da CLI do OpenWhisk

Configure a CLI do OpenWhisk com o apihost `wsk property set --apihost openwhisk.ng.bluemix.net`
Para poder usar o `wsk api`, o arquivo de configuração da CLI `~/.wskprops` precisa conter o Token de acesso do Bluemix.
Para obter o token de acesso, use o comando da CLI `wsk bluemix login`; para obter mais informações sobre o comando, execute `wsk bluemix login -h`

**Nota:** se os erros do comando requerem conexão única (sso), isso não é suportado atualmente. Como solução alternativa, efetue login com a CLI do CloudFoundry usando `cf login`, em seguida, copie o Token de Acesso do arquivo de configuração do diretório HOME `~/.cf/config.json` para o arquivo `~/.wskprops` como a propriedade `APIGW_ACCESS_TOKEN="value of AccessToken`. Remova o prefixo `Bearer` ao copiar a sequência de token de acesso.

**Nota:** as APIs criadas usando o `wsk api-experimental` continuarão funcionando por um curto período, no entanto, é necessário começar a migrar suas APIs para ações da web e reconfigurar suas APIs existentes usando o novo comando da CLI `wsk api`.

### Criar sua primeira API usando a CLI

1. Crie um arquivo JavaScript com o conteúdo a seguir. Para esse exemplo, o nome do arquivo é 'hello.js'.
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. Crie uma ação da web por meio da função JavaScript a seguir. Para este exemplo, a ação é chamada 'hello'. Certifique-se de incluir a sinalização `--web true`
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: ação hello criada
  ```
  
3. Crie uma API com o caminho base `/hello`, caminho `/world` e método `get` com o tipo de resposta `json`
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
  Uma nova URL é gerada expondo a ação `hello` por meio de um método de HTTP **GET**.
  
4. Vamos experimentá-lo enviando uma solicitação de HTTP para a URL.
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
     {
  "payload": "Hello world OpenWhisk"
  }
  ```
  A ação da web `hello` foi chamada, retornando um objeto JSON que inclui o parâmetro `name` enviado por meio do parâmetro de consulta. É possível passar parâmetros para a ação por meio de parâmetros de consulta simples ou por meio do corpo da solicitação. As ações da web permitem chamar uma ação de uma maneira pública sem a chave da API de autorização do OpenWhisk.
  
### Controle total sobre a resposta de HTTP
  
  A sinalização `--response-type` controla a URL de destino da ação da web a ter o proxy efetuado pelo API Gateway. Usando `--response-type json` como acima retorna o resultado integral da ação no formato JSON e configura automaticamente o cabeçalho Content-Type como `application/json`, que permite que você inicie facilmente. 
  
  Após iniciar, você deseja ter o controle total sobre as propriedades de resposta de HTTP como `statusCode`, `headers` e retornar tipos de conteúdo diferentes no `body`. É possível fazer isso usando `--response-type http`; isso configurará a URL de destino da ação da web com a extensão `http`.

  É possível escolher mudar o código da ação para obedecer ao retorno de ações da web com a extensão `http` ou incluir a ação em uma sequência passando seu resultado para uma nova ação que transforma o resultado para ser formatado adequadamente para uma resposta de HTTP. É possível ler mais sobre as extensões de tipos de resposta e ações da web na documentação [Ações da web](webactions.md).

  Mude o código para o `hello.js` retornando as propriedades JSON `body`, `statusCode` e `headers`
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  Observe que o corpo precisa ser retorno codificado em `base64` e não uma sequência.
  
  Atualize a ação com o resultado modificado
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  Atualize a API com `--response-type http`
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  Vamos chamar a API atualizada
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
     {
  "payload": "Hello world Serverless API"
  }
  ```
  Agora você está no controle total de suas APIs, pode controlar o conteúdo, como HTML de retorno, ou configurar o código de status para coisas como Não localizado (404) ou Desautorizado (401) ou até mesmo Erro interno (500).

### Expondo múltiplas ações da web

Digamos que você queira expor um conjunto de ações de um clube do livro para seus amigos.
Você tem uma série de ações para implementar seu backend para o clube do livro:

| ação | método de HTTP | Descrição |
| ----------- | ----------- | ------------ |
| getBooks    | GET | obter detalhes do livro  |
| postBooks   | POST | inclui um livro |
| putBooks    | PUT | atualiza detalhes do livro |
| deleteBooks | DELETE | exclui um livro |

Vamos criar uma API para o clube do livro chamada `Book Club`, com `/club` como seu caminho base da URL de HTTP e `books` como seu recurso.
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

Observe que a primeira ação exposta com o caminho base `/club` obtém o rótulo da API com o nome `Book Club`; quaisquer outras ações expostas sob `/club` serão associadas a `Book Club`

Vamos listar todas as ações que acabamos de expor.

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Agora, só por brincadeira, vamos incluir um novo livro `JavaScript: The Good Parts` com um HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

Vamos obter uma lista de livros usando nossa ação `getBooks` por meio de HTTP **GET**
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportando a Configuração
Vamos exportar a API chamada `Book Club` para um arquivo que poderemos usar como uma base para recriar as APIs usando um arquivo como entrada. 
```
wsk api get "Book Club" > club-swagger.json
```

Vamos testar o arquivo swagger excluindo primeiramente todas as URLs expostas em um caminho base comum.
É possível excluir todas as URLs expostas usando o caminho base `/club` ou o rótulo de nome da API `"Book Club"`:
```
wsk api delete /club
```
```
ok: deleted API /club
```
### Alterando a configuração

É possível editar a configuração no Painel do OpenWhisk, clicar na [guia APIs](https://console.ng.bluemix.net/openwhisk/apimanagement) para configurar a segurança, a limitação de taxa e outros recursos.

### Importando a Configuração

Agora vamos restaurar a API chamada `Book Club` usando o arquivo `club-swagger.json`
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Podemos verificar que a API foi recriada
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
