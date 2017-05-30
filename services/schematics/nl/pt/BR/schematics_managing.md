---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando recursos em seus ambientes
{: #managing}

O {{site.data.keyword.bplong}} simplifica o gerenciamento de seus ambientes. É possível modificar seus recursos implementados e reimplementar mudanças on demand repetidamente.

{:shortdesc}

As mudanças em seu ambiente podem ser implementadas com um processo leve. Quando você desejar mudar os recursos que foram alocados, deverá codificar as mudanças em sua configuração em sintaxe declarativa ou seja, indicará apenas o resultado desejado. Com o {{site.data.keyword.bpshort}}, é possível visualizar as mudanças antes da implementação.


## Atualizando recursos com a GUI
{: #gui}

Se preferir uma visualização gráfica para gerenciar os recursos em seus ambientes, será possível usar o painel do {{site.data.keyword.bpshort}}.
{:shortdesc}

Depois de publicar mudanças de código em sua configuração no GitHub ou de modificar variáveis na GUI, conclua as etapas a seguir para implementar atualizações em seu ambiente:

1. No painel do **{{site.data.keyword.bpshort}}**, selecione **Ambientes**.

2. Clique na linha do ambiente específico que você deseja atualizar.

3. Clique em **Plano** e inspecione se há erros em seu log de plano. O ambiente é bloqueado até que você ou outros colaboradores em sua conta do {{site.data.keyword.Bluemix_notm}} apliquem o plano ou o cancelem. 

4. Clique em **Aplicar** para implementar atualizações. 


## Atualizando recursos com a CLI
{: #cli}

É possível atualizar recursos programaticamente em seus ambientes com a CLI do {{site.data.keyword.bpshort}}.
{:shortdesc}

Depois de publicar mudanças de código em sua configuração no GitHub, conclua as etapas a seguir para implementar atualizações em seu ambiente:

1. Execute o comando `plan`. A CLI do {{site.data.keyword.bpshort}} puxa a configuração do ambiente atualizado do GitHub e gera uma visualização de como seus recursos diferem com relação à implementação atual.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. Visualize a saída do plano no log de atividades.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. Implemente seu plano executando o comando `apply`.  

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Atualizando recursos com a API
{: #api}

É possível gerenciar recursos programaticamente em seus ambientes com a API do {{site.data.keyword.bpshort}}.
{:shortdesc}

Depois de publicar mudanças de código em sua configuração no GitHub, conclua as etapas a seguir para implementar atualizações em seu ambiente:

1. Execute a chamada `POST v1/environments/<environment_ID>/plan`. A API do {{site.data.keyword.bpshort}} puxa a configuração do ambiente atualizado do GitHub e a compara com o arquivo de estado do Terraform para mostrar como seus recursos diferem com relação à implementação atual.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Resposta de exemplo:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. Visualize a saída do plano no log de atividades.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Implemente seu plano executando a chamada `PUT /v1/environments/<environment_ID>/apply`. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Auditando mudanças em seus ambientes
{: #auditing}

As configurações podem ser auditadas no histórico de versões de seu repositório de controle de versão. Para monitorar implementações em seu ambiente ou visualizar logs de implementações anteriores, o {{site.data.keyword.bpshort}} oferece as opções a seguir para visualizar logs de auditoria.

### No painel do {{site.data.keyword.bpshort}}
{: #auditing-gui}

1. Selecione a linha do ambiente para acessar a página de detalhes do ambiente.

2. Monitore a seção **Atividades recentes**. Também é possível visualizar logs históricos de planos e implementações anteriores.

### Com a CLI do {{site.data.keyword.bpshort}}
{: #auditing-cli}

1. Recupere seu ID de ambiente.

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Recupere os IDs de atividade de seu ambiente. Os IDs de atividade são designados a ações de plano, aplicação, destruição e exclusão. O comando a seguir lista todas as atividades executadas em seu ambiente.

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. Recupere dados sobre uma atividade específica, como quem fez mudanças em um ambiente e quando.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. Opcional: para visualizar um log detalhado, como saída de plano ou aplicação, execute o comando `log`. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### Com a API do {{site.data.keyword.bpshort}}
{: #auditing-api}

1. Recupere seu ID de ambiente.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  O corpo de resposta contém todos os ambientes em sua conta do {{site.data.keyword.Bluemix_notm}}. Localize o valor `id` do ambiente específico que você deseja auditar.

2. Recupere os IDs de atividade das ações executadas em seu ambiente.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Obtenha uma atividade específica para um ambiente. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Inspecione um log detalhado da saída do Terraform.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
