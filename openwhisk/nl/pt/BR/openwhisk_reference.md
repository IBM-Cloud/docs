---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Detalhes do sistema {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}
*Última atualização: 14 de abril de 2016*

As seções a seguir fornecem mais detalhes sobre o sistema {{site.data.keyword.openwhisk}}.
{: shortdesc}

## entidades do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Namespaces e pacotes

Ações, acionadores e regras do {{site.data.keyword.openwhisk_short}} devem estar em um namespace e, como opção, em um pacote.

Os pacotes podem conter ações e feeds. Um pacote não pode conter outro pacote, portanto, o aninhamento de pacote não é permitido. Além disso, as entidades não precisam estar contidas em um pacote.

No Bluemix, um par de organização+espaço corresponde a um namespace do {{site.data.keyword.openwhisk_short}}. Por exemplo, a organização `BobsOrg` e o espaço `dev` corresponderiam ao namespace do {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

É possível criar seus próprios namespaces se estiver autorizado a fazer isso. O namespace `/whisk.system` é reservado para entidades distribuídas com o sistema {{site.data.keyword.openwhisk_short}}.


### Nomes completos

O nome completo de uma entidade é `/namespaceName[/packageName]/entityName`. Observe que a `/` é usada para delimitar namespaces, pacotes e entidades. Além disso, os namespaces devem ter como prefixo uma `/`.

Por conveniência, o namespace poderá ser deixado desativado se for o *namespace padrão* do usuário.

Por exemplo, considere um usuário cujo namespace padrão seja `/myOrg`. Aqui estão exemplos de nomes completos de diversas entidades e seus aliases.

| Nome Completo | Alias | Namespace | Package | Nome |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `leitura` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `vídeo` | `transcode` |
| `/myOrg/filter` | `filtro` | `/myOrg` | - | `filtro` |

Você estará usando esse esquema de nomenclatura ao usar a CLI do {{site.data.keyword.openwhisk_short}}, entre outros locais.

### Nomes de entidades

Os nomes de todas as entidades, incluindo ações, acionadores, regras, pacotes e namespaces, são uma sequência de caracteres que seguem o formato a seguir:

* O primeiro caractere deve ser um caractere alfanumérico, um dígito ou um sublinhado.
* Os caracteres subsequentes podem ser alfanuméricos, dígitos, espaços ou qualquer um dos seguintes: `_`, `@`, `.`, `–`.
* O último caractere não pode ser um espaço.

Mais precisamente, um nome deve corresponder à seguinte expressão regular (expressa usando a sintaxe de metacaractere Java): `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Semântica de ação
{: #openwhisk_semantics}

As seções a seguir descrevem detalhes sobre ações do {{site.data.keyword.openwhisk_short}}.

### Statelessness

As implementações de ações devem ser stateless ou *idempotent*. Enquanto o sistema não impinge essa propriedade, não há garantias de que qualquer estado mantido por uma ação estará disponível entre chamadas.

Além disso, várias instanciações de uma ação podem existir, com cada instanciação tendo seu próprio estado. Uma chamada de ação pode ser despachada para qualquer uma dessas instanciações.

### Saída e entrada de chamada

A entrada e a saída de uma ação é um dicionário de pares de valores de chaves. A chave é uma sequência e o valor um valor JSON válido.

### Ordenação de chamada de ações
{: #openwhisk_ordering}

Chamadas de uma ação não são ordenadas. Se o usuário chamar uma
ação duas vezes a partir da linha de comandos ou a API REST, a
segunda chamada poderá ser executada antes da primeira. Se
as ações tiverem efeitos colaterais, elas poderão ser observadas em
qualquer ordem.

Além disso, não há garantia de execução de ações atomicamente. Duas ações podem ser executadas simultaneamente e seus efeitos secundários podem ser intercalados. Quaisquer efeitos colaterais de simultaneidade serão dependentes da implementação.

### No máximo uma vez semântica
{: #openwhisk_atmostonce}

O sistema suporta no máximo uma chamada de ações.

Quando uma solicitação de chamada é recebida, o sistema registra a solicitação e despacha uma ativação.

O sistema retorna um ID de ativação (no caso de uma chamada não de bloqueio) para confirmar que a chamada foi recebida. Observe que mesmo na ausência dessa resposta (talvez devido a uma conexão de rede interrompida), é possível que a chamada tenha sido recebida.

O sistema tenta chamar a ação uma vez, resultando em um dos quatro resultados a seguir:
- *sucesso*: a chamada da ação foi concluída com sucesso.
- *erro de aplicativo*: a chamada da ação foi bem-sucedida, mas a ação retornou um valor de erro de propósito, por exemplo, devido a uma pré-condição dos argumentos não ter sido cumprida.
- *erro de desenvolvedor da ação*: a ação foi chamada, mas foi concluída de forma anormal, por exemplo, a ação não capturou uma exceção ou existia um erro de sintaxe.
- *erro interno do whisk*: o sistema não pôde chamar a ação.
O resultado é registrado no campo `status` do registro de ativação, como documento em uma seção a seguir.

Cada chamada recebida com sucesso e para a qual o usuário pode ser faturado terá, eventualmente, um registro de ativação.


## Registro de ativação
{: #openwhisk_ref_activation}

Cada chamada de ação e disparo do acionador resulta em um registro de ativação.

Um registro de ativação contém os campos a seguir:

- *activationId*: o ID de ativação.
- *start* e *end*: registros de data e hora de início e término da ativação. Os valores estão no [formato de hora do UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* e `name`: o namespace e o nome da entidade.
- *logs*: uma matriz de sequências com os logs produzidos pela ação durante sua ativação. Cada elemento de matriz corresponde a uma saída de linha para stdout ou stderr pela ação e inclui a hora e o fluxo da saída do log. A estrutura é a seguinte: `'TIMESTAMP STREAM: LOG_OUTPUT'`.
- *response*: um dicionário que define as chaves `success`, `status` e `result`:
  - *status*: o resultado de ativação, que pode ser um dos valores a seguir: "sucesso", "erro de aplicativo", "erro de desenvolvedor da ação", "erro interno do whisk".
  - *success*: é `true` se, e somente se, o status for `"sucesso"`
- *result*: um dicionário que contém o resultado da ativação. Se a ativação foi bem-sucedida, conterá o valor retornado pela ação. Se a ativação foi mal sucedida, `result` terá a chave `error`, geralmente com uma explicação da falha.


## Ações JavaScript
{: #openwhisk_ref_javascript}

### Protótipo de função

As ações JavaScript do {{site.data.keyword.openwhisk_short}} são executadas em um tempo de execução Node.js, atualmente versão 0.12.9.

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

É comum que as funções JavaScript continuem a execução em uma função de retorno de chamada mesmo após o retorno. Para acomodar isso, uma ativação de uma ação JavaScript pode ser *síncrona* ou *assíncrona*.

A ativação de uma ação JavaScript é **síncrona** se a função principal sair sob uma das condições a seguir:

- A função principal sai sem executar uma instrução `'return'`.
- A função principal sai executando uma instrução `'return'` que retorna qualquer valor *exceto* `'whisk.async()'`.

Aqui estão dois exemplos de ações síncronas.

```
// a synchronous action function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicates normal completion
  } else if (params.payload == 2) {
    return whisk.error();   // indicates abnormal completion
  }
}
```
{: codeblock}

A ativação de uma ação JavaScript é **assíncrona** se a função principal sair chamando a função `'return whisk.async();'`.  Nesse caso, o sistema assume que a ação ainda está em execução, até que a ação execute um dos seguintes:
- ```return whisk.done();```
- ```return whisk.error();```

Aqui está um exemplo de uma ação executada de forma assíncrona.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

É possível que uma ação seja síncrona em algumas entradas e assíncrona em outras. Eis um exemplo:

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // ativação assíncrona
      }  else {
         return whisk.done();   // ativação síncrona
      }
  }
```
{: codeblock}

