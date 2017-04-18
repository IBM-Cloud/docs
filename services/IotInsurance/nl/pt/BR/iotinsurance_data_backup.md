---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Fazer backup de dados
É possível fazer backup dos dados do {{site.data.keyword.iotinsurance_full}} replicando o banco de dados do {{site.data.keyword.cloudantfull}}.
{:shortdesc}

A tabela a seguir mostra os bancos de dados do
{{site.data.keyword.iotinsurance_short}} que são armazenados no {{site.data.keyword.iotinsurance_full}}.

*Tabela 1: Bancos de dados do {{site.data.keyword.iotinsurance_short}}*

Nomes de Banco de Dados| Frequência de mudança| Motivo da Alteração | Requer Backup | Comentário
------------- | -------------| -------------| -------------| -------------
favoritos|Administração|Nova ação do administrador|YES|-
Dispositivos|Administração|Novos dispositivos ou usuários incluídos ou removidos|YES| O Transformer gera dinamicamente uma tabela na memória e a preenche com dados do provedor de dispositivo. Para gateways conectados diretamente, essa tabela armazena os dispositivos.
hazardevents|Aleatório|Novo evento de blindagem detectado|YES|-
Jscode|Administração|Novo código JS para blindagens implementadas|YES*| O administrador pode opcionalmente ignorar o backup e implementar uma nova versão do código JS.
Promoções|Administração|Nova promoção incluída|YES|-
shieldassociations|Administração|Novo usuário ou blindagem incluída|YES|-
Blindagens|Administração|Nova blindagem incluída|YES|- Users|Administração|Novo usuário incluído|YES|-
aggregation|-|-|Não|Pode ser reconstruído.
aggregationschedule|-|-| Não|Pode ser reconstruído.

Para fazer backup dos dados do {{site.data.keyword.iotinsurance_short}},
execute as etapas a seguir:

## Criando uma instância do {{site.data.keyword.cloudant_short_notm}} de réplica
{: #createinstance}
Crie uma instância do {{site.data.keyword.cloudant}} de réplica usando as instruções do [{{site.data.keyword.cloudant}}
![Ícone de link externo](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html). Para propósitos de recuperação de desastre, crie a réplica em um local diferente de seu serviço {{site.data.keyword.iotinsurance_short}} original. Por exemplo, se sua instância original estiver em Dallas, a réplica poderá estar em Londres.

## Localize as credenciais e URLs
{: #locate_credentials}
Localize as credenciais e URLs para sua instância {{site.data.keyword.cloudant}} original e instância replicada.
1. Abra o serviço {{site.data.keyword.cloudant}}.
2. Clique na guia **Credenciais de serviço** que está localizada abaixo do nome do serviço.
3. Clique em **Visualizar credenciais**.
4. Anote o nome do usuário, a senha e a URL.

## Criando novas tarefas de replicação
{: #create_replication}
Crie uma tarefa de replicação para cada banco de dados que deve ser submetido a backup. Os bancos de dados que requerem backup são listados na Tabela 1 na seção anterior.

1. Abra o console do {{site.data.keyword.Bluemix_notm}}.

2. Abra o serviço do {{site.data.keyword.cloudant}} original.

3. Clique em **Ativar** para abrir o painel do {{site.data.keyword.cloudant}}.

4. No menu, selecione **Replicação**.

5. Insira a URL do banco de dados original na seção Origem de banco de dados. Cada URL do banco de dados está no formato https://<CloudantbaseURL>/<database_name>.  Por
exemplo, a URL do banco de dados de eventos de risco é https://<CloudantbaseURL>/hazardevents.

6. Insira a URL do novo banco de dados na seção Banco de dados de destino.

7. **Importante:** não selecione **Tornar esta replicação contínua**.  A replicação contínua impacta gravemente o desempenho.

8. Clique em **Replicar dados**.  

9. (opcional) Como as tarefas de replicação subsequentes sobrescrevem os dados
anteriores, considere a exportação dos dados para um arquivo CSV.  Para obter instruções, veja [Exportar Cloudant JSON como CSV, RSS ou iCal ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Repita estas etapas para cada banco de dados.

## Executando um backup
{: #run_backup}
Depois de criar as tarefas de replicação, é possível executar novamente backups a qualquer momento.
1. Abra o console do {{site.data.keyword.Bluemix_notm}}.
2. Abra o serviço do {{site.data.keyword.cloudant}} original.
3. Clique em **Ativar** para abrir o painel do {{site.data.keyword.cloudant}}.
4. No menu, clique em **Replicação** e depois selecione **Todas as replicações**.
5. Selecione todos os bancos de dados e execute novamente cada replicação. É
possível verificar o status das tarefas em andamento clicando em **Replicações
ativas**.
6. Quando todas as replicações estiverem concluídas, será possível exportar os dados
para um arquivo simples CSV.

## Restauração de dados
{: #restore_data}
É possível restaurar os dados de um banco de dados replicado ou carregando um arquivo CSV salvo.
1. Abra o console do {{site.data.keyword.Bluemix_notm}}.
2. Pare o serviço do {{site.data.keyword.iotinsurance_short}}.
3. Restaure os dados de uma das seguintes maneiras:
  - Carregue os dados de um arquivo de backup CSV diretamente na instância primária do Cloudant
  - Crie uma tarefa de replicação que tenha o banco de dados replicado como origem e o banco de dados original como destino. Essa tarefa move os dados replicados para o banco de dados original.
4. Execute os scripts a seguir para recriar os documentos de design e restaurar a
integridade referencial.  Os scripts estão localizados no [{{site.data.keyword.iotinsurance_short}}site GitHub de exemplos de API ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - Esse script recria os documentos de design no {{site.data.keyword.cloudant}}.
  - iot4i-api/wearable-framework/health/check-relations - Esse script restabelece a integridade referencial. Por exemplo, o script corrige um caso no qual uma blindagem é excluída, mas a associação a um usuário ainda existe.
