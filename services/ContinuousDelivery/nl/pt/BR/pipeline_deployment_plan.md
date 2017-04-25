---

copyright:
  years: 2017
lastupdated: "2017-3-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Customizando planos de implementação para pipelines compostos
{: #tasks_overview}

Em um plano de implementação para um pipeline composto, uma tarefa representa alguma atividade de negócios significativa que está associada a uma implementação de software. As tarefas são definidas em planos de implementação.

{:shortdesc}

A maioria das tarefas possui um ponto de início, um ponto final e uma duração mensurável. Uma tarefa pode ser de um dos tipos a seguir:

<ul>
<li>Tarefas manuais podem representar qualquer atividade que esteja associada a uma implementação de software, como colocar um servidor off-line ou atualizar um banco de dados.</li>
<li>Tarefas do UrbanCode Deploy representam apps do IBM&reg; UrbanCode&reg; Deploy. É possível executar apps do IBM UrbanCode Deploy com tarefas do tipo do IBM UrbanCode Deploy.</li>
<li>Tarefas do Continuous Delivery Pipeline representam instâncias do {{site.data.keyword.deliverypipeline}}, que fazem parte do {{site.data.keyword.contdelivery_full}}. É possível gerenciar as instâncias do {{site.data.keyword.deliverypipeline}} com esse tipo de tarefa.</li>
<li>Tarefas atrasadas representam eventos críticos que acontecem em um momento específico.</li>
<li>Tarefas de cabeçalho são elementos organizacionais. Por exemplo, é possível usar uma tarefa de cabeçalho para identificar um grupo de tarefas.</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## Criando Tarefas
{: #tasks_create}

Ao criar uma tarefa, você seleciona o plano de implementação no qual deseja incluir a tarefa. Por padrão, novas tarefas são inseridas no final do plano de implementação. Após a criação de uma tarefa, é possível movê-la ou copiá-la e colá-la em outro plano de implementação. Também é possível criar dependências com outras [tarefas](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies).

Depois de salvar uma tarefa, ícones de ação são exibidos para a tarefa. É possível usar os ícones de ação para mudar o status da tarefa durante uma implementação. Todas as tarefas possuem o ícone de ação **Ignorar**. Outros ícones, como **Iniciar**, são exibidos quando o contexto é apropriado para eles.

![](../UCCR/images/deploy-plan-intro.png "Plano de implementação típico")

*Figura 1. Um plano de implementação simples com tarefas e ícones de ação*

Cada tarefa em um plano de implementação está contido em uma linha separada. As informações exibidas para cada tarefa estão descritas na tabela a seguir.

### Tabela 1. Propriedades da tarefa

| Property  | Descrição  |
| ------------------ | ------------------ |
| Nome               |Nome da Tarefa       |
| Tipo               |Tipo de tarefa: Manual, Continuous Delivery Pipeline, Atrasada, E-mail, Cabeçalho/Nota, UrbanCode Deploy|             
| Status             |Status da tarefa: não iniciada, concluída, com falha, ignorada, não aplicável |
| Proprietário              |Pessoa a quem a tarefa é designada                                                        |
| Horário de início  |Horário de início ou horário de início esperado com base no início planejado ou na duração estimada de outras tarefas        |
| Horário de término               |Horário em que a tarefa foi resolvida        |
| Duração               |Período de tempo do início da tarefa à resolução da tarefa (em minutos)        |
| Dependências.               |Número de tarefas que são pré-requisitos para a tarefa e dependentes da tarefa        |

---
Após a inclusão das tarefas nos planos de implementação, é possível gerenciá-las de várias maneiras:

   * Para mover uma tarefa, arraste-a para um novo local.

   * Para copiar uma tarefa ou um grupo, clique na tarefa, clique no ícone **Copiar** <img class="inline" src="../UCCR/images/copy-group.png"  alt="ícone copiar">, coloque o cursor onde deseja inserir a tarefa copiada e clique no ícone **Colar** <img class="inline" src="../UCCR/images/paste-group.png"  alt="ícone colar">.

   * Para recortar uma tarefa ou um grupo de um plano de implementação, clique na tarefa e clique em **Recortar** <img class="inline" src="../UCCR/images/cut-group.png"  alt="ícone recortar">.

   * Para excluir uma tarefa, clique nela e clique em **Excluir** <img class="inline" src="../UCCR/images/trash-group.png"  alt="ícone excluir">. A tarefa é removida do plano de implementação.

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## Criando tarefas manuais
{: #tasks_manual}

Geralmente, as tarefas manuais representam alguma atividade que está associada a uma liberação de software que tem um ponto de início, um ponto final e uma duração mensurável.

Para criar uma tarefa manual, siga estas etapas:

1. Na página Detalhes do plano de implementação, clique em **Criar tarefa**. Para inserir uma tarefa em uma posição específica no plano, antes de clicar em **Criar tarefa**, selecione uma tarefa. A nova tarefa é inserida acima da tarefa selecionada.

1. Na janela Criar tarefa, na lista **Tipo**, selecione **Manual**.

1. No campo **Nome**, digite um nome para a tarefa.

3. No campo **Duração (minutos)**, digite o número de minutos que você espera que a tarefa seja executada até que seja concluída. A duração estimada é usada para calcular os tempos de implementação esperados.

3. Na lista **Tags**, anexe uma tag à tarefa. É possível selecionar diversas identificações. Para criar uma tag, digite o nome da tag no campo de texto da lista.

3. Na lista **Grupos e usuários designados**, designe a tarefa a um usuário ou um grupo. O usuário designado executa a tarefa durante a implementação.

3. Na lista **Proprietário**, selecione o proprietário da tarefa. O proprietário padrão é o usuário que criou a tarefa. A lista **Proprietário** é exibida depois que a tarefa é designada a um usuário ou um grupo.    

5. Clique em **Salvar**. A tarefa é inserida no plano de implementação.

## Criando tarefas atrasadas
{: #tasks_delayed}

As tarefas do tipo atrasada representam marcos ou eventos críticos durante uma implementação. Com as tarefas atrasadas, é possível assegurar que tarefas importantes sejam iniciadas no momento esperado. Geralmente, as tarefas atrasadas são pré-requisitos para outras tarefas importantes.

Uma tarefa atrasada inicia assim que esteja elegível para ser executada e é concluída em um horário especificado pelo usuário. Uma tarefa do tipo atrasada iniciada possui um status de "Em andamento" até atingir seu horário planejado, quando seu status muda para "Concluído". Quando uma tarefa atrasada é concluída, as tarefas que dependem dela começam a ser executadas.

Para criar uma tarefa atrasada, siga estas etapas:

1. Na página Detalhes do plano de implementação, clique em **Criar tarefa**. Se desejar inserir uma tarefa em uma posição específica no plano, antes de clicar em **Criar tarefa**, selecione uma tarefa. A nova tarefa é inserida acima da tarefa selecionada.

1. Na janela Criar tarefa, na lista **Tipo**, selecione **Atrasada**.

1. No campo **Nome**, digite um nome para a tarefa.

3. No campo **Horário**, insira ou selecione o horário em que a tarefa será concluída.

3. Na lista **Fuso horário**, selecione o fuso horário para o valor que será inserido no campo **Horário**.    

5. Clique em **Salvar**. A tarefa é inserida no plano de implementação.

## Criando tarefas de cabeçalho
{: #tasks_header}

As tarefas de cabeçalho representam elementos da organização que podem ser incluídos em planos de implementação. Se você criar um grupo de tarefas, será possível identificar o grupo com uma tarefa de cabeçalho. As tarefas de cabeçalho podem ter dependências como qualquer outra tarefa.

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

Para criar uma tarefa de cabeçalho, siga estas etapas:

1. Na página Detalhes do plano de implementação, clique em **Criar tarefa**. Se desejar inserir uma tarefa em uma posição específica no plano, antes de clicar em **Criar tarefa**, selecione uma tarefa. A nova tarefa é inserida acima da tarefa selecionada.

1. Na janela Criar tarefa, na lista **Tipo**, selecione **Cabeçalho**.

1. No campo **Nome**, digite um nome para a tarefa. O nome pode representar um nome do grupo de tarefas.

3. No campo **Descrição**, digite ou cole uma descrição. É possível inserir uma nota, um lembrete ou outras instruções.

5. Clique em **Salvar**. A tarefa é inserida no plano de implementação.

## Criando tarefas do Delivery Pipeline
{: #tasks_pipelineCD}

No serviço {{site.data.keyword.contdelivery_short}}, o {{site.data.keyword.deliverypipeline}} automatiza os fluxos de trabalho do DevOps. É possível gerenciar as instâncias do {{site.data.keyword.deliverypipeline}} com tarefas de pipeline.

Para criar uma tarefa do Delivery Pipeline, siga estas etapas:

1. Na página Detalhes do plano de implementação, clique em **Criar tarefa**. Se desejar inserir uma tarefa em uma posição específica no plano, antes de clicar em **Criar tarefa**, selecione uma tarefa. A nova tarefa é inserida acima da tarefa selecionada.

1. Na janela Criar tarefa, na lista **Tipo**, selecione **Continuous Delivery Pipeline**.

1. No campo **Nome**, digite um nome para a tarefa. O nome pode representar um nome do grupo de tarefas.

3. No campo **Descrição**, digite ou cole uma descrição. É possível inserir uma nota, um lembrete ou outras instruções.

3. No campo **ID do pipeline**, digite ou cole o ID do pipeline.

3. No campo **Nome do estágio**, digite ou cole o nome do estágio.

5. Clique em **Salvar**. A tarefa é inserida no plano de implementação.

## Gerenciando grupos de tarefas
{: #tasks_groups}

É possível combinar duas ou mais tarefas em um grupo de tarefas. Ao criar um grupo, você define o padrão de execução do grupo, que é sequencial ou paralelo. É possível executar as tarefas em um grupo de padrão paralelo em qualquer ordem e podem ser executadas simultaneamente, a menos que existam dependências. As tarefas em grupos sequenciais são feitas na ordem da lista, começando com a primeira tarefa ou a tarefa mais elevada.

É possível integrar grupos em outros grupos. É possível integrar um grupo de padrão sequencial em um grupo de padrão paralelo e vice-versa. No entanto, não é possível integrar um grupo de padrão sequencial em outro grupo sequencial ou integrar um grupo de padrão paralelo em outro grupo paralelo.  

Para criar um grupo de tarefas, siga estas etapas:

1. Na página Detalhes do plano de implementação, selecione duas ou mais tarefas.

1. Dependendo do tipo de grupo que você deseja criar, conclua uma destas etapas:

  <ul>
  <li>Para criar um grupo paralelo, clique no ícone **Paralelo** <img class="inline" src="../UCCR/images/para-icon.png"  alt="ícone de grupo paralelo">. Se não for possível criar um grupo paralelo com as tarefas selecionadas, o ícone será desativado. Por exemplo, talvez você não possa criar um grupo paralelo caso todas as tarefas selecionadas já estejam em um grupo paralelo.
</li>
  <li>Para criar um grupo sequencial, clique no ícone **Sequencial** <img class="inline" src="../UCCR/images/seq-icon.png"  alt="ícone de grupo sequencial">.
  </li>
  </ul>

O grupo é formado e uma barra de seleção de grupo é incluída no plano de implementação. Se você tiver selecionado tarefas não contíguas, as tarefas formarão uma lista contígua que iniciará com a tarefa mais elevada selecionada.

A figura a seguir mostra um grupo paralelo. A barra de seleção do grupo identifica o tipo de grupo: paralelo <img class="inline" src="../UCCR/images/para-select.png"  alt="seleção de grupo paralelo"> ou sequencial <img class="inline" src="../UCCR/images/seq-select.png"  alt="seleção de grupo sequencial">.

(![](../UCCR/images/group-select.png "Plano de implementação típico"))

*Figura 2. Um grupo paralelo*

Para mover um grupo, clique na **barra de seleção de grupo** ou clique em qualquer lugar no grupo e arraste-o para um novo local.

Para copiar um grupo, selecione o grupo, clique no ícone **Copiar** <img class="inline" src="../UCCR/images/copy-group.png"  alt="ícone copiar">, coloque o cursor onde deseja inserir o grupo copiado e clique em **Colar** <img class="inline" src="../UCCR/images/paste-group.png"  alt="ícone colar">.

Para recortar um grupo, selecione o grupo e clique no ícone **Recortar** <img class="inline" src="../UCCR/images/cut-group.png"  alt="ícone recortar">.

Para desagrupar um grupo, selecione o grupo e clique no ícone **Desagrupar** <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="ícone desagrupar"> na barra de seleção de grupo.

Para excluir as tarefas que estão em um grupo, selecione o grupo e clique no ícone **Excluir** <img class="inline" src="../UCCR/images/trash-group.png"  alt="ícone excluir">. As tarefas são removidas do plano de implementação.

## Gerenciando tags de tarefas
{: #tasks_tags}

As tarefas estão organizando elementos que podem ser incluídos em tarefas. É possível filtrar planos de implementação por tag. Por exemplo, durante uma implementação para um ambiente de produção, é possível desativar as tarefas que incluem a tag `DEV_only`, que indica que as tarefas são apenas para o ambiente de desenvolvimento.

Para incluir uma tag em uma tarefa, siga estas etapas:

1. Na página Detalhes do plano de implementação, selecione uma tarefa ou um grupo de tarefas e clique em **Gerenciar tags**  <img class="inline" src="../UCCR/images/task-tag.png"  alt="gerenciar tags">. É possível selecionar múltiplas tarefas e grupos.

1. Na janela "Gerenciar tags para tarefas selecionadas", na lista **Tags comuns**, selecione as tags. É possível criar uma tag digitando um nome na caixa de texto da lista.

1. Clique em **Salvar**.

As tags são exibidas nas linhas da tarefa da página Detalhes do plano de implementação. Na figura a seguir, a tarefa Implementar WAR tem duas tags: `Deployment` e `Critical`.

As tags que são usadas por um plano de implementação são exibidas na guia **Versões** da página Detalhes do plano de implementação. Para renderizar uma tarefa para que não seja aplicável a uma implementação, limpe as tags da tarefa. Tarefas com o status "Não aplicável" não podem ser iniciadas.  

![](../UCCR/images/task-tag-labels.png "Plano de implementação típico")

*Figura 3. Tags de tarefas*

## Criando dependências de tarefa
{: #tasks_dependencies}

É possível tornar uma tarefa um pré-requisito para outras tarefas. Se uma tarefa for um pré-requisito, as tarefas dependentes não poderão ser iniciadas, mesmo se, de outra forma, forem elegíveis, até que a tarefa de pré-requisito seja resolvida.

Uma tarefa pode ter múltiplas tarefas dependentes e múltiplas tarefas de pré-requisito. É possível definir dependências para uma tarefa com qualquer outra tarefa no plano de implementação. No entanto, você não pode criar dependências circulares. Por exemplo, não é possível tornar uma tarefa dependente de uma tarefa que já depende da primeira tarefa.

Ao controlar as dependências de tarefas, é possível assegurar que os eventos ocorram em sua ordem esperada.

Para tornar uma tarefa um pré-requisito para outras tarefas, conclua estas etapas:

1. Na página Detalhes do plano de implementação, selecione uma tarefa ou um grupo de tarefas e clique em **Gerenciar pré-requisitos** <img class="inline" src="../UCCR/images/task-depend.png"  alt="pré-requisito de tarefa">. É possível selecionar múltiplas tarefas e grupos.

1. Na janela "Gerenciar pré-requisitos para tarefas selecionadas", na lista **Tarefas de pré-requisito para tarefas selecionadas**, selecione a tarefa de pré-requisito.

1. Clique em **Salvar**.

As dependências de tarefas são mostradas na coluna Dependências na página Detalhes do plano de implementação. As setas para cima indicam pré-requisitos de tarefas; as setas para baixo indicam dependências de tarefas.

Na figura a seguir, a primeira tarefa não possui pré-requisitos e duas tarefas dependem dela. A segunda tarefa possui uma tarefa de pré-requisito e nenhuma tarefa depende dela.

(![](../UCCR/images/plan-w-depend.png "Plano de implementação típico"))

*Figura 4. Dependências de tarefa*

Para revisar ou modificar dependências, selecione a tarefa e clique em **Gerenciar pré-requisitos** <img class="inline" src="../UCCR/images/task-depend.png"  alt="pré-requisito de tarefa">.
