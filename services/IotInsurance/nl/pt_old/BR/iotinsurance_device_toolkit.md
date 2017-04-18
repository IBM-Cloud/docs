---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Kit de ferramentas de dispositivo
{: #iot4i_connecting_devices}
Usando o kit de ferramentas de dispositivo do {{site.data.keyword.iotinsurance_full}}, é possível conectar dispositivos fabricados por qualquer fornecedor de dispositivo ao serviço do {{site.data.keyword.iotinsurance_short}}.
{:shortdesc}

Os dispositivos podem enviar dados diretamente ao
{{site.data.keyword.iot_full}} ou por meio da nuvem do fornecedor do dispositivo. Conecte os dispositivos registrando os usuários autorizados e, em seguida, configurando a geração e a recepção de evento de dispositivo. Para obter uma lista dos dispositivos e fornecedores suportados, bem como dos
procedimentos de integração de amostra, veja [Dispositivos
e fornecedores suportados](iotinsurance_supporteddevices.html).

Use as instruções nas seções a seguir para conectar seus dispositivos.

## Registrando usuários autorizados
{: #reg_users}
Quando a nuvem do fornecedor do dispositivo suporta OAuth como protocolo de autorização, o {{site.data.keyword.iotinsurance_short}} pode agir como cliente OAuth e conectar-se à nuvem do fornecedor. Um ID do cliente e a autorização que são obtidos do fornecedor do dispositivo são necessários para receber e atualizar dados em nome do usuário.  

### Fluxo OAuth
{: #oauth_flow}
O diagrama a seguir mostra um fluxo do OAuth simplificado no qual o
{{site.data.keyword.iotinsurance_short}} é autorizado por meio de um provedor
OAuth, como o Facebook. No diagrama, o {{site.data.keyword.iotinsurance_short}}
solicita acesso a um cliente OAuth, que redireciona a solicitação de acesso para o
provedor OAuth. O provedor produz um formulário HTML no qual o usuário do
{{site.data.keyword.iotinsurance_short}} insere um ID de usuário e uma senha. O
provedor então concede autorização e opcionalmente retorna um código OAuth para ativar
atualizações. O diagrama mostra um fluxo muito básico; provedores OAuth geralmente
oferecem diversos terminais REST para as etapas que são descritas no diagrama.  

![Fluxo do processo OAuth do {{site.data.keyword.iotinsurance_short}}. Este diagrama é descrito no corpo principal do tópico.](images/IoT4I_oauth_flow.svg "{{site.data.keyword.iotinsurance_short}} OAuth process flow")

### Fluxo de registro do usuário
{: #user_reg_flow}

O registro do usuário varia por fornecedor. Para entender como obter os tokens de acesso
de nuvem necessários e como registrá-los no {{site.data.keyword.iotinsurance_short}} usando
a API, veja [Dispositivos e fornecedores suportados](iotinsurance_supporteddevices.html).

#### Fluxo do registro móvel (*descontinuado*)

**Nota**: o app móvel suporta somente o Wink, e mudanças no {{site.data.keyword.amashort}} desativaram o fluxo de registro do usuário que
é descrito nesta seção. Esse fluxo está disponível somente para instâncias existentes da
versão 1.0 do {{site.data.keyword.iotinsurance_short}}.

O diagrama a seguir mostra um fluxo de registro do usuário simplificado. Nesse exemplo,
uma nova solicitação de registro do usuário é feita de um dispositivo móvel. A
solicitação é processada pelo {{site.data.keyword.amafull}}, que fornece um
identificador ao sistema de suporte do cliente e envia a solicitação para o serviço de
registro de API. O serviço de registro de API redireciona a solicitação OAuth para a nuvem
do fornecedor do dispositivo, que por sua vez verifica a autenticação com o sistema de
suporte do cliente. A nuvem do fornecedor do dispositivo retorna o código de autorização
ou token para o serviço de registro de API. O serviço de registro então cria o usuário
e um token exclusivo da API no {{site.data.keyword.iot_short_notm}} e no
{{site.data.keyword.cloudant}}.

![Fluxo de registro do usuário do {{site.data.keyword.iotinsurance_short}}. Este diagrama é descrito no corpo principal do tópico.](images/IoT4I_reg_user.svg "{{site.data.keyword.iotinsurance_short}} User registration flow")

## Gerando eventos de dispositivo
{: #generating_device_events}
Os dispositivos podem se conectar ao {{site.data.keyword.iot_short_notm}} quando
o fabricante fornece um código de autorização direto que pode ser usado com a chave API
que é gerada durante o registro do usuário. Esse tipo de conexão é descrito em
[Desenvolvendo
dispositivos no {{site.data.keyword.iot_short_notm}}](https://console.{DomainName}/docs/services/IoT/devices/device_dev_index.html).

Quando o dispositivo é conectado por meio da nuvem do fornecedor, os eventos
do dispositivo são enviados por meio de uma conexão que usa o terminal REST fornecido
pelo fornecedor do dispositivo. O token de acesso OAuth que é obtido durante o registro
do usuário concede autorização para essas chamadas. O transformador do
{{site.data.keyword.iotinsurance_short}} puxa as informações do usuário associado
para cada dispositivo da nuvem do fornecedor. Em seguida, ele inclui a associação do
usuário com os dados do evento do dispositivo que ele passa para o
{{site.data.keyword.iot_short_notm}}.

Quando o dispositivo é conectado diretamente ao
{{site.data.keyword.iot_short_notm}}, o link entre o dispositivo e o usuário é
armazenado no {{site.data.keyword.iot_short_notm}}. O transformador do
{{site.data.keyword.iotinsurance_short}} armazena em cache essas informações
e, em seguida, enriquece os eventos de dispositivo com o link para o usuário.

### Nuvem para nuvem - fluxo de eventos do dispositivo
{: #device_event_flow}
O diagrama a seguir mostra um fluxo de evento de dispositivo simplificado. Nesse exemplo,
um dispositivo detecta um vazamento de água. O transformador do
{{site.data.keyword.iotinsurance_short}} periodicamente pesquisa a nuvem do
fornecedor para ver se há mudanças no status do dispositivo. Quando o evento é detectado,
o transformador o envia para o {{site.data.keyword.iot_short_notm}}. O mecanismo
de blindagem do {{site.data.keyword.iotinsurance_short}} analisa o evento e, em
seguida, gera um alerta e armazena o alerta no {{site.data.keyword.cloudant}}. O
{{site.data.keyword.iot_short_notm}} transfere o alerta para o mecanismo de ação
do {{site.data.keyword.iotinsurance_short}} para análise. O mecanismo de ação
então envia por push o alerta para o app móvel do consumidor por meio do {{site.data.keyword.mobilepushshort}}.  

![Fluxo de registro de evento de dispositivo do {{site.data.keyword.iotinsurance_short}}. Este diagrama é descrito no corpo principal do tópico.](images/IoT4I_device_reg.svg "{{site.data.keyword.iotinsurance_short}} Device event registration flow")

### Como configurar a pesquisa de status do dispositivo
{: #device_polling}
O microsserviço de transformador é responsável por pesquisar e receber atualizações de status. Se
a API REST do fornecedor do dispositivo suportar atualizações de dispositivo assíncronas,
será possível estabelecer uma assinatura que permite ao transformador receber
atualizações de status do dispositivo à medida que elas ocorrem. Caso contrário, você
poderá configurar o transformador para pesquisar atualizações de status do dispositivo.

As chamadas de pseudo-função a seguir são usadas para definir o processo de pesquisa:

*Tabela 1: Chamadas de pseudo-função*

Pseudo-função | Description (Descrição)
------------- | -------------
`getRegisteredUserDevices(userName)` | Recupera os dispositivos do usuário registrado disponíveis que estão utilizando o nome do usuário.
`getProviderDevices(providerUserToken)` | Chama a API REST do provedor de dispositivo para obter o status dos dispositivos do usuário que estão utilizando o token de acesso do usuário.
`findDevicesToAdd(), findDevicesToDel(), findDevicesToUpdate()` | Localiza os dispositivos novos, excluídos e modificados, comparando dispositivos registrados com dispositivos que existem atualmente no provedor de dispositivo.
` syncData()` | Sincronize os dispositivos do usuário, excluindo dispositivos antigos, incluindo novos e atualizando os modificados.  
 `notifyIoTP()` | Notifique o {{site.data.keyword.iot_short_notm}} sobre as mudanças, tais como eventos MQTT.
O transformador posta atualizações de status para o {{site.data.keyword.iot_short_notm}}, conforme mostrado no exemplo de código a seguir.
```
// as specified in VCAP.services
var appClientConfig = {
  "org":iot_org,
  "id":iot_appid,
  "auth-key":iot_authkey,
  "auth-token":iot_authtoken
};

var appClient = new iotclient.IotfApplication(appClientConfig);
try {
  appClient.connect();
} catch (err) {
  console.log('IoT connect failed with error' +err);
}

...

// generate IoT event, note that the content is an arbitrary JSON object  
try {
  appClient.publishDeviceEvent("iOS",userToken.username, "status", "json", JSON.stringify(iotDevice));
} catch (err) {
  console.log('IoT publish failed with error' +err +'foruser' +userToken.username);
}

```

O transformador usa o {{site.data.keyword.cloudant}} para acessar dados do
usuário, como token de acesso, e para armazenar o último status conhecido do dispositivo
para propósitos de comparação.  Os métodos e fragmentos de código do
{{site.data.keyword.cloudant}} a seguir são fornecidos como referência.  

`getUserTokensByProvider` Esse método obtém todos os tokens do usuário de um provedor específico.

```
dbHelper.getUserTokensByProvider(provider, function (err,results) {
  if (!err) {
    console.log(results.token.length + " tokens retrieved for provider: " + Provider);
  } else {
    console.log("no tokens returned, err:",err);
  }
  });
```

`getDevicesByUser` - Esse método recupera todos os dispositivos do usuário registrado, por nome de usuário.
```
dbHelper.getDevicesByUser(username, function (err,results) {
  if (!err) {
    console.log(results.length + " devices retrieved for username: " + username);
  } else {
    console.log("no devices returned, err:",err);
  }
  });
```

`bulkUpdateDevices` - Esse método atualiza ou inclui um grupo de dispositivos do usuário.
```
dbHelper.bulkUpdateDevices(userDevices, function (err,results) {
  if (!err) {
    console.log(results.length + " devices updated");
    } else {
      console.log("no devices updated, err:",err);
    }
  });
```

`bulkDelDevices` - Esse método exclui um grupo de dispositivos do usuário.
```
dbhelper.bulkDelDevices(userDevices, function (err, results) {
  if (!err) {
    console.log(results.length + "devices deleted");
  } else {
    console.log("no devices deleted, err:",err);
  }
  });

```


## Implementando uma nova instância de transformador
{: #deploy_new_transformer}
É possível implementar uma nova instância de transformador na mesma organização e espaço em que o {{site.data.keyword.iotinsurance_short}} é implementado.  

**Nota:** para obter informações e assistência ao implementar uma nova
instância do Transformer, veja [Entrando em
contato com o suporte](../support/index.html#contacting-support).

Antes de iniciar, faça download e instale a interface de linha de comandos do Cloud
Foundry. Use a interface de linha de comandos do Cloud Foundry para modificar e
implementar instâncias de serviço para o {{site.data.keyword.iot_short_notm}}. Para obter mais informações, veja [Iniciar codificação com a interface da linha de comandos cf ![Ícone de link externo](../../icons/launch-glyph.svg)](https://www.ng.bluemix.net/docs/#starters/install_cli.html){:new_window}.

1. Na interface da linha de comandos, mude seu diretório para o `diretório
com as origens e o arquivo YML descritor de implementação` usando o
comando a seguir:
```
$ cd directory_name
```
2. Lista todos os apps no {{site.data.keyword.iotinsurance_short}}
e anote o nome do transformador. O nome termina com `transformer`.

3. Pare o transformador do {{site.data.keyword.iotinsurance_short}}. For example,
```
$ cf stop iot4i-dev-transformer
```
4. Liste todos os serviços incluídos no {{site.data.keyword.iotinsurance_short}} e anote os nomes dos serviços {{site.data.keyword.iot_short_notm}} e {{site.data.keyword.cloudant}}.  O nome dos serviços do {{site.data.keyword.iot_short_notm}} inclui as letras `iotf` no nome. O nome do serviço do {{site.data.keyword.cloudant}} inclui `cloudant` no nome.

5. Usando os nomes que você anotou nas etapas anteriores, crie um arquivo descritor de implementação semelhante ao exemplo a seguir.  
  ```
  applications:
  - path: .
    memory: 1024M
    instances: 1
    name: iot4i-dev-transformer
    no-route: false
    disk_quota: 1024M
    command: node index.js
    services:
    - iot4i-iotf-service
    - iot4i-cloudantNoSQLDB
    env:
       ENV: dev
       APIDOMAIN: iot4insurance-api-v.mybluemix.net
       NODE_MODULES_CACHE: false
  ```
6. Envie por push o transformador para o {{site.data.keyword.Bluemix_notm}} usando o
comando a seguir, substituindo `newtransformer` pelo nome do seu arquivo
descritor de implementação:
  ```
  $ cf push -f newtransformer.yml
  ```
7. É possível verificar os logs para visualizar mensagens de implementação usando o comando a seguir:
  ```
  $ cf logs iot4i-dev-transformer
  ```
