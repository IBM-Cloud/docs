---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling CLI
{: #autoscalingcli}

*Última atualização: 25 de fevereiro de 2016*

É possível configurar o serviço {{site.data.keyword.autoscaling}} usando o {{site.data.keyword.autoscaling}} CLI for {{site.data.keyword.Bluemix_notm}}. O {{site.data.keyword.autoscaling}} CLI suporta Linux64, Win64 e OSX e fornece funcionalidade semelhante ao ajuste automático de escala que a API RESTful fornece.
{: shortdesc}

Antes de iniciar, instale o {{site.data.keyword.Bluemix_notm}} CLI. Veja [Fazer download do {{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window} para obter instruções.

## Incluindo o plug-in do {{site.data.keyword.Bluemix_notm}} CLI

Após o {{site.data.keyword.Bluemix_notm}} CLI ser instalado, é possível incluir o plug-in {{site.data.keyword.autoscaling}} CLI.

Conclua as etapas a seguir para incluir o repositório e instalar o plug-in:
1. Para incluir o repositório do plug-in {{site.data.keyword.Bluemix_notm}} CLI, execute o comando a seguir:
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. Para instalar o plug-in {{site.data.keyword.autoscaling}} CLI, execute o comando a seguir:
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Anexando uma política de ajuste automático de escala

É possível anexar uma política de ajuste automático de escala a um app específico. Execute o seguinte comando:

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">O nome do app ao qual você deseja anexar uma política de ajuste automático de escala.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">O nome do arquivo JSON que descreve a política de ajuste automático de escala. Consulte o <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">doc da API RESTful de {{site.data.keyword.autoscaling}}</a> para obter mais detalhes.</dd>
</dl>


## Gerando uma política de ajuste automático de escala

É possível gerar uma política de ajuste automático de escala respondendo às perguntas na interface de linha de comandos. Dependendo de sua entrada, um arquivo JSON que contém a definição da política de ajuste automático de escala é salvo com o nome que você inserir. Se não inserir o nome do arquivo, o conteúdo da política será impresso na linha de comandos diretamente sem que seja salvo em um arquivo. Execute o seguinte comando:

```bx as policy-create```
{: codeblock}


## Exibindo uma política de ajuste automático de escala

É possível mostrar a política de ajuste automático de escala de um app. O conteúdo da política é impresso na linha de comandos diretamente. Execute o seguinte comando:

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">O nome do app para o qual você deseja mostrar a política de ajuste automático de escala. Por padrão, a estrutura JSON é convertida em uma série de saídas legíveis.</dd>
</dl>

**Dica:** Também é possível usar a opção **--json** para impressão elegante da resposta JSON original.


## Removendo uma política de ajuste automático de escala

É possível remover uma política de ajuste automático de escala de um app. Execute o seguinte comando:

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">O nome do app do qual você deseja remover a política de ajuste automático de escala.</dd>
</dl>


## Ativando ou desativando uma política de ajuste automático de escala

É possível ativar ou desativar a política de ajuste automático de escala de um app específico. Execute o seguinte comando:

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">O nome do app para o qual você deseja ativar ou desativar a política de ajuste automático de escala.</dd>
</dl>


## Exibindo o histórico de ajuste automático de escala de um app

É possível mostrar o histórico da atividade de ajuste automático de escala de um app específico. Uma tabela de registros de histórico de ajuste automático de escala é exibida na interface de linha de comandos.

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">O nome do app para o qual você deseja mostrar o histórico da política de ajuste automático de escala.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">O registro de data e hora do início do intervalo de histórico. Os formatos suportados são `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Por padrão, o registro de data e hora está configurado para 50 horas à frente do horário atual. Veja o <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">Padrão de formatos de data e hora do W3C</a> para obter detalhes sobre o formato do registro de data e hora.
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">O registro de data e hora do término do intervalo de histórico. Os formatos suportados são `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Por padrão, o registro de data e hora está configurado para o horário atual. Veja o <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">Padrão de formatos de data e hora do W3C</a> para obter detalhes sobre o formato do registro de data e hora.
</dl>

**Dica:** Também é possível usar a opção **--json** para impressão elegante da resposta JSON original.

# rellinks
## gerais
* [{{site.data.keyword.autoscaling}} serviço](../../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}}CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [Padrão de formatos de data e hora do W3C](https://www.w3.org/TR/NOTE-datetime){: new_window}


