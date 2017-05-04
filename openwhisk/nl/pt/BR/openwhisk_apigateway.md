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

# API Gateway (Experimental)
{: #openwhisk_apigateway}

[Ações da web](openwhisk_webactions.html) são liberadas para disponibilidade geral.

As ações da web permitem que você chame uma ação com métodos de HTTP, além de POST, e sem a chave API de autorização da ação.

Como resultado do feedback do usuário, as Ações da web são o modelo de programação escolhido para construir ações do OpenWhisk capazes de manipular eventos HTTP.

A maioria da funcionalidade de API Gateway foi mesclada em Ações da web. As Ações da web permitem manipular qualquer solicitação de HTTP e retornar respostas de HTTP com controle total da sua Ação da web.

Uma integração revisada do OpenWhisk API Gateway estará disponível em breve. Ela será configurada para transmitir por proxy as Ações da web, fornecendo a elas recursos de API Gateway, como limitação de taxa, validação de token oauth, chaves API e muito mais. 
Veja o vídeo [Criar e controlar APIs](https://youtu.be/XT9KwWTnnzo)

**Nota:** as APIs criadas usando o `wsk api-experimental` continuarão funcionando, no entanto, será necessário iniciar a migração das APIs para as ações da web.

## Configuração da CLI do OpenWhisk
{: #openwhisk_apigateway_cli}
Esse recurso experimental só funciona com o novo modelo de autenticação do OpenWhisk no qual cada namespace agora tem uma chave de autenticação exclusiva associada a ele.
Siga as instruções em [Configurar a CLI](https://console.ng.bluemix.net/openwhisk/cli) sobre como configurar a chave de autenticação para seu namespace específico.

## Expor uma ação do OpenWhisk
{: #openwhisk_apigateway_hello}

Vamos expor uma ação simples que já esteja pré-instalada com o OpenWhisk

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
Uma nova URL é gerada ao expor a ação `echo` por meio de um método de HTTP **GET**.

Vamos experimentá-lo enviando uma solicitação de HTTP para a URL.
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
Isso chamará a ação `echo`, retornando uma sequência de caracteres JSON com os parâmetros enviados.
```
{
  "marco":"polo"
}
```
{: screen}

É possível passar parâmetros para a ação por meio de parâmetros de consulta simples ou por meio do corpo da solicitação.

### Expondo múltiplas ações
{: #openwhisk_apigateway_actions}

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
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

Observe que a primeira ação exposta com o caminho base `/club` obtém o rótulo da API com o nome `Book Club`; quaisquer outras ações expostas sob `/club` serão associadas a `Book Club`

Vamos listar todas as ações que acabamos de expor.

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Agora, só por brincadeira, vamos incluir um novo livro `JavaScript: The Good Parts` com um HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

Vamos obter uma lista de livros usando nossa ação `getBooks` por meio de HTTP **GET**
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportando a Configuração
Vamos exportar a API chamada `Book Club` para um arquivo que poderemos usar como uma base para recriar as APIs usando um arquivo como entrada. 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

Vamos testar o arquivo swagger excluindo primeiramente todas as URLs expostas em um caminho base comum.
É possível excluir todas as URLs expostas usando o caminho base `/club` ou o rótulo de nome da API `"Book Club"`:
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

Agora vamos restaurar a API chamada `Book Club` usando o arquivo `club-swagger.json`
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Podemos verificar que a API foi recriada
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **Nota**: esse recurso é atualmente uma oferta experimental que permite aos usuários uma oportunidade antecipada para experimentar e fornecer feedback. O feedback a seguir já foi recebido:
  - Nenhuma capacidade para customizar o controle de acesso HTTP para Compartilhamento de Recurso de Origem Cruzada (CORS); atualmente, os cabeçalhos de resposta da API gerada são configurados para permitir qualquer verbo ou origem HTTP (ou seja, *). Os cabeçalhos a seguir são sempre retornados:
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: autorização, tipo de conteúdo
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - Somente o tipo de conteúdo `application/json` é suportado para solicitação e resposta.
  - Nenhuma maneira programática para controlar a resposta da ação do OpenWhisk.
  - Todas as ações do OpenWhisk são expostas por meio de acesso público, nenhuma capacidade de configurar uma chave API customizada.
  - Parâmetros de caminho não são suportados, somente o parâmetro de consulta e o corpo da solicitação.
  - Se a API for criada sem um nome de API, o nome será o caminho base e isso não poderá ser mudado
  - Ao recriar as APIs por meio do arquivo de entrada, a API precisará ser excluída primeiro.
  - Ao exportar APIs, isso contém a chave API do OpenWhisk; essas informações são sensíveis, não há modelagem disponível.
