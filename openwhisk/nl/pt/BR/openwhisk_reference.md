---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Detalhes do sistema {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}


As seções a seguir fornecem mais detalhes sobre o sistema {{site.data.keyword.openwhisk}}.
{: shortdesc}

## entidades do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Namespaces e pacotes
{: #openwhisk_entities_namespaces}

Ações, acionadores e regras do {{site.data.keyword.openwhisk_short}} devem estar em um namespace e, como opção, em um pacote.

Os pacotes podem conter ações e feeds. Um pacote não pode conter outro pacote, portanto, o aninhamento de pacote não é permitido. Além disso, as entidades não precisam estar contidas em um pacote.

No Bluemix, um par organização+espaço corresponde a um namespace do {{site.data.keyword.openwhisk_short}}. Por exemplo, a organização `BobsOrg` e o espaço `dev` corresponderiam ao namespace do {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

É possível criar seus próprios namespaces se estiver autorizado a fazer isso. O namespace `/whisk.system` é reservado para entidades distribuídas com o sistema {{site.data.keyword.openwhisk_short}}.


### Nomes completos
{: #openwhisk_entities_fullyqual}

O nome completo de uma entidade é `/namespaceName[/packageName]/entityName`. Observe que a `/` é usada para delimitar namespaces, pacotes e entidades. Além disso, os namespaces devem ter como prefixo uma `/`.

Por conveniência, o namespace poderá ser deixado desativado se for o
*namespace padrão* do usuário.

Por exemplo, considere um usuário cujo namespace padrão seja `/myOrg`. Seguem
exemplos de nomes completos de diversas entidades e seus aliases.

| Nome Completo | Alias | Namespace | Package | Nome |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `leitura` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `vídeo` | `transcode` |
| `/myOrg/filter` | `filtro` | `/myOrg` |  | `filtro` |

Você estará usando esse esquema de nomenclatura ao usar a CLI do {{site.data.keyword.openwhisk_short}}, entre outros locais.

### Nomes de entidades
{: #openwhisk_entities_names}

Os nomes de todas as entidades, incluindo ações, acionadores, regras, pacotes e
namespaces, são uma sequência de caracteres que seguem o formato a seguir:

* O primeiro caractere deve ser um caractere alfanumérico ou um sublinhado.
* Os caracteres subsequentes podem ser alfanuméricos, espaços ou qualquer um dos seguintes: `_`, `@`, `.`, `-`.
* O último caractere não pode ser um espaço.

Mais precisamente, um nome deve corresponder à expressão regular a seguir (expressa
com a sintaxe de metacaractere Java):
`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Semântica de ação
{: #openwhisk_semantics}

As seções a seguir descrevem detalhes sobre ações do {{site.data.keyword.openwhisk_short}}.

### Statelessness
{: #openwhisk_semantics_stateless}

As implementações de ações devem ser stateless ou *idempotent*. Enquanto o sistema não impinge essa propriedade, não há garantias de que qualquer estado mantido por uma ação estará disponível entre chamadas.

Além disso, várias instanciações de uma ação podem existir, com cada instanciação tendo seu próprio estado. Uma chamada de ação pode ser despachada para qualquer uma dessas instanciações.

### Saída e entrada de chamada
{: #openwhisk_semantics_invocationio}

A entrada e a saída de uma ação é um dicionário de pares de valores de chaves. A chave é uma sequência e o valor um valor JSON válido.

### Ordenação de chamada de ações
{: #openwhisk_ordering}

Chamadas de uma ação não são ordenadas. Se o usuário chamar uma ação duas vezes por meio da linha de comandos ou a API REST, a segunda chamada poderá ser executada antes
da primeira. Se
as ações tiverem efeitos colaterais, elas poderão ser observadas em
qualquer ordem.

Além disso, não há garantia de execução de ações atomicamente. Duas ações podem ser executadas simultaneamente e seus efeitos secundários podem ser intercalados. O OpenWhisk não assegura qualquer
modelo de consistência simultâneo específico para efeitos colaterais. Quaisquer efeitos
colaterais de simultaneidade serão dependentes da implementação.

### Garantias de execução de ação
{: #openwhisk_atmostonce}

Quando uma solicitação de chamada é recebida, o sistema registra a solicitação e despacha uma ativação.

O sistema retorna um ID de ativação (no caso de uma chamada não de bloqueio) para
confirmar que a chamada foi recebida.
Observe que se houver uma falha de rede ou outra falha que intervenha antes de você receber uma resposta HTTP, será possível
que o {{site.data.keyword.openwhisk_short}} tenha recebido e processado a solicitação.

O sistema tenta chamar a ação uma vez, resultando em um dos quatro resultados a seguir:
- *sucesso*: a chamada da ação foi concluída com sucesso.
- *erro de aplicativo*: a chamada da ação foi bem-sucedida, mas a ação retornou um valor de erro de propósito, por exemplo, devido a uma pré-condição dos argumentos não ter sido cumprida.
- *erro de desenvolvedor da ação*: a ação foi chamada, mas foi
concluída de forma anormal, por exemplo, a ação não detectou uma exceção ou existia um
erro de sintaxe.
- *erro interno do whisk*: o sistema não pôde chamar a ação.
O resultado é registrado no campo `status` do registro de ativação, como documento em uma seção a seguir.

Cada chamada recebida com sucesso e para a qual o usuário pode ser faturado terá, eventualmente, um registro de ativação.

Observe que no caso de *erro de desenvolvedor de ação*, a ação pode ter sido executada parcialmente e ter gerado efeitos colaterais
visíveis externamente.   É de responsabilidade do usuário verificar se esses efeitos colaterais realmente aconteceram e emitir lógica
de nova tentativa, se desejado.   Observe também que determinados *erros internos de whisk* indicarão que uma ação iniciou a execução,
mas o sistema falhou antes da ação registrar a conclusão.

## Registro de ativação
{: #openwhisk_ref_activation}

Cada chamada de ação e disparo do acionador resulta em um registro de ativação.

Um registro de ativação contém os campos a seguir:

- *activationId*: o ID de ativação.
- *start* e *end*: registros de data e hora de início e término da ativação. Os valores estão no [formato de hora do UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* e `name`: o namespace e o nome da entidade.
- *logs*: uma matriz de sequências com os logs produzidos pela ação
durante sua ativação. Cada elemento de matriz corresponde a uma saída de linha para
`stdout` ou `stderr` pela ação e inclui a hora e o
fluxo da saída do log. A estrutura é a seguinte: `TIMESTAMP STREAM: LOG_OUTPUT`.
- *response*: um dicionário que define as chaves `success`, `status` e `result`:
  - *status*: o resultado de ativação, que pode ser um dos valores a seguir: "sucesso", "erro de aplicativo", "erro de desenvolvedor da ação", "erro interno do whisk".
  - *success*: é `true` se e somente se o status for `"sucesso"`
- *result*: um dicionário que contém o resultado da ativação. Se a
ativação foi bem-sucedida, conterá o valor retornado pela ação. Se a ativação foi mal
sucedida, `result` terá a chave `error`, geralmente com
uma explicação da falha.


## Ações JavaScript
{: #openwhisk_ref_javascript}

### Protótipo de função
{: #openwhisk_ref_javascript_fnproto}

As ações de JavaScript do {{site.data.keyword.openwhisk_short}} são executadas em um tempo de execução do Node.js.

Ações escritas em JavaScript devem ser confinadas a um único arquivo. O arquivo pode conter várias funções, mas por convenção uma função chamada `main` deve existir e é a chamada quando a ação for chamada. Por exemplo, a seguir está um exemplo de uma ação com várias funções.

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

Os parâmetros de entrada de ação são passados como um objeto JSON como um parâmetro para a função `main`. O resultado de uma ativação bem-sucedida também é um objeto JSON, mas é retornado de forma diferente dependendo de se a ação é síncrona ou assíncrona conforme descrito na seção a seguir.


### Comportamento síncrono e assíncrono
{: #openwhisk_ref_javascript_synchasynch}

É comum que as funções JavaScript continuem a execução em uma função de retorno de
chamada mesmo após um retorno. Para acomodar isso, uma ativação de uma ação JavaScript
pode ser *síncrona* ou *assíncrona*.

A ativação de uma ação JavaScript é **síncrona** se a função principal sair sob uma das condições a seguir:

- A função principal sai sem executar uma instrução `return`.
- A função principal sai executando uma instrução `return` que retorna qualquer valor *exceto* uma Promessa.

Aqui está um exemplo de ação síncrona.

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

A ativação de uma ação JavaScript será **assíncrona** se a
função principal sair retornando uma Promessa.  Nesse caso, o sistema assume que a ação
ainda está em execução, até que a Promessa tenha sido cumprida ou rejeitada.
Comece
instanciando um novo objeto Promessa e passando a ele uma função de retorno de chamada. O
retorno de chamada aceita dois argumentos, resolver e rejeitar, que são ambos funções. Todos
os códigos assíncronos vão dentro desse retorno de chamada.


Segue um exemplo de como cumprir uma Promessa chamando a função resolver.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Segue um exemplo de como rejeitar uma Promessa chamando a função rejeitar.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

É possível que uma ação seja síncrona em algumas entradas e assíncrona em outras. A seguir há um exemplo.

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
                }, 100);
             })
      } else {
         // synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

Observe que, independentemente de uma ativação ser síncrona ou assíncrona, a
chamada da ação pode bloqueio ou não bloqueio.

### Objeto whisk global JavaScript global removido

O objeto global `whisk` foi removido; migre suas ações de nodejs para
usar métodos alternativos.
Para as funções `whisk.invoke()` e `whisk.trigger()`, use a
biblioteca do cliente [openwhisk](https://www.npmjs.com/package/openwhisk) já instalada.
Para `whisk.getAuthKey()`, é possível obter o valor da chave API da variável de ambiente `__OW_API_KEY`.
Para `whisk.error()`, é possível retornar uma Promessa rejeitada (ou seja, Promise.reject).

### Ambientes de tempo de execução do JavaScript
{: #openwhisk_ref_javascript_environments}

As ações de JavaScript são executadas por padrão em um ambiente do Node.js versão 6.9.1.  O
ambiente 6.9.1 também será usado para uma ação se a sinalização `--kind` for explicitamente especificada com um valor 'nodejs:6' ao criar/atualizar a ação.
Os pacotes a seguir estão disponíveis para serem usados no ambiente do Node.js 6.9.1:

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.3.2
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.29.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0


## Ambientes de tempo de execução do Python
{: #openwhisk_ref_python_environments}

O OpenWhisk suporta a execução de ações Python usando duas versões de tempo de execução diferentes.

### Ações do Python 3

As ações do Python 3 são executadas usando o Python 3.6.1. Para usar esse tempo de execução, especifique o parâmetro da CLI `wsk`,
`--kind python:3` ao criar ou atualizar uma ação.
Os pacotes a seguir estão disponíveis para
uso por ações do Python, além das bibliotecas padrão do Python 3.6.

- aiohttp v1.3.3
- appdirs v1.4.3
- asn1crypto v0.21.1
- async-timeout v1.2.0
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- chardet v2.3.0
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- Flask v0.12
- gevent v1.2.1
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- multidict v2.1.4
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- w3lib v1.17.0
- Werkzeug v0.12
- yarl v0.9.8
- zope.interface v4.3.3

### Ações do Python 2

As ações do Python 2 são executadas usando o Python 2.7.12. Esse é o tempo de execução padrão para ações do Python, a menos que você especifique a sinalização
`--kind` ao criar ou atualizar uma ação. Para selecionar explicitamente esse tempo de
execução, use `--kind python:2`. Os pacotes a seguir estão disponíveis para uso por ações do
Python 2, além da biblioteca padrão do Python 2.7.

- appdirs v1.4.3
- asn1crypto v0.21.1
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- enum34 v1.1.6
- Flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- ipaddress v1.0.18
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- virtualenv v15.1.0
- w3lib v1.17.0
- Werkzeug v0.12
- zope.interface v4.3.3

## Ações do Docker
{: #openwhisk_ref_docker}

As ações do Docker executam binário fornecido pelo usuário em um contêiner do Docker. O binário é executado em uma imagem do Docker com base no
[python:2.7.12-alpine](https://hub.docker.com/r/library/python), de maneira que o binário deve ser compatível com essa distribuição.

A estrutura básica do Docker é uma maneira conveniente de construir imagens do Docker compatíveis com o OpenWhisk. É possível instalar a estrutura básica com o comando da CLI `wsk sdk install docker`.

O programa binário principal deve estar localizado em `/action/exec` dentro do contêiner. O executável recebe os argumentos de entrada por meio de uma sequência única de argumentos de linha de comandos que pode ser desserializada como um objeto `JSON`. Ele deve retornar um resultado por meio de `stdout` como sequência de linha única de `JSON` serializado.

Você pode incluir qualquer etapa ou dependência de compilação modificando o `Dockerfile` incluído no `dockerSkeleton`.

## API REST
{: #openwhisk_ref_restapi}

Todos os recursos no sistema estão disponíveis por meio de uma API REST. Existem terminais de coleção e entidade para ações, acionadores, regras, pacotes, ativações e namespaces.

Estes são os terminais de coleta:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations`

O `openwhisk.`<span class="keyword" data-hd-keyref="DomainName">DomainName</span>' é o nome do host da API OpenWhisk (por exemplo, openwhisk.ng.bluemix.net, 172.17.0.1 e assim por diante).

Para o `{namespace}`, o caractere `_` pode ser
usado para especificar o *namespace padrão* do usuário (isto é, endereço de e-mail).

É possível executar uma solicitação GET nos terminais de coleção para buscar uma
lista de entidades na coleção.

Existem terminais de entidade para cada tipo de entidade:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations/{activationName}`


Os terminais de namespace e ativação suportam apenas solicitações GET. Os terminais
de ações, acionadores, regras e pacotes suportam solicitações GET, PUT e DELETE. Os
terminais de ações, acionadores e regras também suportam solicitações POST, que são
usadas para chamar ações e acionadores e ativar ou desativar as regras. Consulte a [Referência de API](https://console.{DomainName}/apidocs/98)
para obter detalhes.

Todas as APIs são protegidas com autenticação Básica de HTTP. As credenciais de
autenticação Básica estão na propriedade `AUTH` em seu arquivo
`~/.wskprops`, delimitadas por dois pontos. Também é possível recuperar essas credenciais nas [etapas de configuração da CLI](./index.html#openwhisk_start_configure_cli).

Segue um exemplo que usa o comando cURL para obter a lista de todos os pacotes
no namespace `whisk.system`:

```
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

A API OpenWhisk suporta chamadas de solicitação-resposta de Web clients. O OpenWhisk responde para solicitações de `OPTIONS` com cabeçalhos de Compartilhamento de Recurso de Origem
Cruzada. Atualmente, todas as origens são permitidas (ou seja, a Origem de Permissão de
Controle de Acesso é "`*`") e os Cabeçalhos de Permissão de Controle de
Acesso produzem Autorização e Tipo de Conteúdo.

**Atenção:** como o OpenWhisk suporta apenas uma chave por conta
atualmente, não é recomendado usar CORS além de experimentos simples. Sua chave
precisaria ser integrada no código do lado do cliente, tornando-a visível para o público. Use
com cuidado.

## Limites do sistema
{: #openwhisk_syslimits}

### Ações
O {{site.data.keyword.openwhisk_short}} possui alguns limites do sistema, incluindo o quanto de memória uma ação pode usar e quantas chamadas de ação são permitidas por minuto.

A tabela a seguir lista os
limites padrão para ações.

| limite | Descrição | configuráveis | unit | Padrão |
| ----- | ----------- | ------------ | -----| ------- |
| tempo limite | um contêiner não tem permissão para executar por mais de N milissegundos | por ação |  milliseconds | 60000 |
| memória | um contêiner não tem permissão para alocar mais de N MB de memória | por ação | MB | 256 |
| Registros do | um contêiner não tem permissão para gravar mais de N MB na saída padrão | por ação | MB | 10 |
| simultâneo | não mais que N ativações são permitidas por namespace em execução ou enfileiradas para execução | por namespace | number | 1000 |
| minuteRate | não mais que N ativações podem ser enviadas por namespace por minuto | por usuário | number | 5000 |
| codeSize | o tamanho máximo do código de ação | não configurável, limite por ação | MB | 48 |
| parâmetros | o tamanho máximo dos parâmetros que podem ser anexados | não configurável, limite por ação/pacote/acionador | MB | 1 |

### Tempo limite (ms) por ação (Padrão: 60s)
{: #openwhisk_syslimits_timeout}
* O limite N de tempo limite está no intervalo [100ms..300.000ms] e é configurado por ação em milissegundos.
* Um usuário pode mudar o limite ao criar a ação.
* Um contêiner executado mais de N milissegundos é finalizado.

### Memória (MB) por ação (Padrão: 256 MB)
{: #openwhisk_syslimits_memory}
* O limite M de memória está no intervalo [128MB..512MB] e é configurado por ação em MB.
* Um usuário pode mudar o limite ao criar a ação.
* Um contêiner não pode ter mais memória alocada do que o limite.

### Por logs de ação (MB) (Padrão: 10MB)
{: #openwhisk_syslimits_logs}
* O limite N do log está no intervalo [0MB..10MB] e é configurado por ação.
* Um usuário pode mudar o limite ao criar ou atualizar a ação.
* Logs que excedem o limite definido são truncados e um aviso é incluído como
última saída da ativação para indicar que a ativação excedeu o limite de log configurado.

### Por artefato de ação (MB) (Fixo: 48 MB)
{: #openwhisk_syslimits_artifact}
* O tamanho máximo do código da ação é 48 MB.
* É recomendado para uma ação de JavaScript usar uma ferramenta para concatenar todos os códigos-fonte incluindo dependências em um único arquivo em pacote configurável.

### Por tamanho de carga útil de ativação (MB) (Fixo: 1 MB)
{: #openwhisk_syslimits_activationsize}
* O tamanho do conteúdo máximo de POST mais quaisquer parâmetros preparados para uma chamada de ação ou um disparo de acionador é 1 MB.

### Por chamada simultânea de namespace (padrão: 1.000)
{: #openwhisk_syslimits_concur}
* O número de ativações que estão em execução ou enfileiradas para execução para um namespace não pode exceder 1.000.
* O limite padrão pode ser estaticamente configurado pelo whisk no consul kvstore.
* Um usuário atualmente não é capaz de mudar os limites.

### Chamadas por minuto (fixo: 5.000)
{: #openwhisk_syslimits_invocations}
* O limite de taxa N é configurado para 5.000 e limita o número de chamadas de ações em janelas de um minuto.
* Um usuário não pode mudar esse limite ao criar a ação.
* Uma CLI ou chamada API que exceder esse limite receberá um código de erro correspondente ao código de status de HTTP `429: TOO MANY REQUESTS`.

### Tamanho dos parâmetros (Fixo: 1 MB)
{: #openwhisk_syslimits_parameters}
* O limite de tamanho dos parâmetros na criação ou atualização de uma ação/pacote/acionador é 1 MB.
* O limite não pode ser alterado pelo usuário.
* Uma entidade com parâmetros muito grandes será rejeitada ao tentar criá-la ou atualizá-la.

### Ulimit de arquivos abertos por ação do Docker (Fixo: 64:64)
{: #openwhisk_syslimits_openulimit}
* O número máximo de arquivos abertos é 64 (para os limites máximo e flexível).
* O comando de execução do docker usa o argumento `--ulimit nofile=64:64`.
* Para obter mais informações sobre o ulimit para arquivos abertos, consulte a
documentação de [execução do
docker](https://docs.docker.com/engine/reference/commandline/run).

### Por processos de ação do Docker de ulimit (Fixo: 512:512)
{: #openwhisk_syslimits_proculimit}
* O número máximo de processos disponíveis a um usuário é 512 (para os limites máximo e flexível).
* O comando de execução do docker usa o argumento `--ulimit nproc=512:512`.
* Para obter mais informações sobre o ulimit para número máximo de processos, consulte a documentação de
[execução do
docker](https://docs.docker.com/engine/reference/commandline/run).

### Acionador

Os acionadores estão sujeitos a uma taxa de disparo por minuto, conforme documentado na tabela abaixo.

| limite | Descrição | configuráveis | unit | Padrão |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | não mais que N acionadores podem ser disparados por namespace por minuto | por usuário | number | 5000 |

### Acionadores por minuto (fixo: 5.000)
* O limite de taxa N é configurado para 5.000 e limita o número de acionadores que podem ser disparados em janelas de um minuto.
* Um usuário não pode mudar esse limite ao criar o acionador.
* Uma CLI ou chamada API que exceder esse limite receberá um código de erro correspondente ao código de status de HTTP `429: TOO MANY REQUESTS`.
