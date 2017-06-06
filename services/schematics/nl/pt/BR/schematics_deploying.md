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

# Implementando recursos em seus ambientes
{: #deploying}

Com o {{site.data.keyword.bplong}}, é possível implementar suas mudanças de código mais recentes diretamente do código-fonte. Ao implementar seu ambiente, você está implementando os recursos definidos por seus arquivos de configuração. Será possível então gerenciar o fornecimento, as orquestrações e o ciclo de vida do ambiente de dentro do {{site.data.keyword.bpshort}}.
{:shortdesc}

## Implementando em seus ambientes com a GUI
{: #gui}

Se você preferir uma visualização gráfica para implementar seu ambiente, será possível usar o painel do {{site.data.keyword.bpshort}}.
{:shortdesc}


### Pré-requisito
{: #gui-prereq}

* Armazene uma configuração do Terraform no controle de versão. As configurações podem ser gravadas em sintaxe HashiCorp Configuration Language (HCL) ou JSON. Veja os <a href="https://www.terraform.io/docs/configuration/index.html">Docs de configuração de Terraform <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para obter a sintaxe HCL e as diretrizes sobre como gravar as configurações. Veja o <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">Provedor {{site.data.keyword.IBM_notm}} Cloud <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para obter os recursos disponíveis.

Depois de armazenar sua configuração:

1. No painel do **{{site.data.keyword.bpshort}}**, selecione **Ambientes**.

2. Clique em **Criar ambiente** para incluir um ambiente ou selecione a linha de um ambiente existente que você deseja implementar.

3. Clique em **Planejar** para visualizar quais recursos serão provisionados quando você implementar seu ambiente. Quando você executar o plano, o {{site.data.keyword.bpshort}} extrairá as variáveis nos detalhes de seu ambiente e a versão mais recente da configuração do controle de versão. A saída do plano exibe como a configuração é comparada com o que está implementado de acordo com o seu arquivo de estado do Terraform. Seu ambiente fica bloqueado contra mudanças adicionais até que o plano seja aplicado ao ambiente ou cancelado. 

4. Visualize o log na seção **Atividade recente** para inspecionar a saída do plano. A saída do plano mostrará se existem erros e quais recursos o serviço está planejando criar, mudar ou destruir.

5. Quando você estiver pronto para ativar seu plano, clique em **Aplicar**. Será possível monitorar o log de atividades para assegurar-se de que o plano foi aplicado com sucesso na execução mais recente. 


## Implementando em seus ambientes com a CLI
{: #cli}

É possível usar o plug-in do {{site.data.keyword.bpshort}} para a CLI do {{site.data.keyword.Bluemix_notm}} para implementar atualizações em seu ambiente.
{:shortdesc}

### pré-requisitos
{: #cli-prereq}

* Armazene uma configuração do Terraform no controle de versão. 
* Instale a CLI do {{site.data.keyword.Bluemix_notm}} em seu sistema operacional por meio do [repositório da CLI do {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/home.html), se ainda não tiver feito isso.

Depois de efetuar login na CLI do {{site.data.keyword.Bluemix_notm}}:

1. Instale o plug-in da CLI do {{site.data.keyword.bpshort}} executando o comando a seguir.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  O plug-in do {{site.data.keyword.bpshort}} aparecerá sob `bx plugin list` se a instalação for bem-sucedida. 

2. Crie um ambiente por meio de sua configuração. Ao criar seu ambiente, você estará apontando o serviço para seu controle de versão para que ele possa extrair o código mais recente. 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="Descrição do comando environment create.">
  <caption>Tabela 1. Descrição do comando environment create.
  </caption>
  <thead>
  <th colspan="1"></th>
  <th colspan="1">O que você está fazendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>O arquivo JSON no qual os detalhes sobre seu ambiente são armazenados.
  <p>
  <p>Exemplo de
JSON:
  <pre>{
      "description": "(Optional) Description of the environment",
      "frozen": false,
      "name": "Name of the environment",
      "sourceurl": "The GitHub URL that points to the Terraform configuration",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Optional) variable_1",
          "secure": false,
          "value": "Visible value"
      },
      {
          "name": "(Optional) variable_2_secret",
          "secure": true,
          "value": "Secured value"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  Observe o valor `ID` retornado. O `ID` é um identificador exclusivo designado a seu ambiente e é usado em comandos subsequentes.
  
3. Execute o comando `plan` para visualizar como seu ambiente mudaria. O comando plan mostra quais recursos mudariam e por qual quantidade em comparação com o que está implementado, mas as mudanças não entrariam em vigor até a execução do comando `apply`.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Descrição do comando plan.">
  <caption>Tabela 2. Descrição do comando plan.
  </caption>
  <thead>
  <th colspan="1"></th>
  <th colspan="1">O que você está fazendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>O ambiente específico para o qual você deseja executar um plano de execução. Será possível executar <code>bx schematics list</code> se for necessário recuperar o valor para o ID de ambiente.
  </td>
  </tbody></table>
  
  Um `activity_id` é designado ao plano e registrado no log de atividades. 

4. Recupere o log de atividades para visualizar a saída do plano de Terraform.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="Descrição do comando log.">
  <caption>Tabela 3. Descrição do comando log.
  </caption>
  <thead>
  <th colspan="1"></th>
  <th colspan="1">O que você está fazendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>A atividade específica da qual você deseja visualizar o log. Será possível executar <code>bx schematics activity list --id ENVIRONMENT_ID</code> se for necessário recuperar o valor para o ID de atividade.
  </td>
  </tbody></table>
  
5. Execute o comando `apply` para implementar recursos em seu ambiente.
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Descrição do comando apply.">
  <caption>Tabela 4. Descrição do comando apply.
  </caption>
  <thead>
  <th colspan="1"></th>
  <th colspan="1">O que você está fazendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>O ambiente específico no qual você deseja implementar atualizações. Será possível executar <code>bx schematics list</code> se for necessário recuperar o valor para o ID de ambiente.
  </td>
  </tbody></table>
  
6. Monitore a saída de aplicação para assegurar-se de que a implementação seja bem-sucedida. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  Uma implementação bem-sucedida retorna a linha a seguir em direção ao término da saída.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## Implementando em seus ambientes com a API
{: #api}

É possível implementar programaticamente seu ambiente com a API do {{site.data.keyword.bpshort}}.
{:shortdesc}

As chamadas para a <a href="https://us-south.schematics.bluemix.net/swagger-api/">API do {{site.data.keyword.bpshort}} <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> apontam para o terminal base a seguir:

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Pré-requisito
{: #api-prereq}

* Armazene uma configuração do Terraform no controle de versão. 

Conclua as etapas a seguir para implementar recursos em seu ambiente:

1. Gere um token IAM OAuth para usar no cabeçalho de autenticação. O comando gera um token UAA e um token IAM.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Exemplo de Saída:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  A saída `Bearer eyJraWQ...` é um exemplo truncado do token IAM. Inclua o token completo no cabeçalho das chamadas API.
  
2. Crie um ambiente executando uma chamada `POST v1/environments`.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  Uma resposta bem-sucedida retorna a saída a seguir.
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  Observe o valor `id` retornado. O `id` é um identificador exclusivo designado a seu ambiente e é usado em chamadas subsequentes.
  
3. Execute a chamada `POST v1/environments/<environment_ID>/plan` para visualizar quais recursos serão implementados ao ambiente quando você aplicar sua configuração. Os planos extraem as configurações de ambiente na ramificação principal de seu repositório.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  Uma resposta bem-sucedida retorna um `activityid`. O valor activity ID é necessário para visualizar logs, como a saída de plano e de aplicação.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. Execute a chamada `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` para visualizar a saída de plano.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. Implemente seu ambiente executando a chamada `PUT v1/environments/<environment_ID>/apply/`.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Monitore a implementação executando a chamada `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` para visualizar a saída de aplicação.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  Uma implementação bem-sucedida retorna a linha a seguir em direção ao término da saída.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
