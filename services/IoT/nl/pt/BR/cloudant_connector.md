---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conectando e configurando um serviço historiador usando um {{site.data.keyword.cloudant}}  
{: #cloudant_main}
Última atualização: 16 de setembro de 2016
{: .last-updated}

Conectar um serviço do {{site.data.keyword.cloudantfull}} ao seu {{site.data.keyword.iot_full}} permite armazenar e acessar os dados de seu dispositivo. Os dados do dispositivo são armazenados em bancos de dados diários, semanais ou mensais, dependendo do intervalo de seu depósito selecionado.

Ao iniciar o uso de um {{site.data.keyword.cloudant}} para armazenar dados do dispositivo, três bancos de dados são automaticamente criados, um banco de dados é criado para o intervalo atual do depósito atual, uma para o próximo intervalo e um banco de dados de configuração. Documentos de design podem ser incluídos no banco de dados de configuração e serão copiados para os novos bancos de dados conforme forem criados. Quando o fim de um intervalo é atingido, os dados do dispositivo são armazenados no banco de dados do depósito para o novo intervalo e um novo banco de dados é criado para o próximo intervalo.

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

Antes de conectar um {{site.data.keyword.cloudant}} a seu serviço do {{site.data.keyword.iot_short}}, conclua as tarefas a seguir:

- Configure um {{site.data.keyword.cloudant}} no mesmo espaço do Bluemix que seu {{site.data.keyword.iot_short_notm}} usando o catálogo do Bluemix.

Assegure que você tenha privilégios de desenvolvedor na organização do Bluemix e que esteja conectado por meio do Bluemix. Se você não estiver conectado por meio do Bluemix ou não tiver privilégios de desenvolvedor nessa organização do Bluemix, não será capaz de autorizar a ligação do {{site.data.keyword.cloudant}} com o {{site.data.keyword.iot_short_notm}}.

Conclua as etapas a seguir para conectar um {{site.data.keyword.cloudant}}:

1. Em seu painel do {{site.data.keyword.iot_short}}, clique em **Extensões** na barra de navegação.
2. No quadro Armazenamento de dados históricos, clique em **Configurar**.
2. Todos os serviços do {{site.data.keyword.cloudant}} disponíveis no mesmo espaço do Bluemix que seu serviço do {{site.data.keyword.iot_short}} são listados na seção Configurar armazenamento de dados históricos.
3. Selecione o serviço do {{site.data.keyword.cloudant}} que você deseja conectar.
4. Selecione as opções de configuração de seu {{site.data.keyword.cloudant}}:

  a. Selecione um intervalo de depósito. O intervalo do depósito controla como que frequência novos bancos de dados são criados para armazenar dados do dispositivo. Novos depósitos são criados à meia-noite no fuso horário selecionado usando o intervalo do depósito selecionado.

  b. Selecione um fuso horário. O horário no fuso horário selecionado será usado para determinar em qual depósito os dados do dispositivo devem ser colocados, não o horário local do dispositivo. Os registros de data e hora nos dados do dispositivo que estão sendo enviados ao {{site.data.keyword.cloudant}} serão convertidos para o fuso horário selecionado ao se decidir em qual banco de dados os dados serão inseridos.

  c. Escolha um nome de banco de dados. O nome do banco de dados será `Iotp_<orgID>_<choice>_<bucket_name>`, em que `<orgID>` é o ID de sua organização, `<choice>` é sua opção de nome do banco de dados e `<bucket_name>` é uma sequência que define se o banco de dados usa um intervalo de depósito diário, semanal ou mensal. O `<bucket_name>` usa o formato a seguir.

  Para intervalos de depósitos diários, `<bucket_name>` será `yyyy-mm-dd`. Para intervalos de depósitos semanais, `<bucket_name>` será `yyyy-www`, em que `www` indica o número da semana, por exemplo, `2016-w03`. Para intervalos de depósitos mensais, `<bucket_name>` será `yyyy-mm`.

5. Clique em **Autorizar**.
6. Clique em **Confirmar** na caixa de diálogo de autorização.

Os dados de seu dispositivo agora estão sendo armazenados em seu {{site.data.keyword.cloudant}}.

## Criando novos documentos de design  
{: #design_docs}

Novos documentos de design estão contidos no banco de dados de configuração e são copiados para cada banco de dados criado. O nome do banco de dados de configuração é 'Iotp_<orgid>_<choice>_configuration'
e usa os mesmos parâmetros que os nomes dos bancos de dados descritos na etapa 3b na seção Antes de iniciar.

Os documentos de design padrão contidos no {{site.data.keyword.iot_short_notm}} implementam consultas disponíveis no historiador atual, além da função de resumo.

Documentos de design adicionais podem ser incluídos no banco de dados de configuração e serão copiados para os novos bancos de dados de intervalo do depósito à medida que forem criados. Para incluir documentos de design no banco de dados de configuração, consulte a [Documentação da API (interface de programação de aplicativos) do Cloudant](https://docs.cloudant.com/document.html).

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant}}](link) -->
