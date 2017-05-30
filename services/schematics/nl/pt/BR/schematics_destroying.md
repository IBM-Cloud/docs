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

# Destruindo recursos em ambientes temporários
{: #destroying}

É possível usar o {{site.data.keyword.bplong}} para destruir seus recursos. Ao destruir seus recursos, você está derrubando seu ambiente e todos os recursos associados.  
{:shortdesc}

**Aviso**: quando você destrói recursos, a ação não pode ser revertida. A destruição de recursos não é recomendada para ambientes de produção, mas pode ser útil para ambientes temporários, como de teste ou QA.

Antes de destruir seus recursos, considere as diretrizes a seguir: 
* Assegure-se de que o tráfego não esteja direcionado para seus recursos.
* Assegure-se de que quaisquer dados que possam ser necessários tenham sido submetidos a backup. 


## Destruindo recursos com a GUI
{: #gui}

É possível usar o painel do {{site.data.keyword.bpshort}} para girar e derrubar ambientes temporários.
{:shortdesc}

1. No painel do **{{site.data.keyword.bpshort}}**, selecione a guia **Ambientes**.

2. Clique na linha do ambiente específico que você deseja remover. 

3. No menu de opções, selecione **Destruir recursos** ou **Excluir ambiente**. As ações de exclusão e destruição não são reversíveis. Para determinar qual opção selecionar, considere se você tem recursos ativos.
  * Selecione **Destruir recursos** se desejar parar e remover seus recursos ativos. Recomenda-se executar um plano antes da destruição para confirmar se os recursos que estão associados ao ambiente podem ser removidos.
  * Selecione **Excluir ambiente** se desejar remover a configuração do ambiente do serviço {{site.data.keyword.bpshort}}. Essa opção geralmente será usada se o ambiente não estiver implementado e não tiver recursos ativos. Se você selecionar essa opção com recursos ativos, não será mais possível usar o serviço {{site.data.keyword.bpshort}} para rastrear ou implementar mudanças em seu ambiente. Os recursos ativos precisam ser gerenciados individualmente, em seus painéis de serviço.
  
  Siga os prompts na tela para confirmar sua opção. 


## Destruindo recursos com a CLI
{: #cli}

É possível usar a CLI do {{site.data.keyword.bpshort}} para girar e derrubar ambientes temporários.
{:shortdesc}

1. Execute o comando `destroy` para derrubar seu ambiente e recursos.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. Opcional: execute o comando `delete` se desejar remover sua configuração do serviço.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Destruindo recursos com a API
{: #api}

É possível usar a API do {{site.data.keyword.bpshort}} para girar e derrubar ambientes temporários.
{:shortdesc}

1. Execute a chamada `PUT v1/environments/<environment_ID>/destroy` para destruir seus recursos.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Opcional: execute a chamada `DELETE v1/environments/<environment_ID>` se desejar remover sua configuração do serviço {{site.data.keyword.bpshort}}.

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