- Nesse caso, a função `main` deve retornar `whisk.async()`. Quando o resultado da ativação está disponível, a função `whisk.done()` deve ser chamada com o resultado passado como um objeto JSON. Isso é referido como uma ativação *assíncrona*.

Observe que, independentemente de se uma ativação é síncrona ou assíncrona, a chamada da ação pode ser bloqueada ou sem bloqueio.

### Métodos adicionais do SDK

A função `whisk.invoke()` chama outra ação. Ela aceita como um argumento um dicionário que define os parâmetros a seguir:

- *name*: o nome completo da ação a ser chamada,
- *parameters*: um objeto JSON que representa a entrada para a ação chamada. Se omitido, usa como padrão um objeto vazio.
- *apiKey*: a chave de autorização com a qual chamar a ação. Usa como padrão `whisk.getAuthKey()`. 
- *blocking*: se a ação deve ser chamada no modo de bloqueio ou sem bloqueio. Usa como padrão `false`, indicando uma chamada sem bloqueio.
- *next*: uma função de retorno de chamada opcional a ser executada quando a chamada for concluída.

A assinatura para `next` é `function(error, activation)`, em que:

- `error` é `false` se a chamada tiver sido bem-sucedida e um valor verdadeiro se tiver falhado, geralmente, uma sequência descrevendo o erro.
- Em erros, `activation` pode ficar indefinida, dependendo do modo de falha.
- Quando definida, `activation` é um dicionário com os campos a seguir:
  - *activationId*: o ID de ativação:
  - *result*: se a ação tiver sido chamada no
modo de bloqueio: o resultado da ação será um objeto JSON, caso contrário `undefined`.

