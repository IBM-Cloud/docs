---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando e chamando ações do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}

*Última atualização: 22 de março de 2016*

Ações são fragmentos de código stateless executados na plataforma {{site.data.keyword.openwhisk}}. Uma ação pode ser uma função JavaScript, uma função Swift ou um programa executável customizado empacotado em um contêiner do Docker. Por exemplo, uma ação pode ser usada para detectar as faces em uma imagem, agregar um conjunto de chamadas de API ou postar um Tweet.
{:shortdesc}

As ações podem ser chamadas explicitamente ou executar em resposta a um evento. Em qualquer um dos casos, uma execução de uma ação resulta em um registro de ativação identificado por um ID exclusivo de ativação. A entrada para uma ação e o resultado de uma ação são um dicionário de pares de valores de chaves, em que a chave é uma sequência e o valor é um valor JSON válido.

As ações podem ser compostas por chamadas a outras ações ou uma sequência definida de ações.

## Criando e chamando ações JavaScript
{: #openwhisk_create_action_js}

As seções a seguir o orientam pelo trabalho com ações em JavaScript. Começando com a criação e a chamada de uma ação simples, você prosseguirá para a inclusão de parâmetros em uma ação e chamada dessa ação com parâmetros, configuração de parâmetros padrão e chamada dos mesmo, criação de ações assíncronas e, por fim, trabalho com sequências de ações.


### Criando e chamando uma ação simples JavaScript
{: #openwhisk_single_action_js}

Revise as etapas e os exemplos a seguir para criar sua primeira ação JavaScript.

1. Crie um arquivo JavaScript com o conteúdo a seguir. Para esse exemplo, o nome do arquivo é 'hello.js'.
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  O arquivo JavaScript pode conter funções adicionais. No entanto, por convenção, uma função chamada `main` deve existir para fornecer o ponto de entrada para a ação.

2. Crie uma ação a partir da função JavaScript a seguir. Para este exemplo, a ação é chamada 'hello'.

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: ação hello criada
  ```
  {: screen}

3. Liste as ações criadas:
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  ações
  hello       privada
  ```
  {: screen}

  É possível ver a ação `hello` que acabou de criar.

4. Após criar sua ação, será possível executá-la na nuvem no {{site.data.keyword.openwhisk_short}} com o comando 'invoke'. É possível chamar ações com uma chamada de *bloqueio* ou *sem bloqueio* especificando uma sinalização no comando. Uma chamada de bloqueio espera até que a ação ser executada até a conclusão e retorna um resultado. Este exemplo usa o parâmetro de bloqueio, `-blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: hello chamada com id 44794bd6aab74415b4e42a308d880e5b
  resposta:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  A saída de comando inclui duas informações importantes:
  * O ID de ativação (`44794bd6aab74415b4e42a308d880e5b`)
  * O resultado da chamada

  O resultado nesse caso é a sequência `Hello world` retornada pela função JavaScript. O ID de ativação pode ser usado para recuperar os logs ou o resultado da chamada em um momento futuro.  

5. Se você não precisar do resultado da ação imediatamente, será possível omitir a sinalização `--blocking` para fazer uma chamada sem bloqueio. É possível obter o resultado posteriormente usando o ID da ativação. Consulte o exemplo a seguir:

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: hello chamada com id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

6. Se esquecer de registrar o ID da ativação, será possível obter uma lista de ativações ordenadas da mais recente até a mais antiga. Execute o comando a seguir para obter uma lista de suas ativações:

  ```
  wsk activation list
  ```
  {: pre}
  ```
  ativações
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  {: screen}

### Passando parâmetros para uma ação
{: #openwhisk_adding_parameters_js}

Os parâmetros podem ser passados para a ação quando for chamada.

1. Use parâmetros na ação. Por exemplo, atualize o arquivo 'hello.js' com o conteúdo a seguir:
  
  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  Os parâmetros de entrada são passados como um parâmetro de objeto JSON para a função `main`. Observe como os parâmetros `name` e `place` são recuperados a partir do objeto `params` neste exemplo.

2. Atualize a ação `hello` e chame a ação, enquanto passa a ela os valores dos parâmetros `name` e `place`. Consulte o exemplo a seguir:
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Observe o uso da opção `--param` para especificar um nome e um valor de parâmetro e a opção `--result` para exibir somente o resultado da chamada.

### Configurando parâmetros padrão
{: #openwhisk_binding_actions}

Ações podem ser chamadas com vários parâmetros denominados. Lembre-se de que a ação `hello` do exemplo anterior espera dois parâmetros: *name* de uma pessoa e *place* de onde ela é.

Em vez de passar todos os parâmetros para uma ação toda vez, é possível fazer a ligação de determinados parâmetros. O exemplo a seguir liga o parâmetro *place* para que a ação use como padrão o local "Vermont":
 
1. Atualize a ação usando a opção `--param` para ligar os valores dos parâmetros.

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. Chame a ação, passando somente o parâmetro `name` desta vez.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Observe que você não precisou especificar o parâmetro place ao chamar a ação. Os parâmetros ligados ainda podem ser substituídos especificando o valor de parâmetro no momento da chamada.

3. Chame a ação, passando os valores `name` e `place`. O segundo sobrescreverá o valor ligado à ação.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### Criando ações assíncronas
{: #openwhisk_asynchrony_js}

As funções JavaScript que continuam a execução em uma função de retorno de chamada podem precisar retornar o resultado da ativação após a função `main` ter retornado. É possível realizar isso usando as funções `whisk.async()` e `whisk.done()` em sua ação.

1. Salve o conteúdo a seguir em um arquivo chamado `asyncAction.js`.

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  Observe que a função `main` retorna imediatamente e o valor de retorno `whisk.async()` indica que essa ativação deve continuar em execução.

  A função JavaScript `setTimeout()` neste caso espera 20 segundos antes de chamar a função de retorno de chamada, quando a chamada a `whisk.done()` indica que a ativação está concluída.

2. Execute os comandos a seguir para criar a ação e chamá-la:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

  Observe que você executou uma chamada de bloqueio de uma ação assíncrona.

3. Busque o log de ativação para ver quanto tempo a ativação levou para concluir:

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  ativações
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  Comparando os registros de data e hora `start` e `end` no registro de ativação, será possível ver que essa ativação levou um pouco mais de 20 segundos para ser concluída.


### Usando ações para chamar uma API externa
{: #openwhisk_apicall_action}

Os exemplos até agora de funções JavaScript autocontidas. Também é possível criar uma ação que chama uma API externa.

Este exemplo chama um serviço Yahoo Weather para obter as condições atuais em um local específico. 

1. Salvar o conteúdo a seguir em um arquivo chamado `weather.js`.
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  Observe que a ação no exemplo usa a biblioteca JavaScript `request` para fazer uma solicitação de HTTP à API do Yahoo Weather e extrai campos do resultado JSON. As [Referências](./openwhisk_reference.html#runtime_ref_runtime_environment) detalham os pacotes do Node.js que podem ser usados em suas ações.
  
  Este exemplo também mostra a necessidade de ações assíncronas. A ação retorna `whisk.async()` para indicar que o resultado dessa ação ainda não está disponível quando a função retorna. Em vez disso, o resultado está disponível no retorno de chamada `request` após a chamada HTTP ser concluída e é passado como um argumento para a função `whisk.done()`.

2. Execute os comandos a seguir para criar a ação e chamá-la:
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Criando sequências de ações
{: #openwhisk_create_action_sequence}

É possível criar uma ação que encadeia uma sequência de ações juntas.

Diversas ações do utilitário são fornecidas em um pacote chamado `/whisk.system/util` que pode ser usado para criar sua primeira sequência. É possível aprender mais sobre pacotes na seção [Pacotes](./openwhisk_packages.html).

1. Exiba as ações no pacote `/whisk.system/util`.
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  pacote /whisk.system/util
   ação /whisk.system/util/cat: concatenar matriz de sequências e dividir linhas em uma matriz
   ação /whisk.system/util/head: filtrar elementos da matriz do primeiro K e descartar o restante
   ação /whisk.system/util/date: obter data e hora atuais
   ação /whisk.system/util/sort: classificar matriz
  ```
  {: screen}

  As ações `cat` e `sort` serão usadas neste exemplo.

2. Crie uma sequência de ações de modo que o resultado de uma ação seja passado como um argumento para a próxima ação.
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  Essa sequência de ações converte algumas linhas de texto a uma matriz e classifica as linhas.

3. Antes de chamar a sequência de ações, crie um arquivo de texto chamado 'haiku.txt' com algumas linhas de texto:

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. Chame a ação:
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  No resultado, você vê que as linhas estão classificadas.

**Nota**: para obter mais informações sobre chamada de sequências de ações com vários parâmetros denominados, consulte [Configurando parâmetros padrão](./openwhisk_actions.html##openwhisk_binding_actions)

## Criando ações Swift
{: #openwhisk_actions_swift}

O processo de criação de ações Swift é semelhante ao de ações JavaScript. As seções a seguir o guiam pela criação e chamada de uma única ação swift e a inclusão de parâmetros nessa ação.

Também é possível usar o [Ambiente de simulação do Swift ](https://swiftlang.ng.bluemix.net) para testar seu código Swift sem precisar instalar o Xcode em sua máquina.

### Criando e chamando uma ação
{: #openwhisk_actions_invoke_swift}

Uma ação é simplesmente uma função Swift de nível superior. Por exemplo, crie um arquivo chamado `hello.swift` com o conteúdo a seguir:

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
          return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

Observe que assim como ações JavaScript, as ações Swift sempre consomem um dicionário e produzem um dicionário.

É possível criar uma ação do {{site.data.keyword.openwhisk_short}} chamada `helloSwift` a partir desta função da seguinte forma:

```
wsk action create helloSwift hello.swift
```
{: pre}

Ao usar a linha de comandos e um arquivo de origem `.swift`, não será necessário especificar que você está criando uma ação Swift (como ocorre em uma ação JavaScript); a ferramenta determina isso a partir da extensão do arquivo.

A chamada da ação é a mesma para as ações Swift que das ações JavaScript:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**Atenção:** as ações Swift são executadas em um ambiente Linux. Swift no Linux ainda está em desenvolvimento e o {{site.data.keyword.openwhisk_short}} geralmente usa a liberação mais recente disponível, que não está necessariamente estável. Além disso, a versão do Swift usada com o {{site.data.keyword.openwhisk_short}} pode estar inconsistente com versões do Swift de liberações estáveis do XCode no MacOS.

## Criando ações Docker
{: #openwhisk_actions_docker}

Com as ações Docker do {{site.data.keyword.openwhisk_short}}, é possível escrever suas ações em qualquer linguagem.

Seu código é compilado em um binário executável e integrado a uma imagem do Docker. O programa binário interage com o sistema aceitando entrada de `stdin` e respondendo por meio de `stdout`.

Como um pré-requisito, deve-se ter uma conta do Docker Hub.  Para configurar um ID e uma conta do Docker grátis, acesse o [Docker Hub](https://hub.docker.com){: new_window}.

Para as instruções a seguir, suponha que o ID do usuário seja "janesmith" e a senha seja "janes_password".  Supondo que a CLI já tenha sido configurada, três etapas são necessárias para configurar um binário customizado para ser usado pelo {{site.data.keyword.openwhisk_short}}.  Depois disso, a imagem do Docker transferida por upload poderá ser usada como uma ação.

1. Faça download da estrutura básica do Docker. É possível fazer download da mesma usando a CLI da seguinte forma:

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  A estrutura básica do Docker agora está instalada no diretório atual.
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  A estrutura básica é um modelo do contêiner do Docker no qual é possível injetar seu código na forma de binários customizados.

2. Configure seu binário customizado na estrutura básica da caixa preta. A estrutura básica já inclui um programa C que pode ser usado.

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  É possível modificar esse arquivo conforme necessário.

3. Construa a imagem do Docker e faça upload da mesma usando um script fornecido. Deve-se primeiro executar `docker login` para autenticação e, em seguida, executar o script com um nome de imagem escolhido.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  Observe que parte do arquivo example.c é compilada como parte do processo de construção da imagem do Docker, portanto, você não precisa de C compilado em sua máquina.

4. Para criar uma ação a partir de uma imagem do Docker em vez de um arquivo JavaScript fornecido, inclua `--docker` e substitua o nome do arquivo JavaScript pelo nome da imagem do Docker.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


É possível localizar mais informações sobre como criar ações Docker na seção [Referências](./openwhisk_reference.html#openwhisk_ref_docker).


## Observando a saída da ação
{: #openwhisk_actions_polling}

As ações do {{site.data.keyword.openwhisk_short}} podem ser chamadas por outros usuários em resposta a vários eventos ou como parte de uma sequência de ações. Nesses casos, pode ser útil monitorar as chamadas.

É possível usar a CLI do {{site.data.keyword.openwhisk_short}} para observar a saída de ações à medida que são chamadas.

1. Emita o comando a seguir a partir de um shell:
  ```
  wsk activation poll
  ```
  {: pre}

  Esse comando inicia um loop de pesquisa que verifica continuamente logs de ativações.

2. Alterne para outra janela e chame uma ação:

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: /whisk.system/samples/helloWorld chamada com id 7331f9b9e2044d85afd219b12c0f1491
  ```
  {: screen}

3. Observe o log de ativação na janela de pesquisa:

  ```
  Ativação: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  Da forma semelhante, sempre que você executar o utilitário de pesquisa, verá em tempo real os logs para quaisquer ações em execução em seu nome no {{site.data.keyword.openwhisk_short}}.

## Excluindo Ações
{: #openwhisk_delete_action}

É possível limpar excluindo ações que você não deseja usar.

1. Execute o comando a seguir para excluir uma ação:
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```
  {: screen}

2. Verifique se a ação não aparece mais na lista de ações.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
