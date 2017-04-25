---

copyright:
  years: 2017
lastupdated: "2017-4-5"
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

# Trabalhando com pipelines compostos (Experimental)
{: #deliverypipeline_create_composite}

Com o recurso de pipeline composto para o {{site.data.keyword.deliverypipeline}}, é possível gerenciar processos repetidos de integração contínua e de entrega contínua para apps de software relacionados.
{:shortdesc}

Você cria pipelines compostos para gerenciar os apps em uma cadeia de ferramentas. Se a sua cadeia de ferramentas contiver apps implementados pelo {{site.data.keyword.deliverypipeline}}, a cadeia de ferramentas será atualizada dinamicamente quando você incluir ou remover pipelines de entrega da cadeia de ferramentas. Também é possível incluir apps de fontes externas no pipeline composto.

## Criando um pipeline composto
{: #compositepipeline_create_for_toolchain}

1. No menu perto do logotipo do Bluemix, clique em **Serviços > DevOps**

1. Na navegação esquerda, clique em **Pipelines**.

2. Ative o recurso de pipeline composto clicando em **Saiba mais** e, em seguida, clicando em **Ativar**. O pipeline composto é ativado para cada usuário, portanto, apenas os membros de sua organização (org) que optarem por participar do recurso experimental verão os pipelines compostos criados.

2. Clique em **Criar** > **Pipeline composto**.

3. Digite um nome para o pipeline composto. Também é possível modificar a descrição do pipeline.

4. Na lista **Cadeia de ferramentas**, selecione uma cadeia de ferramentas.

    1. Para criar uma cadeia de ferramentas vazia e um pipeline composto, selecione **Novo**.

    2. Para criar um pipeline composto para uma das cadeias de ferramentas, selecione seu nome.

5. Se você criar uma cadeia de ferramentas vazia, selecione **Incluir ambientes padrão**. Você usa esses ambientes lógicos padrão para controlar a execução do processo por meio do pipeline composto.

6. Clique em **Criar**.

Os estágios configurados são mapeados automaticamente para o espaço apropriado em sua organização e um plano de implementação é criado para o pipeline composto.

Se você tiver criado o pipeline composto para uma cadeia de ferramentas que contém pipelines de entrega, os apps para todos os pipelines na cadeia de ferramentas serão incluídos no pipeline composto. Os estágios configurados nos pipelines de entrega são mapeados automaticamente para os espaços apropriados em sua organização e seu status é exibido. Para visualizar o status de cada tarefa em um app, expanda o app.

Um plano de implementação também é criado para o pipeline composto. Por padrão, as tarefas para todos os apps são executadas em paralelo para um espaço, mas é possível mudar a ordem de implementação dos apps no plano.

Se você tiver criado o pipeline composto para uma nova cadeia de ferramentas, um plano de implementação será criado para customização.

![Expanda cada app para visualizar cada tarefa em seu pipeline](images/composite_view.png "expandir cada app")

## Modificando o plano de implementação
{: #compositepipeline_modify_dp}

Por padrão, um plano de implementação é criado para um pipeline composto. Esse plano de implementação captura todas as informações sobre os estágios em qualquer Delivery Pipeline na cadeia de ferramentas. É possível visualizar e modificar o plano de implementação de cada estágio.

No estágio para o qual você deseja modificar o plano de implementação, clique no menu e, em seguida, em **Plano de implementação**.

![Abra o plano de implementação](images/open_deployment_plan.png "abrir o plano de implementação")

A lista de tarefas de implementação para seu ambiente é exibida.

![Plano de implementação padrão para um pipeline composto que contém três pipelines individuais](images/composite_deploy_plan.png)

Para obter mais informações sobre como modificar o plano de implementação, veja [Customizando planos de implementação para pipelines compostos](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html).

## Modificando pipelines individuais
{: #compositepipeline_add_job}

É possível modificar pipelines individuais por meio do pipeline composto.

1. Expanda o app.

2. No menu no estágio, clique em **Configurar**.

3. Inclua, modifique ou exclua tarefas do estágio. Para obter instruções detalhadas, veja [Incluindo uma tarefa em um estágio](pipeline_build_deploy.html#deliverypipeline_add_job).

## Executando tarefas em um pipeline composto
{: #compositepipeline_run_jobs}

Depois de expandir um app para exibir suas tarefas, será possível executar manualmente todas as suas tarefas em um estágio. Clique no ícone **Implementar no *estágio*** no espaço de um app.

![Executando um estágio em um único app](images/composite_run_stage.png)

Para executar todas as tarefas em todos os apps que estão em um espaço, clique no ícone **Implementar no *espaço*** no espaço do pipeline composto.

![Executando um estágio em todos os apps](images/composite_run_space.png)

As tarefas são executadas de acordo com o plano de implementação do blueprint composto.

## Exibindo logs
{: #compositepipeline_view_logs}

Para visualizar os logs de uma tarefa, expanda o app que contém a tarefa e clique na tarefa.

## Usando o IBM Bluemix DevOps Connect para se integrar ao IBM UrbanCode Deploy
{: #compositepipeline_devops_connect}

O IBM Bluemix DevOps Connect coordena a comunicação entre a instalação local do IBM&reg; UrbanCode&reg; Deploy e o {{site.data.keyword.contdelivery_short}}. Após a instalação do DevOps Connect, é possível criar integrações que possam ser usadas para gerenciar apps IBM UrbanCode Deploy com pipelines compostos.

**Pré-requisitos**

   * Para registrar o DevOps Connect, deve-se ter um IBMid.

   * Certifique-se de que o [Java&trade; Runtime Environment versão 8 atualização 121 ou mais recente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://java.com/en/download/){:new_window} esteja no sistema host e que a variável PATH do sistema esteja configurada para seu local.

   * Você precisará de um token de autorização de administrador do IBM UrbanCode Deploy.

Para usar o DevOps Connect para se integrar ao IBM UrbanCode Deploy, siga estas etapas:

1. Instale o DevOps Connect e use-o para integrar sua organização ao IBM UrbanCode Deploy.

  1. Em um pipeline composto, clique em **Incluir app**. Na lista **Gerenciado por**, selecione **IBM UrbanCode Deploy**.

  1. Exiba as etapas de integração. Se você vir uma lista de apps, primeiro clique no ícone de informações (![Ícone de informações](/images/info.png)) por **Apps** e, em seguida, clique em **Configurar o IBM UrbanCode Deploy para esta organização**.

  1. Na janela Configurar a integração do UrbanCode Deploy, clique em **Download** para fazer download do DevOps Connect. Coloque o arquivo JAR em um computador que tenha acesso ao IBM UrbanCode Deploy.

  1. Na janela, copie o script de instalação do DevOps Connect. O script contém o comando para iniciar o DevOps Connect e as credenciais que são necessárias para identificar o serviço {{site.data.keyword.contdelivery_short}}.

  1. No computador no qual o DevOps Connect foi colocado, abra um shell de comando e cole o script copiado nele.

  1. Execute o script. O DevOps Connect exibe mensagens de inicialização.

1. Registre o DevOps Connect.

  1.  No computador no qual o DevOps Connect foi colocado, abra um navegador da web para abrir o painel do DevOps Connect. A URL padrão é https://localhost:8443. Para mudar a URL e conhecer outras opções de inicialização, veja a [documentação do DevOps Connect ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window}.


1. Na página "Conectar-se à IBM", insira seu IBMid e senha e clique em **Conectar**. Você se conecta toda vez que inicia o DevOps Connect.

1. Com o DevOps Connect, use o plug-in IBM UrbanCode Deploy for DevOps Connect para criar uma integração entre sua organização e o IBM UrbanCode Deploy.

    1. Na página Integrações, clique em **Incluir novo**.

    1. No campo **Nome**, digite um nome para a integração.

    1. Na lista **Tipo de integração**, selecione **IBM UrbanCode Deploy for DevOps Connect**.

    1. No campo **URI do servidor**, digite a URL pública do servidor IBM UrbanCode Deploy; por exemplo, `https://my_UCD.example.com:8443`.

    1. No campo **Token de autenticação**, digite ou cole o token de autenticação que foi gerado pelo IBM UrbanCode Deploy.

    1. No campo **E-mail do usuário administrativo**, digite seu endereço de e-mail.

    1. Para confirmar que a integração foi bem-sucedida, clique em **Executar integração**. O DevOps Connect conecta-se à instância do IBM UrbanCode Deploy especificada no campo **URI do servidor**. O DevOps Connect é autorizado pelo token colado no campo **Token de autenticação**.

    1. Clique em **Salvar**.

Se a sua integração tiver sido bem-sucedida, será possível incluir apps IBM UrbanCode Deploy nos pipelines compostos. Para obter mais informações, veja [Incluindo apps do IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps).


## Incluindo apps do IBM UrbanCode Deploy
{: #compositepipeline_add_apps}

Se você for membro de uma organização que tenha se integrado ao IBM UrbanCode Deploy usando o DevOps Connect, será possível incluir os apps que podem ser acessados no IBM UrbanCode Deploy no pipeline composto. Para obter instruções de instalação, veja [Usando o IBM Bluemix DevOps Connect para se integrar ao IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect).

Quando você for membro de uma organização que esteja conectada ao IBM UrbanCode Deploy, será possível incluir apps IBM UrbanCode Deploy aos pipeline compostos, selecionar os processos de app para incluir no plano de implementação e customizar a implementação dos apps.

1. No pipeline composto, clique em **Incluir app**.

2. Na lista **Gerenciado por**, selecione **IBM UrbanCode Deploy**. Se recentemente você tiver integrado o {{site.data.keyword.contdelivery_short}} ao IBM UrbanCode Deploy, talvez seja necessário atualizar seu navegador para ver o servidor.

3. Selecione os apps a serem incluídos e clique em **Continuar**. Todos os processos de app que estiverem disponíveis para apps IBM UrbanCode Deploy serão mostrados. Entradas para executar os processos selecionados são incluídas no plano de implementação.

4. Selecione os processos de app a serem usados para os apps. Use as opções de procura e filtro para localizar os processos.

5. Clique em **Salvar**. Cada app IBM UrbanCode Deploy selecionado é exibido como um app no pipeline composto.

6. Mapeie ambientes dos apps IBM UrbanCode Deploy para ambientes lógicos do pipeline composto:

    1. No menu perto de um nome de ambiente lógico, selecione **Gerenciar ambientes lógicos**.

    ![Selecionando Gerenciar ambientes lógicos](images/composite_logical_env.png)

    2. Para cada app no pipeline composto, selecione ambientes definidos no IBM UrbanCode Deploy. Os processos de app selecionados são executados apenas nos ambientes desse app.

    3. Clique em **Salvar**.

    4. Repita essas etapas para cada ambiente lógico que você usar.
