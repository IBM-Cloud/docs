---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote Message Hub
{: #openwhisk_catalog_message_hub}

Esse pacote permite se comunicar com instâncias do [Message Hub](https://developer.ibm.com/messaging/message-hub) para publicar e consumir mensagens usando a API Kafka nativa de alto desempenho.
{: shortdesc}

## Criando um Acionador que atende a uma instância do IBM MessageHub
{: #openwhisk_catalog_message_hub_trigger}

Para criar um acionador que reaja quando as mensagens forem postadas em uma instância do Message Hub, será necessário usar o feed chamado `/messaging/messageHubFeed`. Essa ação de feed suporta os parâmetros a seguir:

|Nome|Tipo|Descrição|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de sequência de caracteres|Esse parâmetro é uma matriz de sequências `<host>:<port>` que formam os brokers na instância do Message Hub|
|usuário|Sequência de caracteres|Nome do usuário do Message Hub|
|password|Sequência de caracteres|Senha do Message Hub|
|tópico|Sequência de caracteres|O tópico que você gostaria que o acionador atendesse|
|kafka_admin_url|Sequência URL|A URL da interface REST do administrador do Message Hub|
|isJSONData|Booleano (Opcional - padrão=false)|Quando configurado como `true`, isso fará com que o provedor tente analisar o valor da mensagem como JSON antes de passá-lo adiante como a carga útil do acionador.|
|isBinaryKey|Booleano (Opcional - padrão=false)|Quando configurado como `true`, isso fará com que o provedor codifique o valor da chave como Base64 antes de passá-lo adiante como a carga útil do acionador.|
|isBinaryValue|Booleano (Opcional - padrão=false)|Quando configurado como `true`, isso fará com que o provedor codifique o valor da mensagem como Base64 antes de passá-lo adiante como a carga útil do acionador.|

Embora essa lista de parâmetros possa parecer assustadora, ela pode ser configurada automaticamente por você usando o comando de atualização de pacote da CLI:

1. Crie uma instância do serviço Message Hub em sua organização e espaço atuais que você está usando para o OpenWhisk.

2. Verifique se o tópico que você deseja atender já existe no Message Hub ou crie um novo tópico, por exemplo, `mytopic`.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Message Hub que você criou.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  Sua ligação de pacote agora contém as credenciais associadas à sua instância do Message Hub.

4. Agora tudo o que você precisa fazer é criar um Acionador que será disparado quando novas mensagens forem postadas no tópico do Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Configurando um pacote Message Hub fora do Bluemix

Caso deseje configurar o Message Hub fora do Bluemix, deve-se criar manualmente uma ligação de pacote para o serviço Message Hub. Você precisa das credenciais de serviço e das informações de conexão do Message Hub.

1. Crie uma ligação de pacote que esteja configurada para o serviço Message Hub.

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. Agora é possível criar um Acionador usando seu novo pacote que será disparado quando novas mensagens forem postadas para o tópico do Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## Atendendo mensagens
{: #openwhisk_catalog_message_hub_listen}

Depois de criar um acionador, o sistema monitorará o tópico especificado em seu serviço de sistema de mensagens. Quando novas mensagens forem postadas, o acionador será disparado.

A carga útil desse acionador conterá um campo `messages` que é uma matriz de mensagens que foram postadas desde a última vez que o acionador foi disparado. Cada objeto de mensagem na matriz conterá os campos a seguir:
- tópico
- partição
- Deslocamento
- Chave
- derivado

Em termos Kafka, esses campos devem ser autoevidentes. No entanto, `key` possui um recurso opcional `isBinaryKey` que permite que a `key` transmita dados binários. Além disso, o `value` requer consideração especial. Os campos opcionais `isJSONData` e `isBinaryValue` estão disponíveis para manipular mensagens JSON e binárias. Esses campos, `isJSONData` e `isBinaryValue`, não podem ser usados em conjunção com o outro.

Como exemplo, se `isBinaryKey` tiver sido configurado como `true` quando o acionador foi criado, a `key` será codificada como uma sequência Base64 quando retornada da carga útil de um acionador disparado.

Por exemplo, se uma `key` de `Some key` for postada com `isBinaryKey` configurado como `true`, a carga útil do acionador se assemelhará ao seguinte:

```json
     {
    "messages": [
    {
            "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

Se o parâmetro `isJSONData` tiver sido configurado como `false` (ou não tiver sido configurado) quando o acionador foi criado, o campo `value` será o valor bruto da mensagem postada. No entanto, se `isJSONData` tiver sido configurado como `true` quando o acionador foi criado, o sistema tentará analisar esse valor como um objeto JSON, no melhor esforço. Se a análise for bem-sucedida, o `value` na carga útil do acionador será o objeto JSON resultante.

Por exemplo, se uma mensagem de `{"title": "Some string", "amount": 5, "isAwesome": true}` for postada com `isJSONData` configurado como `true`, a carga útil do acionador poderá ser semelhante a isto:

```json
     {
  "messages": [
    {
      "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
          "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
    }
  ]
}
```

No entanto, se o mesmo conteúdo da mensagem fosse postado com `isJSONData` configurado como `false`, a carga útil do acionador seria assim:

```json
     {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

Semelhante a `isJSONData`, se `isBinaryValue` tiver sido configurado como `true` durante a criação do acionador, o `value` resultante na carga útil do acionador será codificado como uma sequência Base64.

Por exemplo, se um `value` de `Some data` for postado com `isBinaryValue` configurado como `true`, a carga útil do acionador se assemelhará a algo como o seguinte:

```json
     {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

Se a mesma mensagem fosse postada sem `isBinaryData` configurado como `true`, a carga útil do acionador seria semelhante ao exemplo abaixo:

```json
     {
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### As mensagens são processadas em lote
Você observará que a carga útil do acionador contém uma matriz de mensagens. Isso significa que se você estiver produzindo mensagens para seu sistema de mensagens muito rapidamente, o feed tentará processar em lote as mensagens postadas em um único disparo do acionador. Isso permite que as mensagens sejam postadas no acionador de maneira mais rápida e eficiente.

Lembre-se de que, ao codificar ações que são disparadas por seu acionador, o número de mensagens na carga útil é tecnicamente sem limites, mas sempre será maior que 0. Aqui está um exemplo de uma mensagem em lote (observe a mudança no valor *offset*):
 
 ```json
     {
   "messages": [
    {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Produzindo mensagens para o Message Hub
Se você quiser usar uma ação do OpenWhisk para produzir de forma conveniente uma mensagem para o Message Hub, será possível usar a ação `/messaging/messageHubProduce`. Essa ação usa os parâmetros a seguir:

|Nome|Tipo|Descrição|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de sequência de caracteres|Esse parâmetro é uma matriz de sequências `<host>:<port>` que formam os brokers na instância do Message Hub|
|usuário|Sequência de caracteres|Nome do usuário do Message Hub|
|password|Sequência de caracteres|Senha do Message Hub|
|tópico|Sequência de caracteres|O tópico que você gostaria que o acionador atendesse|
|derivado|Sequência de caracteres|O valor para a mensagem que você gostaria de produzir|
|Chave|Sequência (opcional)|A chave para a mensagem que você gostaria de produzir|

Embora os primeiros três parâmetros possam ser ligados automaticamente usando `wsk package refresh`, aqui está um exemplo de chamada de ação com todos os parâmetros necessários:

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## Exemplos

### Integrando o OpenWhisk ao IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage e IBM Data Science Experience
O exemplo que integra o OpenWhisk ao serviço IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage, IBM Data Science Experience (Spark) pode ser [localizado aqui](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0).

## Referências
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
