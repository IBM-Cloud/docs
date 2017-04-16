---

copyright:
  years: 2015, 2016

---

<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Estendendo o serviço {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_extending}
Última atualização: 29 de agosto de 2016
{: .last-updated}

É possível estender os recursos do serviço
{{site.data.keyword.deliverypipeline}} configurando suas tarefas para usar
serviços suportados. Por exemplo, as tarefas de teste executam varreduras de código
estático e as tarefas de construção podem globalizar as sequências.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

As tarefas a seguir descrevem como integrar ferramentas selecionadas com um Pipeline de entrega.

## Executando varreduras de código estático usando o pipeline

{: #deliverypipeline_scan}

Deseja encontrar os problemas de segurança em seu código antes de implementá-lo? Ao
usar o IBM® Static Analyzer for Bluemix™ como parte do pipeline, é possível executar
verificações automatizadas com relação a seus arquivos binários de construção
`.war`, `.ear`, `.jar` ou
`.class` estáticos do seu app Java™.

Um pipeline que usa o serviço Analisador estático normalmente inclui estes estágios:

+ Um estágio de construção para construir os arquivos de origem
+ Um estágio de processamento que inclui estas tarefas:
  + Uma tarefa de construção para executar o serviço Analisador estático
  + Uma tarefa de compilação para executar uma compilação de
contêiner
+ Um estágio de implementação para implementar o contêiner


### Criando uma varredura de código estático

Antes de começar,
[revise os Termos
de uso do serviço](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01).

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Crie um estágio de processamento.

  a. Clique em **INCLUIR ESTÁGIO**.

  b. Nomeie o estágio, por exemplo, `Processamento`.

  c. Para o tipo de entrada, selecione **Artefatos de construção**.

  d. Para o estágio e a tarefa, verifique os valores e atualize-os se necessário.

2. No estágio de processamento, inclua uma tarefa de compilação
para executar a varredura de código.

  a. Na guia **TAREFAS**, clique em **INCLUIR TAREFA**.

  b. Para o tipo de tarefa, selecione **Teste**.

  c. Para o tipo de testador, selecione **IBM Security Static Analyzer**.

  d. Para a organização e o espaço, verifique os valores e atualize-os se necessário.

  e. Marque ou desmarque a caixa de seleção **Configurar serviço e espaço para mim** conforme necessário.

    * Se desejar que o pipeline verifique o espaço do Bluemix para o serviço e um
app que ligue o serviço ao contêiner, marque a caixa de seleção. Se o serviço ou o app
vinculado não existir, o pipeline incluirá o plano grátis do serviço em seu espaço. O
app vinculado que é criado se chama `pipeline_bridge_app`. Em
seguida, o pipeline usa as credenciais do pipeline_bridge_app para acessar os serviços
vinculados.

    * Se você já tiver configurado o serviço e o app vinculado em seu espaço do Bluemix, ou se quiser
[configurar
esses requisitos manualmente](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), deixe a caixa de seleção desmarcada.

  f. No campo **Minutos para aguardar a análise ser concluída**,
digite um valor de 0 a 59 minutos. O valor padrão é de 5 minutos. Uma URL para o painel
do Analisador estático está nos logs do console ao final da tarefa.

     Se a varredura do Analisador estático não for concluída antes do tempo
especificado, a tarefa falhará. No entanto, a análise da varredura continua a ser
executada e é possível visualizá-la no painel do Analisador estático. Uma vez
concluída a varredura do Analisador estático, se você executar novamente a tarefa, a
solicitação de varredura não será enviada novamente e a tarefa de pipeline poderá ser
concluída. Como alternativa, é possível configurar o pipeline para não ser bloqueado
no caso de um resultado de varredura bem-sucedida. Para obter instruções, consulte a
próxima etapa.

  g. Marque ou desmarque a caixa de seleção **Parar de executar este
estágio se esta tarefa falhar** dependendo do que você deseja que aconteça se
essa tarefa falhar ou atingir o tempo limite. As tarefas podem falhar quando as
vulnerabilidades são altas.

    * Se você marcar a caixa de seleção e a tarefa falhar, as tarefas posteriores
no estágio e nos estágios posteriores não serão executadas.

    * Se você desmarcar a caixa de seleção e a tarefa falhar, o estágio
continuará sem bloquear as tarefas e os estágios posteriores. Por exemplo, se você souber
que o relatório inclui muitos problemas a serem processados, poderá configurar o estágio
para continuar porque a varredura pode levar um longo tempo. Neste cenário, você pode não desejar que o
restante das tarefas e dos estágios parem apenas porque a
varredura está demorando muito.

  h. Clique em **SALVAR**.

3. Quando a tarefa for concluída, visualize os resultados clicando em
**Visualizar logs e histórico**. Se a análise for bem-sucedida ou
atingir o tempo limite, uma URL será mostrada nos resultados da varredura. Se o status da
varredura estiver pendente, aguarde até que a varredura seja concluída para ver os
resultados completos.

4. Se você precisar executar o estágio de processamento novamente antes que a
análise seja concluída, será possível. Entretanto, nas situações a seguir, uma nova
análise não será submetida novamente e os resultados anteriores serão usados:
  * O estágio de processamento ainda estava em execução quando você iniciou uma nova análise
  * Uma varredura já foi enviada para a construção
  * Uma nova construção de origem não foi executada ainda

5. Para iniciar uma nova análise, conclua uma destas etapas:
  * Execute o estágio de construção que entra no estágio de processamento e, em
seguida, execute o estágio de processamento novamente.
  * Abra a URL dos resultados da varredura e clique no ícone
**Lixeira**. Em seguida, execute o estágio de processamento novamente.

Exemplos de saída do
console:

**Varredura bem-sucedida**
![Exemplo de varredura bem-sucedida](images/analyzer_success.png)

**Varredura pendente**
![Exemplo de varredura pendente](images/analyzer_pending.png)

Para obter mais informações sobre como usar o serviço Analisador estático, [consulte as documentações do serviço Analisador estático](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## Criando notificações do Slack para construções no pipeline
{: #deliverypipeline_slack}

É possível enviar notificações sobre os resultados da construção do IBM Container
Service, IBM Security Static Analyzer e IBM Globalization do pipeline de entrega para os
canais do Slack.

Antes de iniciar, crie ou copie uma URL de WebHook do Slack:

1. Abra a página Integração do Slack para sua equipe: `https://_project_name_.slack.com/services`
2. Na lista de integrações, localize **WebHooks recebidos** e
clique em **Incluir**.
3. Selecione um canal e clique em **Incluir integração de WebHooks
recebidos**.
4. Inclua uma **URL de WebHook** ou copie uma existente.

Para obter mais informações,
[consulte WebHooks recebidos na
documentação do Slack](https://api.slack.com/incoming-webhooks).

Para criar notificações do Slack:

1. No pipeline, abra a configuração para um estágio.
2. Na guia **PROPRIEDADES DO AMBIENTE**, clique em **INCLUIR PROPRIEDADE**.
3. Selecione **Propriedade de texto**.
4. Insira o nome e um valor para a propriedade do ambiente. Repita para criar várias propriedades
de ambiente.

  *Tabela 1. Propriedades do ambiente para configurar notificações do Slack*

  <table>
  <tr>
  <th>Nome</th>
  <th>Valor</th>
  <th>Descrição</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>Um URL</td>
    <td>Necessária. A URL do WebHook que é salva nas configurações do seu Projeto do Slack.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>É possível inserir
um dos seguintes valores:
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>Qualquer cor hexadecimal, como #439FEO</li></ul></td>
    <td>Opcional. A cor da borda que é exibida com o lado da mensagem no Slack. As cores padrão são verde para mensagens válidas, vermelho para mensagens inválidas e cinza para
mensagens informativas.</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>Para receber somente um subconjunto dos tipos de mensagens, insira um dos valores a
seguir:
      <ul>
      <li><code>good</code>: obtenha somente mensagens desconhecidas, válidas e de informação. As mensagens inválidas não são
enviadas.</li>
      <li><code>bad</code>: obtenha todas as mensagens.</li>
      <li><code>info</code>: obtenha somente mensagens de informação. As mensagens válidas, inválidas e desconhecidas não são enviadas.</li>
      <li><code>unknown</code>: obtenha todas as mensagens.</li></ul>
      Exemplo: se você configurar <code>NOTIFY_FILTER = bad</code>, notificações de erro só serão exibidas no Canal do Slack.</td>
    <td>Opcional. Decida para que tipo de mensagens enviar notificações. Por
padrão, mensagens válidas e inválidas são enviadas, mas mensagens informativas não.
      <ul><li><code>good</code>: resultados de construção bem-sucedidos.</li>
      <li><code>bad</code>: resultados de construção malsucedidos.</li>
      <li><code>info</code>: mensagens informativas sobre o processo de construção.</li>
      <li><code>unknown</code>: mensagens desconhecidas não são designadas com um tipo.</li></ul></td>
   </table>

5. Clique em **Salvar**.

6. Repita estas etapas para enviar notificações do Slack para outros estágios que
incluam tarefas do IBM Container Service, IBM Security Analyzer e IBM Globalization.

A notificação de construção que é exibida no Slack inclui um link para o projeto de
serviços DevOps e às vezes para o painel do projeto. Para que um usuário do Slack abra
esses links, o usuário deve estar registrado nos serviços DevOps e ser membro do projeto
no qual o pipeline está configurado.

## Criando notificações do HipChat para construções no pipeline
{: #deliverypipeline_hipchat}

É possível enviar notificações sobre os resultados de construção do IBM Container
Service, IBM Security Static Analyzer e IBM Globalization do Pipeline de entrega para os
espaços do HipChat.

Antes de iniciar, crie ou copie um token do HipChat existente:

1. Acesse a página Conta do HipChat para sua equipe: `https://_project_name_.hipchat.com/account/api`
2. Crie um novo token ou use um existente.

Para criar notificações do HipChat:

1. No pipeline, abra a configuração para um estágio.
2. Na guia **PROPRIEDADES DO AMBIENTE**, clique em
**INCLUIR PROPRIEDADE**.
3. Selecione **Propriedade de texto**.
4. Insira o nome e um valor para a propriedade do ambiente. Repita para criar várias propriedades
de ambiente.

  *Tabela 2. Propriedades do ambiente para configurar notificações do HipChat*

  <table>
  <tr>
  <th>Nome</th>
  <th>Valor</th>
  <th>Descrição</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>Sequência alfanumérica</td>
    <td>Necessária. Consulte "Antes de iniciar" para obter instruções sobre como criar ou
copiar um token do HipChat existente.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>Nome da sala</td>
    <td>Necessária.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>Digite
um dos seguintes valores:
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>verde</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>Opcional: especifique a cor do plano de fundo e a cor da borda das notificações
do HipChat. Se você configurar <code>HIP_CHAT_COLOR</code>, não precisará especificar a cor quando chamar o script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>Digite
um dos seguintes valores:
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    Essa variável se aplica às cores de notificação do HipChat e do Clack. Se você
especificar <code>NOTIFICATION_COLOR</code>, não será necessário especificar
<code>HIP_CHAT_COLOR</code> ou <code>SLACK_COLOR</code>.</td>
    <td>Opcional: especifique a cor do plano de fundo e a cor da borda das notificações
do HipChat e do Slack. Se você configurar <code>NOTIFICATION_COLOR</code>, não precisará especificar a cor quando chamar o script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>Digite
um dos seguintes valores:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>Opcional: Especifique o nível de notificação. Consulte
<code>NOTIFICATION_FILTER</code> para obter mais detalhes sobre o que aciona a
notificação.</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>Digite
um dos seguintes valores:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>Opcional: Especifique o nível do filtro de notificação. As notificações são enviadas quando
os parâmetros a seguir são atendidos:
      <ul><li><code>NOTIFICATION_FILTER = good</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> e <code>NOTIFICATION_LEVEL = bad</code> ou <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> ou <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. Clique em **Salvar**.

6. Repita estas etapas para enviar notificações do HipChat para outros estágios
que incluam tarefas do IBM Container Service, IBM Security Static Analyzer e IBM
Globalization.

## Usando o Active Deploy para implementação com tempo de inatividade zero no pipeline
{: #deliverypipeline_activedeploy}

É possível automatizar a implementação contínua dos seus apps ou grupos de
contêiner usando o serviço IBM® Active Deploy no Pipeline de entrega se serviços do Bluemix®
DevOps. Para obter mais informações sobre introdução,
[consulte
a documentação do Active Deploy](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## Construindo e implementando imagens de contêiner com o pipeline
{: #deliverypipeline_containers}

É possível automatizar construções de apps e implementações de contêiner no
Bluemix® usando o IBM® Continuous Delivery Pipeline for Bluemix. O serviço Pipeline de entrega nos serviços DevOps suporta:
  - Compilando imagens do Docker
  - Implementando imagens em contêineres no Bluemix

Para obter mais informações sobre introdução, consulte
[a
visão geral de Pipeline de entrega e contêineres](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov).
