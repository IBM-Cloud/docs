---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote Cloudant
{: #openwhisk_catalog_cloudant}
O pacote `/whisk.system/cloudant` permite trabalhar com um banco de dados do Cloudant. Ele inclui as ações e os feeds a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | pacote | dbname, host, username, password | Trabalhar com um banco de dados do Cloudant |
| `/whisk.system/cloudant/read` | ação | dbname, id | Ler um documento a partir de um banco de dados |
| `/whisk.system/cloudant/write` | ação | dbname, overwrite, doc | Gravar um documento em um banco de dados |
| `/whisk.system/cloudant/changes` | alimentação | dbname, maxTriggers | Disparar eventos acionadores nas mudanças em um banco de dados |

Os tópicos a seguir percorrem a configuração de um banco de dados do Cloudant, a configuração de um pacote associado e o uso de ações e feeds no pacote `/whisk.system/cloudant`.

## Configurando um banco de dados Cloudant no Bluemix
{: #openwhisk_catalog_cloudant_in}

Se você estiver usando o OpenWhisk no Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Bluemix Cloudant. Se você não estiver usando o OpenWhisk e o Cloudant no Bluemix, vá para a próxima etapa.

1. Crie uma instância de serviço do Cloudant em seu [painel](http://console.ng.Bluemix.net) do Bluemix.

  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.

2. Certifique-se de que a sua CLI do OpenWhisk esteja no namespace correspondente à organização e ao espaço do Bluemix que você usou na etapa anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Como alternativa, é possível usar `wsk property set --namespace` para configurar um namespace a partir de uma lista daqueles disponíveis para você.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente um pacote de ligação para a instância de serviço do Cloudant criada.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_testCloudant_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  Você vê o nome completo da ligação do pacote que corresponde à instância de serviço do Bluemix Cloudant.

4. Verifique se a ligação do pacote que foi criada anteriormente está configurada com seu host e credenciais da instância de serviço do Cloudant Bluemix.

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
  ]
  ```

## Configurando um banco de dados Cloudant fora do Bluemix
{: #openwhisk_catalog_cloudant_outside}

Caso você não esteja usando o OpenWhisk no Bluemix ou caso deseje configurar o banco de dados Cloudant fora do Bluemix, deve-se criar manualmente uma ligação de pacote para sua conta do Cloudant. Você
precisa do nome do host, do nome do usuário e da senha da conta do Cloudant.

1. Crie uma ligação de pacote que esteja configurada para sua conta do Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. Verifique se a ligação do pacote existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  pacotes
  /myNamespace/myCloudant private binding
  ```


## Recebendo mudanças em um banco de dados do Cloudant
{: #openwhisk_catalog_cloudant_listen}

É possível usar o feed `changes` para configurar um serviço para disparar um acionador em cada mudança em seu banco de dados do Cloudant. Os parâmetros são como segue:

- `dbname`: nome do banco de dados do Cloudant.
- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é definido como infinite.


1. Crie um acionador com o feed `changes` na ligação do pacote criada anteriormente. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
  ok: feed do acionador myCloudantTrigger criado
  ```

2. Pesquisa de ativações.

  ```
  wsk activation poll
  ```
  {: pre}

3. Em seu painel do Cloudant, modifique um documento existente ou crie um novo.

4. Observe novas ativações para o acionador `myCloudantTrigger` para cada mudança no documento.
  
  **Nota**: se você não for capaz de observar novas ativações, consulte as seções subsequentes sobre leitura e gravação em um banco de dados do Cloudant. O teste das etapas de leitura e
gravação a seguir ajudará a verificar se as suas credenciais do Cloudant estão corretas.
  
  Agora, é possível criar regras e associá-las a ações para reagir às atualizações do documento.
  
  O conteúdo dos eventos gerados tem os parâmetros a seguir:
  
  - `id`: o ID do documento.
  - `seq`: o identificador de sequência que é gerado pelo Cloudant.
  - `changes`: uma matriz de objetos, cada um dos quais tendo um campo `rev` que contém o ID da revisão do documento.
  
  A representação JSON do evento acionador é a seguinte:
  
  ```json
     {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```
  
## Gravando em um banco de dados do Cloudant
{: #openwhisk_catalog_cloudant_write}

É possível usar uma ação para armazenar um documento em um banco de dados do Cloudant denominado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

1. Armazene um documento usando a ação `write` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  ```
  ```json
     {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. Verifique se o documento existe procurando-o em seu painel do Cloudant.

  A URL do painel para o banco de dados `testdb` é semelhante à seguinte: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


## Lendo de um banco de dados do Cloudant
{: #openwhisk_catalog_cloudant_read}

É possível usar uma ação para buscar um documento a partir de um banco de dados do Cloudant chamado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

- Busque um documento usando a ação `read` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
     {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## Usando uma sequência de ações e um acionador de mudança para processar um documento de um banco de dados do Cloudant
{: #openwhisk_catalog_cloudant_read_change notoc}
É possível usar uma sequência de ações em uma regra para buscar e processar o documento associado a um evento de mudança do Cloudant.

Aqui está um código de amostra de uma ação que manipula um documento:
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

Crie a ação para processar o documento do Cloudant:
```
wsk action create myAction myAction.js
```
{: pre}

Para ler um documento do banco de dados, é possível usar a ação `read` do pacote do Cloudant.
A ação `read` pode ser editada com `myAction` para criar uma sequência de ações.
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

A ação `sequenceAction` pode ser usada em uma regra que ativa a ação em novos eventos acionadores do Cloudant.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Nota**: o acionador `changes` do Cloudant é usado para suportar o parâmetro `includeDoc`, que não é mais suportado.
  Será necessário recriar os acionadores criados anteriormente com `includeDoc`. Sigas estas etapas para recriar o acionador:
  ```
  wsk trigger delete myCloudantTrigger
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  O exemplo ilustrado acima pode ser usado para criar uma sequência de ações para ler o documento mudado e chamar suas ações existentes.
  Lembre-se de desativar as regras que podem não ser mais válidas e criar novas usando o padrão de sequência de ações.

