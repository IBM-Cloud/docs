---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conectando e configurando um serviço historiador usando um {{site.data.keyword.cloudant_short_notm}}  
{: #cloudant_main}

Conectar um serviço do {{site.data.keyword.cloudantfull}} ao seu {{site.data.keyword.iot_full}} permite armazenar e acessar os dados de seu dispositivo. Os dados do dispositivo são armazenados em bancos de dados diários, semanais ou mensais, dependendo do intervalo de seu depósito selecionado.

Ao iniciar o uso de um {{site.data.keyword.cloudant_short_notm}} para armazenar dados do dispositivo, três bancos de dados são automaticamente criados, um banco de dados é criado para o intervalo atual do depósito atual, uma para o próximo intervalo e um banco de dados de configuração. Documentos de design podem ser incluídos no banco de dados de configuração e serão copiados para os novos bancos de dados conforme forem criados. Quando o fim de um intervalo é atingido, os dados do dispositivo são armazenados no banco de dados do depósito para o novo intervalo e um novo banco de dados é criado para o próximo intervalo.

Quando os dados do dispositivo são enviados para um banco de dados, eles podem ser armazenados de duas maneiras diferentes. Se os dados forem JSON válido e o formato do evento de dispositivo estiver configurado para `JSON`, os dados do dispositivo serão armazenados no formato a seguir:

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

Se os dados do dispositivo não for um JSON válido ou se o formato não estiver configurado para `JSON`, os dados do dispositivo serão armazenados como uma sequência codificada base64 no campo `payload` no formato a seguir:

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## Antes de iniciar  
{: #byb}

Antes de conectar um {{site.data.keyword.cloudant_short_notm}} a seu serviço do {{site.data.keyword.iot_short}}, conclua as tarefas a seguir:

- Configure um {{site.data.keyword.cloudant_short_notm}} no mesmo espaço do Bluemix que seu {{site.data.keyword.iot_short_notm}} usando o catálogo do Bluemix.

Assegure que você tenha privilégios de desenvolvedor na organização do Bluemix e que esteja conectado por meio do Bluemix. Se você não estiver conectado por meio do Bluemix ou não tiver privilégios de desenvolvedor nessa organização do Bluemix, não será capaz de autorizar a ligação do {{site.data.keyword.cloudant_short_notm}} com o {{site.data.keyword.iot_short_notm}}.

Conclua as etapas a seguir para conectar um {{site.data.keyword.cloudant_short_notm}}:

1. Em seu painel do {{site.data.keyword.iot_short}}, clique em **Extensões** na barra de navegação.
2. No quadro Armazenamento de dados históricos, clique em **Configurar**.
2. Todos os serviços do {{site.data.keyword.cloudant_short_notm}} disponíveis no mesmo espaço do Bluemix que seu serviço do {{site.data.keyword.iot_short}} são listados na seção Configurar armazenamento de dados históricos.
3. Selecione o serviço do {{site.data.keyword.cloudant_short_notm}} que você deseja conectar.
4. Selecione as opções de configuração de seu {{site.data.keyword.cloudant_short_notm}}:

  a. Selecione um intervalo de depósito. O intervalo do depósito controla como que frequência novos bancos de dados são criados para armazenar dados do dispositivo. Novos depósitos são criados à meia-noite no fuso horário selecionado usando o intervalo do depósito selecionado.

  b. Selecione um fuso horário. O horário no fuso horário selecionado será usado para determinar em qual depósito os dados do dispositivo devem ser colocados, não o horário local do dispositivo. Os registros de data e hora nos dados do dispositivo que estão sendo enviados ao {{site.data.keyword.cloudant_short_notm}} serão convertidos para o fuso horário selecionado ao se decidir em qual banco de dados os dados serão inseridos.

  c. Escolha opções que determinam o nome do banco de dados. O nome do banco de dados será `iotp_<orgID>_<dbname>_<bucket_name>` em que:

 +  * `<orgID>` é o ID da sua organização.
 +  * `<dbname>` é a sua opção para essa parte do nome do banco de dados controlada pelo campo `Nome do banco de dados`.
 +  * `<bucket_name>` é uma sequência determinada pela sua opção para o campo `Intervalo de depósitos`:
 +    * Para os intervalos de depósito `day`, `<bucket_name>` será `yyy-mm-dd`.  Por exemplo, `2016-07-06` para eventos em 6 de julho de 2016.
 +    * Para os intervalos de depósito `week`, `<bucket_name>` será `yyyy-'w'ww` em que `'w'ww` indica um número da semana.  Por exemplo, `2016-w03` para eventos na terceira semana de 2016.
 +    * Para os intervalos de depósito `month`, `< bucket_name>` será `yyyy-mm`.  Por exemplo, `2016-07` para eventos em julho de 2016.

5. Clique em **Autorizar**.
6. Clique em **Confirmar** na caixa de diálogo de autorização.

Os dados de seu dispositivo agora estão sendo armazenados em seu {{site.data.keyword.cloudant}}.

## Orientações sobre o uso do Serviço Historian  
{: #recipes}

As orientações a seguir descrevem como usar o {{site.data.keyword.cloudant_short_notm}} como o armazenamento de Historian para o {{site.data.keyword.iot_short}}:

- A orientação [Configurar o {{site.data.keyword.cloudant_short_notm}} como o Armazenamento de dados do Historian para o {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-parti/) descreve como os dados do dispositivo são armazenados no {{site.data.keyword.cloudant_short_notm}} e demonstra como configurar e armazenar dados do dispositivo no {{site.data.keyword.cloudant_short_notm}} como Armazenamento de dados do Historian.

- A orientação [Consultar e processar dados de dispositivo do {{site.data.keyword.iot_short}} por meio do {{site.data.keyword.cloudant_short_notm}}](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-partii) mostra como consultar e executar operações de processamento de dados nos dados do dispositivo que são armazenados no {{site.data.keyword.cloudant_short_notm}}.

- A orientação [Visualizar dados de dispositivo do Watson IoT armazenados no Cloudant NoSQL DB](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=27327) mostra como vincular entre Cartões de gráfico de linha e o Armazenamento de dados do Historian para exibir dados de dispositivo no Painel do Watson IoT Platform.


## Criando novos documentos de design  
{: #design_docs}

Novos documentos de design estão contidos no banco de dados de configuração e são copiados para cada banco de dados criado. O nome do banco de dados de configuração é `iotp_<orgid>_<choice>_configuration
e usa os mesmos parâmetros que os nomes dos bancos de dados descritos na etapa 3b na seção Antes de iniciar.

Os documentos de design padrão contidos no {{site.data.keyword.iot_short_notm}} implementam consultas disponíveis no historiador atual, além da função de resumo.

Documentos de design adicionais podem ser incluídos no banco de dados de configuração e serão copiados para os novos bancos de dados de intervalo do depósito à medida que forem criados. Para incluir documentos de design no banco de dados de configuração, consulte a [Documentação da API (interface de programação de aplicativos) do Cloudant](https://docs.cloudant.com/document.html).

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
