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

# Plug-in da CLI do {{site.data.keyword.bpshort}} para a CLI do {{site.data.keyword.Bluemix_notm}}
{: #cli}

Consulte os comandos do {{site.data.keyword.bpshort}} para a CLI do {{site.data.keyword.Bluemix}} para gerenciar seus ambientes e executar outras operações no {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Antes de usar os comandos da CLI:

* Efetue login no {{site.data.keyword.Bluemix_notm}} com `bx login [--sso]` para autenticar sua sessão. Os usuários com um ID federado precisarão usar a sinalização `--sso` para gerar uma senha descartável.

Para visualizar uma lista de comandos, é possível executar `bx schematics help`.

<table id="manage_environments" summary="Gerenciar seus ambientes com os comando bx schematics environment.">
<caption>Tabela 1. Comandos disponíveis para gerenciar seu ambiente. Os comandos seguem a sintaxe <code>bx schematics environment</code>.
</caption>
 <thead>
 <th colspan="5">Gerenciando seu Ambiente</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Atualizar os recursos provisionados por seu ambiente com os comandos bx schematics action.">
 <caption>Tabela 2. Comandos disponíveis para atualizar recursos em seu ambiente. Os comandos seguem a sintaxe <code>bx schematics action</code>.
 </caption>
  <thead>
  <th colspan="5">Atualizando seus recursos</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Auditando atividades executadas em seu ambiente com os comandos bx schematics activity.">
  <caption>Tabela 3. Comandos disponíveis para auditar as atividades executadas em seu ambiente. Os comandos seguem a sintaxe <code>bx schematics activity</code>.
  </caption>
   <thead>
   <th colspan="5">Auditando seu Ambiente</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Crie um ambiente no {{site.data.keyword.Bluemix_notm}} por meio de sua configuração.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### Parâmetro

<dl>
<dt>--file FILE_NAME</dt>
<dd>O arquivo JSON usado para passar detalhes sobre seu ambiente.
<p>
<p>Exemplo de JSON com todos os valores disponíveis:
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
}</pre></dd>
<dt>--json</dt>
<dd>Imprimir a saída no formato JSON.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Remova a configuração de seu ambiente do {{site.data.keyword.Bluemix_notm}}. Esse comando é recomendado apenas para ambientes sem recursos em execução. Se você excluir um ambiente com recursos em execução, será necessário gerenciar cada recurso nos painéis de serviço individuais.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### Parâmetro

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forçar o avanço do comando sem uma confirmação sim/não.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Recupere uma lista de todos os ambientes existentes em sua conta do {{site.data.keyword.Bluemix_notm}}.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### Parâmetro
<dl>
<dt>--count VALUE</dt>
<dd>O número de ambientes a serem limitados em seu retorno.</dd>
<dt>--offset VALUE</dt>
<dd>O deslocamento na lista de ambientes.</dd>
<dt>--json</dt>
<dd>Imprimir a saída no formato JSON.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Recupere detalhes sobre um ambiente existente.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--json</dt>
<dd>Imprimir a saída no formato JSON.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Atualize os detalhes sobre um ambiente existente, como o nome do ambiente ou a URL do GitHub. Para atualizar o número de recursos alocados no ambiente, veja [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>O arquivo JSON usado para passar detalhes sobre seu ambiente.
Veja [bx schematics environment create](#environment-create) para obter um exemplo de fragmento JSON com valores permitidos.</dd>
<dt>--json</dt>
<dd>Imprimir a saída no formato JSON.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Implemente a configuração de seu ambiente. O comando `apply` verifica e executa as configurações armazenados no repositório GitHub.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forçar o avanço do comando sem uma confirmação sim/não.</dd>
<dt>--json</dt>
<dd>Imprimir a saída de aplicação no formato JSON.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Destrua seu ambiente e recursos. O comando `destroy` destrói seu ambiente, incluindo recursos em execução. Essa ação é usada geralmente apenas para ambientes temporários, como um ambiente de QA, com a intenção de ficar no ambiente por um período limitado. Não é recomendado destruir ambientes de produção. A ação `destroy` não pode ser revertida e deve ser usada com cuidado.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forçar o avanço do comando sem uma confirmação sim/não.</dd>
<dt>--json</dt>
<dd>Imprimir a saída de destruição no formato JSON.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Compare a configuração de seu ambiente com a configuração implementada. O comando `plan` verifica a configuração no repositório GitHub e executa um diff no arquivo de estado que está associado ao ambiente implementado. A saída de plano mostra quais recursos seriam incluídos ou removidos se você tivesse implementado a configuração de seu ambiente com o comando `apply`. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>O arquivo JSON opcional usado para passar parâmetros para a ação de plano. É possível passar o parâmetro <code>sourcesha</code> para referenciar uma ramificação Git específica para a configuração de Terraform do ambiente. A ramificação Git deve ser especificada como uma referência principal, como <code>refs/heads/BRANCH_NAME</code>. Se nenhum parâmetro for especificado, o valor padrão será o principal da ramificação principal, que é <code>refs/heads/master</code>.
<p>
<p>Exemplo de fragmento JSON com valor:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>Imprimir a saída de plano no formato JSON.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

Liste os dados de atividades de Terraform executadas em um ambiente.

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>O identificador exclusivo do ambiente. É possível recuperar esse valor executando <code>bx schematics environment list</code>.</dd>
<dt>--count VALUE</dt>
<dd>O número de atividades a serem retornadas.</dd>
<dt>--offset VALUE</dt>
<dd>O deslocamento na lista.</dd>
<dt>--json</dt>
<dd>Imprimir a saída de plano no formato JSON.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

Visualize os logs de atividade detalhados para ações executadas em um ambiente.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>A sinalização para retornar detalhes sobre uma atividade específica. É possível recuperar uma lista de IDs de atividade por ambiente com o comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

Visualize arquivos de plano para um ambiente.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>A sinalização para retornar detalhes sobre uma atividade específica. É possível recuperar uma lista de IDs de atividade por ambiente com o comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Recupere detalhes sobre uma atividade específica executada em um ambiente.

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### Parâmetro
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>A sinalização para retornar detalhes sobre uma atividade específica. É possível recuperar uma lista de IDs de atividade por ambiente com o comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
<dt>--json</dt>
<dd>Imprimir a saída de plano no formato JSON.</dd>
</dl>
