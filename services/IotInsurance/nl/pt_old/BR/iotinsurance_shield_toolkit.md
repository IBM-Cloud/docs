---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Kit de ferramentas de blindagem
{: #iot4i_shield_toolkit}
Use blindagens para proteger a propriedade e os usuários por meio da identificação de riscos
e da criação de respostas automatizadas apropriadas. Use ou modifique as blindagens que estão incluídas na biblioteca de blindagens do {{site.data.keyword.iotinsurance_short}} ou crie e implemente suas próprias blindagens usando as instruções e os exemplos a seguir.{:shortdesc}

## Sobre as blindagens.
Uma blindagem é um conjunto de regras e ações definidas que podem ser acionadas por condições específicas na entrada que é recebida de um sensor. Por exemplo, é possível criar uma blindagem com uma regra para o envio de uma mensagem de texto sempre que o sensor detectar um vazamento de água.

## Usando blindagens da biblioteca de blindagens do
{{site.data.keyword.iotinsurance_short}}

É possível localizar uma ampla variedade de blindagens predefinidas na [biblioteca de blindagens do {{site.data.keyword.iotinsurance_short}} ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}. Visualize o arquivo LEIA-ME no site para obter instruções para fazer download e começar a usar
as blindagens.

## Criando sua própria blindagem
Este exemplo mostra como configurar seu ambiente, definir uma blindagem,
criar um usuário e, em seguida, associar a blindagem ao usuário.  É possível também criar
promoções e riscos simulados.  

Amostras de código para criar uma blindagem simples para vazamentos de água são
mostradas nas seções a seguir. Um conjunto completo de código de exemplo está disponível
no [Diretório do
GitHub iot4i-api-examples-nodejs](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/).

### Pré-requisitos
Antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:

- [Node.js](https://nodejs.org/en/) instalado no computador.  
- Um ambiente de tempo de execução ativado para Node.js, como o Eclipse.
- Software Git e acesso ao [Repositório de código-fonte GitHub para os exemplos de API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Como alternativa, é possível fazer download do [archive com os arquivos de código-fonte](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Código-fonte preparado.  
  Para preparar o código-fonte, conclua estas etapas:
  1. Clone ou faça download do [Repositório de código-fonte GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) para seu computador.
  2. Instale os pré-requisitos de software livre do projeto usando uma linha de comandos para acessar a pasta que contém os arquivos de código-fonte clonados e executando o comando `npm install`.

### Configurando o Ambiente
{: #environment}
Para configurar seu ambiente para enviar chamadas de API REST, deve-se configurar a URL
para a API no arquivo config.js. A URL do agregador pode ser ignorada nesse contexto.

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### Criando uma definição de blindagem
{: #create_shield_def}

Método: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Crie uma definição de blindagem no arquivo createShield.js.  O exemplo a seguir
mostra uma blindagem simples que detecta um vazamento de água.

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

em
que:
- **UUID** - O identificador exclusivo universal (UUID) da blindagem.
- **actions** - Uma lista de ações que são acionadas quando um risco é criado. Nesse exemplo, informações sobre o risco são enviadas para o app do usuário utilizando uma notificação push do iOS.

### Criando um código de blindagem
{: #create_shield_code}
Crie um código de blindagem no arquivo shieldCode.js para definir como o mecanismo de blindagem processa uma carga útil.

O exemplo a seguir mostra um código de blindagem que pode ser usado para processar uma carga útil de vazamento de água para a blindagem que foi mostrada nos exemplos anteriores.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Cada código de blindagem contém recursos que são definidos em instruções resource/shield.js. Cada um dos recursos a seguir inclui um exemplo que pode ser usado com a blindagem, a carga útil e o usuário que são mostrados nos exemplos anteriores.

  - Nome da blindagem  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Atraso de blindagem - o atraso em milissegundos entre os riscos.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - Identificador exclusivo universal (UUID) da blindagem  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Condição de entrada - a condição e os atributos que são necessários para que o mecanismo de blindagem processe a carga útil. No exemplo, a condição é que a carga útil deve conter o atributo **liquid_detected**.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - o núcleo da blindagem que calcula e executa um algoritmo para determinar se um risco está presente. No exemplo a seguir, o único atributo necessário é **liquid_detected**, mas safelets podem ser usados para definir algoritmos complexos.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Mensagem - a mensagem que será enviada ao usuário se o risco for processado.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Execução de blindagem - a função que é usada para executar a blindagem
diretamente, em vez de esperar que o mecanismo de blindagem execute todas as blindagens
relevantes automaticamente.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Registrar blindagem - uma função predefinida que deve ser chamada no código de
blindagem para registrar a blindagem no mecanismo de blindagem. O valor
**undefined** no exemplo representa a função de pré-processamento, que
não é necessária nesse exemplo específico. Em algumas blindagens, a função de
pré-processamento pode ser usada para reorganizar os dados na carga útil. Por exemplo, se
leituras de temperatura forem relatadas em Fahrenheit e o safelet requerer Celsius, a função
de pré-processamento poderá ser usada para converter as temperaturas para o valor necessário.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Criando um usuário
{: #create_user}

Método: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Crie um usuário no arquivo createUser.js. O exemplo a seguir mostra como criar um único usuário.

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

em
que:
- **username** - A chave exclusiva para o usuário que é utilizado para identificar cada entidade que é associada ao usuário, como dispositivos, blindagens e promoções.
- **password** - Somente o hash da senha é armazenado no banco de dados.
- **DeviceId** - O identificador que é usado para registrar o usuário no {{site.data.keyword.iot_full}}. O valor é o mesmo que o do username.
- **accessLevel** - O valor define os terminais de API que o usuário pode acessar:
  - 100 - app móvel
  - 10 - painel
  - 1 - administrador do sistema

### Criando uma associação de blindagem
{: #create_shield_assoc}

Método: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Crie uma associação de blindagem que vincule a blindagem ao usuário no createUserShieldAssociation.js.

O exemplo a seguir mostra uma associação de blindagem para a blindagem e o usuário que foram criados nas seções anteriores.

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Criando um risco simulado
{: #create_sim_hazard}

Método: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

É possível criar uma carga útil de risco simulado para testar suas blindagens.

O exemplo a seguir mostra como criar uma carga útil que ativa a blindagem que foi
criada no exemplo anterior e envia um alerta para o usuário associado.

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### Criando uma Promoção
{: #create_promotion}

O {{site.data.keyword.iotinsurance_short}} pode enviar promoções para o proprietário
usando o app móvel. Crie promoções usando o arquivo createPromotion.js.

O exemplo a seguir mostra como criar uma promoção para um encanador autorizado.

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

É possível implementar seu app móvel e usar [as instruções no repositório do GitHub ioti-mobile](https://github.com/ibm-watson-iot/ioti-mobile) para conectar como o usuário criado na seção anterior.

# Links Relacionados
{: #rellinks}

## Referência de API
{: #api}
* [API do {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Links Relacionados
{: #general}
* [Fórum de suporte do desenvolvedor](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Fórum de suporte do Stack overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