A função `whisk.trigger()` dispara um acionador. Ela aceita como um argumento um objeto JSON com os parâmetros a seguir:

- *name*: o nome completo do acionador a ser chamado.
- *parameters*: um objeto JSON que representa a entrada para o acionador. Se omitido, usa como padrão um objeto vazio.
- *apiKey*: a chave de autorização com a qual disparar o acionador. Usa como padrão `whisk.getAuthKey()`.
- *next*: uma função de retorno de chamada opcional a ser executada quando o disparo for concluído.

A assinatura para `next` é `function(error, activation)`, em que:

- `error` é `false` se o disparo tiver sido bem-sucedido e um valor verdadeiro se tiver falhado, geralmente, uma sequência descrevendo o erro.
- Em erros, `activation` pode ficar indefinida, dependendo do modo de falha.
- Quando definida, `activation` é um dicionário com um campo `activationId` que contém o ID de ativação.

A função `whisk.getAuthKey()` retorna a chave de autorização sob a qual a ação está em execução. Normalmente, não é necessário chamar essa função diretamente porque ela é usada implicitamente pelas funções `whisk.invoke()` e `whisk.trigger()`.

### Ambiente de Tempo de Execução
{: #openwhisk_ref_runtime_environment}

As ações JavaScript são executadas em um ambiente do Node.js versão 0.12.9 com os pacotes a seguir disponíveis para serem usados pela ação:

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- base
- errorhandler
- expresso
- express-session
- jade
- log4js
- mesclar
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- pedido
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Ações do Docker
{: #openwhisk_ref_docker}

As ações do Docker executam binário fornecido pelo usuário em um contêiner do Docker. O binário é executado em uma imagem do Docker com base no Ubuntu 14.04 LTD, de modo que o binário deve ser compatível com essa distribuição.

O parâmetro "payload" de entrada da ação é passado como um argumento posicional ao programa binário e a saída padrão da execução do programa é retornada no parâmetro "result".

A estrutura básica do Docker é uma maneira conveniente de construir imagens do Docker compatíveis com o {{site.data.keyword.openwhisk_short}}. É possível instalar a estrutura básica com o comando da CLI `wsk sdk install docker`.

O programa binário principal deve ser copiado para o arquivo `dockerSkeleton/client/clientApp`. Quaisquer arquivos ou bibliotecas associados podem residir no diretório `dockerSkeleton/client`.

Também é possível incluir qualquer etapa ou dependência de compilação modificando o `dockerSkeleton/Dockerfile`. Por exemplo, será possível instalar o Python se sua ação for um script Python.


## Limites do sistema
{: #openwhisk_syslimits}

O {{site.data.keyword.openwhisk_short}} tem alguns limites do sistema, incluindo quanto de memória uma ação usa e quantas chamadas de ação são permitidas por hora. A tabela a seguir lista os limites padrão.

| limite | Descrição | configuráveis | unit | Padrão |
| ----- | ----------- | ------------ | -----| ------- |
| tempo limite | um contêiner não tem permissão para executar por mais de N milissegundos | por ação |  milliseconds | 60000 |
| memória | um contêiner não tem permissão para alocar mais de N MB de memória | por ação | MB | 256 |
| simultâneo | não é permitido ter mais de N ativações simultâneas por namespace | por namespace | number | 100 |
| minuteRate | um usuário não pode chamar mais do que este número de ações por minuto | por usuário | number | 120 |
| hourRate | um usuário não pode chamar mais do que este número de ações por hora | por usuário | number | 3600 |

### Tempo limite (ms) por ação (Padrão: 60s)
* O limite N de tempo limite está no intervalo [100ms..300.000ms] e é configurado por ação em milissegundos.
* Um usuário pode mudar o limite ao criar a ação.
* Um contêiner executado mais de N milissegundos é finalizado.

### Memória (MB) por ação (Padrão: 256 MB)
* O limite M de memória está no intervalo [128MB..512MB] e é configurado por ação em MB.
* Um usuário pode mudar o limite ao criar a ação.
* Um contêiner não pode ter mais memória alocada do que o limite.

### Nº de chamadas simultâneas (Nº) por namespace (Padrão: 100)
* O número de ativações que são atualmente processadas para um namespace não pode exceder 100.
* O limite padrão pode ser estaticamente configurado pelo whisk no consul kvstore.
* Um usuário atualmente não é capaz de mudar os limites.


### Chamadas por minuto/hora (Nº) (Fixo: 120/3.600)
* O limite de taxa N é configurado para 120/3.600 e limita o número de chamadas de ações em janelas de um minuto/hora.
* Um usuário não pode mudar esse limite ao criar a ação.
* Uma chamada da CLI que exceder esse limite receberá um código de erro correspondente a TOO_MANY_REQUESTS.
