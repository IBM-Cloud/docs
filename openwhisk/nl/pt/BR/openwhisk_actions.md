---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Criando e chamando ações do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}


Ações são fragmentos de código stateless executados na plataforma {{site.data.keyword.openwhisk}}. Uma ação pode ser gravada como uma função JavaScript, Swift ou Python, um método Java ou um programa executável customizado empacotado em um contêiner do Docker. Por exemplo, uma ação pode ser usada para detectar as faces em uma imagem, responder a uma mudança do banco de dados, agregar um conjunto de chamadas API ou postar um Tweet.
{:shortdesc}
As ações podem ser chamadas explicitamente ou executar em resposta a um evento. Em qualquer um dos casos, cada execução de uma ação resulta em um registro de ativação identificado por um ID de ativação exclusivo. A entrada para uma ação e o resultado de uma ação são um dicionário de pares de valores de chaves, em que a chave é uma sequência e o valor é um valor JSON válido. As ações também podem ser compostas por chamadas a outras ações ou uma sequência definida de ações.

Aprenda como criar, chamar e depurar ações em seu ambiente de desenvolvimento preferencial:
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)

Além disso, saiba mais sobre:

* [Observando a saída da ação](#openwhisk_actions_polling)
* [Listando ações](#openwhisk_listing_actions)
* [Excluindo Ações](#openwhisk_delete_action)
* [Acessando metadados de ação dentro do corpo de ação](#openwhisk_action_metadata)


## Criando e chamando ações JavaScript
{: #openwhisk_create_action_js}

As seções a seguir o orientam pelo trabalho com ações em JavaScript. Você começa com a criação e a chamada de uma ação simples. Em seguida, move para a inclusão de parâmetros em uma ação e a chamada dessa ação com os parâmetros. Em seguida, está configurando parâmetros padrão e chamando-os. Em seguida, você cria ações assíncronas e, por fim, trabalha com sequências de ações.


### Criando e chamando uma ação simples JavaScript
{: #openwhisk_single_action_js}

Revise as etapas e os exemplos a seguir para criar sua primeira ação JavaScript.

1. Crie um arquivo JavaScript com o conteúdo a seguir. Para esse exemplo, o nome do arquivo é 'hello.js'.

  ```javascript
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

3. Liste as ações que você criou:

  ```
  wsk action list
  ```
  {: pre}
  ```
  ações
  hello       privada
  ```

  É possível ver a ação `hello` que acabou de criar.

4. Após você criar a sua ação, será possível executá-la na nuvem no OpenWhisk com o comando 'invoke'. É possível chamar ações com uma chamada de *bloqueio* (ou seja, estilo de solicitação/resposta) ou uma chamada de *não bloqueio* especificando uma sinalização no comando. Uma solicitação de chamada de bloqueio irá *esperar* que o resultado de ativação fique disponível. O período de espera é o menor dentre 60 segundos ou o [limite de tempo](./openwhisk_reference.html#openwhisk_syslimits) configurado da ação. O resultado da ativação será retornado se ele estiver disponível dentro do período de espera. Caso contrário, a ativação continuará o processamento no sistema e um ID de ativação será retornado para seja possível verificar o resultado posteriormente, como com solicitações de não bloqueio (consulte [aqui](#openwhisk_actions_polling) para obter dicas sobre ativações de monitoramento).

  Este exemplo usa o parâmetro de bloqueio, `--blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
    ```
  ```json
     {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```

  A saída de comando inclui duas informações importantes:
  * O ID de ativação (`44794bd6aab74415b4e42a308d880e5b`)
  * O resultado da chamada se ele estiver disponível dentro do período de espera estimado

  O resultado nesse caso é a sequência `Hello world` retornada pela função JavaScript. O ID de ativação pode ser usado para recuperar os logs ou o resultado da chamada em um momento futuro.  

5. Se você não precisar do resultado da ação imediatamente, será possível omitir a sinalização `--blocking` para fazer uma chamada sem bloqueio. É possível obter o resultado posteriormente usando o ID da ativação. Consulte o exemplo a seguir:
  
  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: hello chamada com id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
     {
      "payload": "Hello world"
  }
  ```

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
  

### Passando parâmetros para uma ação
{: #openwhisk_adding_parameters_js}

Os parâmetros podem ser passados para a ação quando for chamada.

1. Use parâmetros na ação. Por exemplo, atualize o arquivo 'hello.js' com o conteúdo a seguir:

  ```javascript
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

3.  Os parâmetros podem ser fornecidos explicitamente na linha de comandos ou fornecendo um arquivo contendo os parâmetros desejados

  Para passar os parâmetros diretamente pela linha de comandos, forneça um par de chave/valor para a sinalização `--param`:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  Para usar um arquivo contendo o conteúdo de parâmetro, crie um arquivo contendo os parâmetros no formato JSON. O
  nome do arquivo deve então ser passado para a sinalização `param-file`:

  Exemplo de arquivo de parâmetro chamado parameters.json:
  ```json
     {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
     {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  Observe o uso da opção `--result` para exibir somente o resultado da chamada.

### Configurando parâmetros padrão
{: #openwhisk_binding_actions}

Ações podem ser chamadas com vários parâmetros denominados. Lembre-se de que a ação `hello` do exemplo anterior espera dois parâmetros: *name* de uma pessoa e *place* de onde ela é.

Em vez de passar todos os parâmetros para uma ação toda vez, é possível fazer a ligação de determinados parâmetros. O exemplo a seguir liga o parâmetro *place* para que a ação use como padrão o local "Vermont":

1. Atualize a ação usando a opção `--param` para ligar os valores de parâmetros ou passando um arquivo que contenha os parâmetros para `--param-file`

  Para especificar os parâmetros padrão explicitamente na linha de comandos, forneça um par de chave/valor para a sinalização `param`:

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  Passar os parâmetros a partir de um arquivo requer a criação de um arquivo contendo o conteúdo desejado no formato JSON.
  O nome do arquivo deve então ser passado para a sinalização `-param-file`:

  Exemplo de arquivo de parâmetro chamado parameters.json:
  ```json
     {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. Chame a ação, passando somente o parâmetro `name` desta vez.

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```json
     {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  Observe que você não precisou especificar o parâmetro place quando chamou a ação. Os parâmetros ligados ainda podem ser substituídos especificando o valor de parâmetro no momento da chamada.

3. Chame a ação, passando os valores `name` e `place`. O último sobrescreve o valor que está ligado à ação.

  Usando a sinalização `--param`:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}
  Usando a sinalização `--param-file`:
  arquivo parameters.json:
  ```json
     {
    "name": "Bernie",
    "place": "Vermont"
  }
  ```
  {: codeblock}  
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  ```json
     {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```

### Criando ações assíncronas
{: #openwhisk_asynchrony_js}

As funções JavaScript que são executadas de forma assíncrona podem precisar retornar o resultado da ativação após a função `main` ter retornado. É possível fazer isso retornando uma Promessa em sua ação.

1. Salve o conteúdo a seguir em um arquivo chamado `asyncAction.js`.

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  Observe que a função `main` retorna uma Promessa, que indica que a ativação não foi concluída ainda, mas espera-se que seja no futuro.

  A função JavaScript `setTimeout()` nesse caso aguarda dois segundos antes de chamar a função de retorno de chamada.  Isso representa o código assíncrono e vai dentro da função de retorno de chamada da Promessa.

  O retorno de chamada da Promessa aceita dois argumentos, resolver e rejeitar, que são ambos funções.  A chamada para `resolve ()` cumpre a Promessa e indica que a ativação foi concluída normalmente.

  Uma chamada para `reject()` pode ser usada para rejeitar a Promessa e sinalizar que a ativação foi concluída de forma anormal.

2. Execute os comandos a seguir para criar a ação e chamá-la:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
     {
      "done": true
  }
  ```
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

  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
  ```json
     {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```
  Comparando os registros de data e hora de `start` e de `end` no registro de ativação, será possível ver que essa ativação levou um pouco mais de dois segundos para ser concluída.


### Usando ações para chamar uma API externa
{: #openwhisk_apicall_action}

Os exemplos até agora de funções JavaScript autocontidas. Também é possível criar uma ação que chama uma API externa.

Este exemplo chama um serviço Yahoo Weather para obter as condições atuais em um local específico.

1. Salvar o conteúdo a seguir em um arquivo chamado `weather.js`.

  ```javascript
  var request = require('request');

  function main(params) {
      var location = params.location || 'Vermont';
      var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if (error) {
                  reject(error);
              }
              else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                  var text = condition.text;
                  var temperature = condition.temp;
                  var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                  resolve({msg: output});
              }
          });
      });
  }
  ```
  {: codeblock}

  Observe que a ação no exemplo usa a biblioteca JavaScript `request` para fazer uma solicitação de HTTP à API do Yahoo Weather e extrai campos do resultado JSON. As [Referências](./openwhisk_reference.html#openwhisk_ref_javascript_environments) detalham os pacotes do Node.js que podem ser usados em suas ações.

  Este exemplo também mostra a necessidade de ações assíncronas. A ação retorna uma Promessa para indicar que o resultado dessa ação não está disponível ainda quando a função é retornada. Em vez disso, o resultado está disponível no retorno de chamada `request` após a chamada HTTP ser concluída e é passado como um argumento para a função `resolve()`.

2. Execute os comandos a seguir para criar a ação e chamá-la:

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```json
     {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```


### Empacotamento de uma ação como um módulo Node.js
{: #openwhisk_js_packaged_action}

Como uma alternativa para gravar todo o seu código de ação em um único arquivo de origem JavaScript, é possível gravar uma ação como um pacote `npm`. Considere como um exemplo um diretório com os seguintes arquivos:

Primeiro, `package.json`:

```json
     {
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

Então, `index.js`:

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

Observe que a ação é exposta por meio de `exports.main`; o próprio manipulador de ações pode ter qualquer nome, contanto que se adeque à assinatura usual de aceitação e retorno de um objeto (ou uma `Promessa` de objeto). De acordo com a convenção Node.js, deve-se nomear esse arquivo `index.js` ou especificar
o nome do arquivo que você preferir como a propriedade `main` no package.json.

Para criar uma ação do OpenWhisk a partir deste pacote:

1. Instale primeiro todas as dependências localmente

  ```
  npm install
  ```
  {: pre}

2. Crie um archive `.zip` contendo todos os arquivos (incluindo todas as dependências):

  ```
  zip -r action.zip *
  ```
  {: pre}

    > Observe: usar a ação do Windows Explorer para criar o arquivo zip resultará em uma estrutura incorreta. As ações zip do OpenWhisk deverão ter o `package.json` na raiz do zip, enquanto o Windows Explorer o colocará dentro de uma pasta aninhada. A opção mais segura é usar o comando `zip` da linha de comandos, conforme mostrado acima.


3. Crie a ação:

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  Observe que ao criar uma ação a partir de um archive `.zip` usando a ferramenta CLI, deve-se fornecer explicitamente um valor para o sinalizador `--kind`.

4. É possível chamar a ação como qualquer outra:

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```json
     {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```


Finalmente, observe que enquanto a maioria dos pacotes `npm` instala fontes JavaScript em `npm install`, alguns também instalam e compilam os artefatos binários. O upload do archive atualmente não suporta dependências binárias, mas apenas as dependências JavaScript. As chamadas de ação poderão falhar se o archive incluir dependências binárias.

## Criando sequências de ações
{: #openwhisk_create_action_sequence}

É possível criar uma ação que encadeia uma sequência de ações juntas.

Várias ações do utilitário são fornecidas em um pacote chamado `/whisk.system/utils` que pode ser usado para criar a sua primeira sequência. É possível aprender mais sobre pacotes na seção [Pacotes](./openwhisk_packages.html).

1. Exiba as ações no pacote `/whisk.system/utils`.

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: construindo blocos que formatam e montam dados
   action /whisk.system/utils/head: extrair prefixo de uma matriz
   action /whisk.system/utils/split: dividir uma sequência em uma matriz
   action /whisk.system/utils/sort: classifica uma matriz
   action /whisk.system/utils/echo: retorna a entrada
   action /whisk.system/utils/date: data e hora atual
   action /whisk.system/utils/cat: concatena a entrada em uma sequência
  ```


  Você estará usando as ações `split` e `sort` neste exemplo.

2. Crie uma sequência de ações de modo que o resultado de uma ação seja passado como um argumento para a próxima ação.

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  Essa sequência de ações converte algumas linhas de texto a uma matriz e classifica as linhas.

3. Chame a ação:

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
  ```
  {: pre}
  ```json
     {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```


  No resultado, você vê que as linhas estão classificadas.

**Nota**: parâmetros transmitidos entre as ações na sequência são explícitos, exceto parâmetros padrão.
Portanto, parâmetros que são transmitidos para a sequência de ações estão disponíveis apenas para a primeira ação na sequência.
O resultado da primeira ação na sequência torna-se o objeto JSON de entrada para a segunda ação na sequência (e assim por diante).
Esse objeto não inclui nenhum dos parâmetros originalmente transmitidos para a sequência, a menos que a primeira ação os inclua explicitamente em seu resultado.
Os parâmetros de entrada para uma ação são mesclados com os parâmetros padrão da ação, com o antigo tendo precedência e substituindo qualquer parâmetro padrão correspondente.
Para obter mais informações sobre como chamar sequências de ações com múltiplos parâmetros nomeados, consulte [Configurando parâmetros padrão](./openwhisk_actions.html#openwhisk_binding_actions).

## Criando ações Python
{: #openwhisk_actions_python}

O processo de criação de ações Python é semelhante ao de ações JavaScript. As seções a seguir orientam você na criação e chamada de uma única ação Python e na inclusão de parâmetros nessa ação.

### Criando e chamando uma ação
{: #openwhisk_actions_python_invoke}

Uma ação é simplesmente uma função Python de nível superior, o que significa que é necessário ter um método chamado `principal`. Por exemplo, crie um
arquivo chamado `hello.py` com o conteúdo a seguir:

```python
def main(dict):
    name = dict.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
    return {"greeting": greeting}
```
{: codeblock}

As ações Python sempre consomem e produzem um dicionário.

É possível criar uma ação OpenWhisk chamada `helloPython` a partir
dessa função da seguinte forma:

```
wsk action create helloPython hello.py
```
{: pre}

Ao usar a linha de comandos e um arquivo de origem `.py`, não será
necessário especificar que você está criando uma ação Python (como ocorre em uma ação
JavaScript); a ferramenta determina isso a partir da extensão do arquivo.

A chamada da ação é a mesma para ações do Python que é para ações do JavaScript:

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
     {
      "greeting": "Hello World!"
  }
```



## Criando ações Swift
{: #openwhisk_actions_swift}

O processo de criação de ações Swift é semelhante ao de ações JavaScript. As seções a seguir o guiam pela criação e chamada de uma única ação swift e a inclusão de parâmetros nessa ação.

Também é possível usar o [Ambiente de simulação do Swift ](https://swiftlang.ng.bluemix.net) para testar seu código Swift sem precisar instalar o Xcode em sua máquina.

### Criando e chamando uma ação
{: #openwhisk_actions_invoke_swift}

Uma ação é simplesmente uma função Swift de nível superior. Por exemplo, crie um arquivo chamado
`hello.swift` com o conteúdo a seguir:

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
        return [ "greeting" : "Hello \(name)!" ]
    } else {
        return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

As ações swift sempre consomem um dicionário e produzem um dicionário.

É possível criar uma ação do {{site.data.keyword.openwhisk_short}} chamada `helloSwift` a partir desta função da seguinte
forma:

```
wsk action create helloSwift hello.swift
```
{: pre}

Ao usar a linha de comandos e um arquivo de origem `.swift`, não
será necessário especificar que você está criando uma ação Swift (como ocorre em uma ação
JavaScript); a ferramenta determina isso a partir da extensão do arquivo.

A chamada da ação é a mesma para as ações Swift que das ações JavaScript:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
     {
      "greeting": "Hello World!"
  }
```


**Atenção:** as ações Swift são executadas em um ambiente Linux. Swift no Linux ainda está em desenvolvimento
e o {{site.data.keyword.openwhisk_short}} geralmente usa a liberação mais recente disponível, que não está necessariamente estável. Além disso, a versão do Swift usada com o {{site.data.keyword.openwhisk_short}} pode estar inconsistente com versões do Swift de liberações estáveis do XCode no MacOS.

### Empacotando uma ação como um executável do Swift
{: #openwhisk_actions_swift_zip}
Ao criar uma ação do Swift do OpenWhisk com um arquivo de origem do Swift, ele precisa ser compilado em um binário antes de a ação ser executada. Depois de isso ser feito, as chamadas subsequentes para a ação serão muito mais rápidas até que o contêiner que está mantendo sua ação seja limpo.

Para evitar o atraso da etapa de compilação, será possível compilar seu arquivo Swift em um binário e, em seguida, fazer upload dele para o OpenWhisk em um arquivo zip. Uma vez que o andaime do OpenWhisk será necessária, a maneira mais fácil de criar o binário será construí-lo no mesmo ambiente em que será executado. Estas são as etapas:

- Execute um contêiner interativo da ação do Swift.
  ```
  docker run -it -v "$(pwd):/owexec" openwhisk/swift3action bash
  ```
  {: pre}
Isso o coloca em um shell bash dentro do contêiner do Docker. Execute os comandos a seguir dentro dele:
  
- Instale o zip por conveniência, para empacotar o binário
  ```
  apt-get install -y zip
  ```
  {: pre}
- Copie o código-fonte e prepare para construí-lo
  ```
  cp /owexec/hello.swift /swift3Action/spm-build/main.swift 
  ```
  {: pre}
  ```
  cat /swift3Action/epilogue.swift >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
  ```
  echo '_run_main(mainFunction:main)' >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
- zBuild e link
  ```
  /swift3Action/spm-build/swiftbuildandlink.sh
  ```
  {: pre}
- Crie o archive zip:
  ```
  cd /swift3Action/spm-build
  ```
  {: pre}
  ```
  zip /owexec/hello.zip .build/release/Action
  ```
- Saia do contêiner do Docker
  ```
  exit
  ```
  {: pre}
Isso criou hello.zip no mesmo diretório que hello.swift. -Faça upload dele para o OpenWhisk com o nome de ação helloSwifty:
  ```
  wsk action update helloSwiftly hello.zip --kind swift:3
  ```
  {: pre}
- Para verificar o quanto ele é mais rápido, execute 
  ```
  wsk action invoke helloSwiftly --blocking
  ``` 
  {: pre}


## Criando ações Java
{: #openwhisk_actions_java}

O processo de criação de ações Java é semelhante ao de ações JavaScript e Swift. As seções a seguir orientam você na criação e chamada de uma única ação Java e na inclusão de parâmetros nessa ação.

Para compilar, testar e arquivar os arquivos Java, deve-se ter um [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) instalado localmente.

### Criando e chamando uma ação
{: #openwhisk_actions_java_invoke}

Uma ação Java é um programa Java com um método chamado `main` que tem a assinatura exata conforme a seguir:
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

Por exemplo, crie um arquivo Java chamado `Hello.java` com o conteúdo a seguir:

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

Em seguida, compile `Hello.java` em um arquivo JAR `hello.jar` conforme a seguir:
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**Nota:** [google-gson](https://github.com/google/gson) deve existir em seu CLASSPATH Java ao compilar o arquivo Java.

É possível criar uma ação OpenWhisk chamada `helloJava` a partir desse arquivo JAR conforme
a seguir:

```
wsk action create helloJava hello.jar --main Hello
```
{: pre}

Ao usar a linha de comandos e um arquivo de origem `.jar`, não é necessário
especificar que você está criando uma ação Java;
a ferramenta determina isso a partir da extensão do arquivo.

É necessário especificar o nome da classe principal usando `--main`. Uma classe principal
elegível é aquela que implementa um método `main` estático, conforme descrito acima. Se a
classe não estiver no pacote padrão, use o nome de classe completo Java,
por exemplo, `--main com.example.MyMain`.

A chamada de ação para as ações Java é a mesma que para as ações Swift e JavaScript:

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
     {
      "greeting": "Hello World!"
  }
```

## Criando ações Docker
{: #openwhisk_actions_docker}

Com as ações Docker do {{site.data.keyword.openwhisk_short}}, é possível escrever suas ações em qualquer linguagem.

O seu código é compilado em um binário executável e integrado em uma imagem do Docker. O programa binário interage com o sistema aceitando entrada de `stdin` e respondendo por meio de `stdout`.

Como um pré-requisito, deve-se ter uma conta do Docker Hub.  Para configurar um ID e uma conta do Docker grátis, acesse o [Docker Hub](https://hub.docker.com){: new_window}.

Para as instruções a seguir, suponha que o ID do usuário do Docker seja `janesmith` e a senha seja `janes_password`.  Supondo que a CLI já esteja configurada, três etapas serão necessárias para configurar um binário customizado para uso pelo {{site.data.keyword.openwhisk_short}}. Depois disso, a imagem do Docker transferida por upload poderá ser usada como uma ação.

1. Faça download da estrutura básica do Docker. É possível fazer download da mesma usando a CLI da seguinte forma:

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  A estrutura básica do Docker agora está instalada no diretório atual.
  ```
  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```
  A estrutura básica é um modelo do contêiner do Docker no qual é possível injetar seu código na forma de binários customizados.

2. Configure seu binário customizado na estrutura básica da caixa preta. A estrutura básica já inclui um programa C que pode ser usado.

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
      printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  É possível modificar esse arquivo conforme necessário ou incluir código e dependências adicionais na imagem do Docker.
  No caso do último, pode ser necessário ajustar o `Dockerfile` conforme necessário para construir o executável.
  O binário deve estar localizado dentro do contêiner em `/action/exec`.

  O executável recebe um único argumento a partir da linha de comandos. Ele é uma serialização de sequência do objeto
  JSON que representa os argumentos para a ação. O programa pode efetuar log em `stdout` ou em `stderr`.
  Por convenção, a última linha de saída *deve* ser um objeto JSON em sequência que representa o resultado da ação.

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

  Observe que parte do arquivo example.c é compilada como parte do processo de construção da imagem do Docker, de modo que você não precisa de C compilado em sua máquina.
  Na verdade, a menos que você esteja compilando o binário em uma máquina host compatível, ele pode não ser executado dentro do contêiner pois os formatos não irão corresponder.

  O seu contêiner do Docker agora pode ser usado como uma ação do {{site.data.keyword.openwhisk_short}}.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}

  Observe o uso de `--docker` ao criar uma ação. Atualmente, todas as imagens do Docker são consideradas como hospedadas no Docker Hub.
  A ação pode ser chamada como qualquer outra ação do {{site.data.keyword.openwhisk_short}}.

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
     {
      "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```

  Para atualizar a ação do Docker, execute buildAndPush.sh para fazer upload da imagem mais recente do Docker Hub. Isso permitirá que o sistema extraia a sua nova imagem do Docker da próxima vez que ele executar o código para sua ação.
  Se não houver nenhum contêiner quente, qualquer chamada nova usará a nova imagem do Docker.
  No entanto, se houver um contêiner quente usando uma versão anterior de sua imagem do Docker, qualquer chamada nova continuará usando essa imagem, a menos que você execute `wsk action update`. Isso indicará ao sistema que, para novas chamadas, ele deve executar um docker pull para obter sua nova imagem do Docker.

  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}

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

3. Observe o log de ativação na janela de pesquisa:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

  Da mesma forma, sempre que executar o utilitário de pesquisa, você verá em tempo real os logs de quaisquer ações em execução em seu nome no OpenWhisk.


## Listando Ações
{: #openwhisk_listing_actions}

É possível listar todas as ações criadas, usando:

```
wsk action list
```
{: pre}

Conforme você gravar mais ações, essa lista ficará mais longa e poderá ser útil para agrupar ações relacionadas nos [pacotes](./packages.md). Para filtrar sua lista de ações apenas àquelas de um pacote específico, será possível usar: 

```
wsk action list [PACKAGE NAME]
```
{: pre}


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

2. Verifique se a ação não aparece mais na lista de ações.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}

## Acessando metadados de ação dentro do corpo de ação
{: #openwhisk_action_metadata}

O ambiente de ação contém várias propriedades que são específicas da ação em execução.
Elas permitem que a ação trabalhe programaticamente com ativos do OpenWhisk por meio da API de REST
ou configure um alarme interno quando a ação estiver prestes a esgotar seu orçamento de tempo atribuído.
As propriedades são acessíveis por meio do ambiente do sistema a todos os tempos de execução suportados:
ações do Node.js, Python, Swift, Java e Docker ao usar a estrutura básica do OpenWhisk Docker.

* `__OW_API_HOST` o host da API para a implementação do OpenWhisk que executa esta ação
* `__OW_API_KEY` a chave API para o assunto que chama a ação, essa chave pode ser uma chave API restrita
* `__OW_NAMESPACE` o namespace para a *ativação* (este não pode ser o mesmo namespace que para a ação)
* `__OW_ACTION_NAME` o nome completo da ação em execução
* `__OW_ACTIVATION_ID` o ID de ativação para esta instância de ação em execução
* `__OW_DEADLINE` o tempo aproximado quando essa ação terá consumido toda sua cota de duração (medido em milissegundos de época)
