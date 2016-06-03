---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Usando e criando pacotes do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_packages}
*Última atualização: 28 de março de 2016*

No {{site.data.keyword.openwhisk}}, é possível usar pacotes para empacotar um conjunto de ações relacionadas juntas e compartilhá-las com outras pessoas.

Um pacote pode incluir *ações* e *feeds*.
- Uma ação é uma parte do código executada no {{site.data.keyword.openwhisk_short}}. Por exemplo, o pacote Cloudant inclui ações para ler e gravar registros em um banco de dados do Cloudant.
- Um feed é usado para configurar uma origem de eventos externos para disparar eventos acionadores. Por exemplo, o pacote Alarme inclui um feed que pode disparar um acionador a uma frequência especificada.

Cada entidade do {{site.data.keyword.openwhisk_short}}, incluindo pacotes, pertence a um *namespace* e o nome completo de uma entidade é `/namespaceName[/packageName]/entityName`. Consulte as [diretrizes de nomenclatura](./openwhisk_reference.html#openwhisk_entities) para obter mais informações.

As seções a seguir descrevem como procurar pacotes e usar acionadores e feeds nos mesmos. Além disso, para aqueles interessados em contribuir com seus próprios pacotes para o catálogo, leia as seções sobre a criação e o compartilhamento de pacotes.

## Procurando pacotes
{: #openwhisk_packagedisplay}

Vários pacotes são registrados com o {{site.data.keyword.openwhisk_short}}. É possível obter uma lista de pacotes em um namespace, listar as entidades em um pacote e obter uma descrição das entidades individuais em um pacote.

1. Obtenha uma lista de pacotes no namespace `/whisk.system`.

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  pacotes
  /whisk.system/alarms                                              compartilhado
  /whisk.system/cloudant                                            compartilhado
  /whisk.system/github                                              compartilhado
  /whisk.system/samples                                             compartilhado
  /whisk.system/slack                                               compartilhado
  /whisk.system/util                                                compartilhado
  /whisk.system/watson                                              compartilhado
  /whisk.system/weather                                             compartilhado
  ```
  {: screen}

2. Obtenha uma lista de entidades no namespace `/whisk.system/cloudant`.

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  pacote /whisk.system/cloudant: serviço de banco de dados do Cloudant
     (parâmetros: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   ação /whisk.system/cloudant/read: ler documento do banco de dados
   ação /whisk.system/cloudant/write: gravar documento no banco de dados
   feed /whisk.system/cloudant/changes: feed de mudança do banco de dados
  ```
  {: screen}

  Essa saída mostra que o pacote Cloudant fornece duas ações, `read` e `write` e um feed acionador denominado `changes`. O feed `changes` dispara acionadores quando documentos são incluídos no banco de dados especificado do Cloudant.

  O pacote Cloudant também define os parâmetros `username`, `password`, `host` e `port`. Esses parâmetros devem ser especificados para que as ações e os feeds sejam significativos. Os parâmetros permitem que as ações operem em uma conta específica do Cloudant, por exemplo.

3. Obtenha uma descrição da ação `/whisk.system/cloudant/read`.

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  ação /whisk.system/cloudant/read: ler documento do banco de dados
     (parâmetros: dbname includeDoc id)
  ```
  {: screen}

  Essa saída mostra que a ação `read` do Cloudant requer três parâmetros, incluindo o banco de dados e o ID do documento a ser recuperado.


## Chamando ações em um pacote
{: #openwhisk_package_invoke}

É possível chamar ações em um pacote, exatamente como outras ações. As próximas poucas etapas mostram como chamar a ação `greeting` no pacote `/whisk.system/samples` com diferentes parâmetros.

1. Obtenha uma descrição da ação `/whisk.system/samples/greeting`.

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  ação /whisk.system/samples/greeting: imprimir uma saudação amistosa
     (parâmetros: name place)
  ```
  {: screen}

  Observe que a ação `greeting` usa dois parâmetros: `name` e `place`.

2. Chame a ação sem quaisquer parâmetros.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  A saída é uma mensagem genérica porque nenhum parâmetro foi especificado.

3. Chame a ação com parâmetros.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  Observe que a saída usa os parâmetros `name` e `place` que foram passados para a ação.


## Criando e usando ligações de pacote
{: #openwhisk_package_bind}

Embora seja possível usar as entidades em um pacote diretamente, você pode observar que está passando os mesmos parâmetros para a ação toda vez. É possível evitar isso fazendo a ligação com um pacote e especificando parâmetros padrão. Esses parâmetros são herdados pelas ações no pacote.

Por exemplo, no pacote `/whisk.system/cloudant`, é possível configurar valores padrão de `username`, `password` e `dbname` em uma ligação de pacote e esses valores serão passados automaticamente a qualquer ação no pacote.

No exemplo simples a seguir, você faz a ligação com o pacote `/whisk.system/samples`.

1. Faça a ligação com o pacote `/whisk.system/samples` e configure um valor de parâmetro `place` padrão.

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: ligação valhallaSamples criada
  ```
  {: screen}

2. Obtenha uma descrição da ligação do pacote.

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  pacote /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: imprimir uma saudação amistosa
   action /myNamespace/valhallaSamples/wordCount: contar palavras em uma sequência
   action /myNamespace/valhallaSamples/helloWorld: imprimir no console
   action /myNamespace/valhallaSamples/echo: retorna os argumentos de entrada, não mudados
  ```
  {: screen}

  Observe que todas as ações no pacote `/whisk.system/samples` estão disponíveis na ligação do pacote `valhallaSamples`.

3. Chame uma ação na ligação do pacote.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  Observe no resultado que a ação herda o parâmetro `place` configurado ao criar a ligação do pacote `valhallaSamples`.

4. Chame uma ação e sobrescreva o valor de parâmetro padrão.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  Observe que o valor do parâmetro `place` especificado com a chamada da ação sobrescreve o valor padrão configurado na ligação do pacote `valhallaSamples`.


## Criando e usando feeds acionadores
{: #openwhisk_package_trigger}

Feeds oferecem uma maneira conveniente para configurar uma origem de eventos externos para disparar esses eventos para um acionador do {{site.data.keyword.openwhisk_short}}. Este exemplo mostra como usar um feed no pacote Alarmes para disparar um acionador a cada segundo e usar uma regra para chamar uma ação a cada segundo.

1. Obtenha uma descrição do feed no pacote `/whisk.system/alarms`.

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  pacote /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  ação /whisk.system/alarms/alarm: disparar acionador quando o alarme ocorrer
     (parâmetros: cron trigger_payload)
  ```
  {: screen}

  O feed `/whisk.system/alarms/alarm` aceita dois parâmetros:
  - `cron`: uma especificação de crontab de quando disparar o acionador.
  - `trigger_payload`: o valor de parâmetro de payload para configurar em cada evento acionador.

2. Crie um acionador que dispare a cada oito segundos.

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: feed acionador everyEightSeconds criado
  ```
  {: screen}

3. Crie um arquivo 'hello.js' com o código de ação a seguir.

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. Certifique-se de que a ação existe.

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. Crie uma regra que chama a ação `hello` toda vez que o acionador `everyEightSeconds` é disparado.

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: regra myRule criada
  ok: regra myRule está sendo ativada
  ```
  {: screen}

6. Verifique se a ação está sendo chamada pesquisando os logs de ativação.

  ```
  wsk activation poll
  ```
  {: pre}

  É necessário ver ativações a cada oito segundos para o acionador, a regra e a ação. A ação recebe os parâmetros `{"name":"Mork", "place":"Ork"}` em cada chamada.


## Criando um Pacote
{: #openwhisk_packages_create}

Um pacote é usado para organizar um conjunto de ações e feeds relacionados.
Também permite que os parâmetros sejam compartilhados entre todas as entidades no pacote.

Para criar um pacote customizado com uma ação simples nele, tente o exemplo a seguir:

1. Crie um pacote chamado "custom".

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: pacote custom criado
  ```
  {: screen}

2. Obtenha um resumo do pacote.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  pacote /myNamespace/custom
  ```
  {: screen}

  Observe que o pacote está vazio.

3. Crie um arquivo chamado `identity.js` que contenha o código de ação a seguir. Essa ação retorna todos os parâmetros de entrada.

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. Crie uma ação `identity` no pacote `custom`.

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: ação custom/identity criada
  ```
  {: screen}

  A criação de uma ação em um pacote requer que o nome da ação tenha como prefixo um nome de pacote. Aninhamento de pacote não é permitido. Um pacote pode conter apenas ações e não pode conter outro pacote.

5. Obtenha um resumo do pacote novamente.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  pacote /myNamespace/custom
   ação /myNamespace/custom/identity
  ```
  {: screen}

  É possível ver a ação `custom/identity` em seu namespace agora.

6. Chame a ação no pacote.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


É possível configurar parâmetros padrão para todas as entidades em um pacote. Faça isso configurando os parâmetros no nível do pacote herdados por todas as ações no pacote. Para saber como isso funciona, tente o exemplo a seguir:

1. Atualize o pacote `custom` com dois parâmetros: `city` e `country`.

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: pacote custom atualizado
  ```
  {: screen}

2. Exiba os parâmetros no pacote e na ação e veja como a ação `identity` no pacote herda os parâmetros do pacote.

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: pacote custom obtido, projetando parâmetros
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: ação custom/identity obtida, projetando parâmetros
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. Chame a ação identity sem quaisquer parâmetros para verificar se a ação realmente herda os parâmetros.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. Chame a ação identity com alguns parâmetros. Parâmetros de chamada são mesclados com os parâmetros do pacote; os parâmetros de chamada substituem os parâmetros do pacote.

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## Compartilhando um pacote
{: #openwhisk_packages_share}

Após as ações e os feeds que formam um pacote serem depuradas e testadas, o pacote pode ser compartilhado com todos os usuários do {{site.data.keyword.openwhisk_short}}. Compartilhar o pacote possibilita que os usuários liguem o pacote, chamem ações no pacote e criem regras do {{site.data.keyword.openwhisk_short}} e ações de sequência.

1. Compartilhe o pacote com todos os usuários:

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: pacote custom atualizado
  ```
  {: screen}

2. Exiba a propriedade `publish` do pacote para verificar se agora é true.

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: pacote custom obtido, projetando publish como verdadeiro
  ```
  {: screen}


Outros usuários agora podem usar seu pacote `custom`, incluindo ligação com o pacote ou chamando diretamente uma ação no mesmo. Outros usuários devem saber os nomes completos do pacote para ligá-lo ou chamar ações nele. Ações e feeds dentro de um pacote compartilhado são *public*. Se
o pacote for privado, então, todo o seu conteúdo também será privado.

1. Obtenha uma descrição do pacote para mostrar os nomes completos do pacote e da ação.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  pacote /myNamespace/custom
   ação /myNamespace/custom/identity
  ```
  {: screen}

  No exemplo anterior, você está trabalhando com o namespace `myNamespace` e esse namespace aparece no nome completo.

