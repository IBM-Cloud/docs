---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Perigo De disposição
{: #gettingstarted}

O {{site.data.keyword.DRA_short}} fornece uma riqueza de informações sobre suas implementações, especificamente de risco. É possível usá-lo para automatizar a proteção de qualidade em seu pipeline de entrega usando políticas e portas. 
{:shortdesc}

Depois de abrir o {{site.data.keyword.DRA_short}} por meio de sua cadeia de ferramentas, clique em **Deployment Risk**. Daí, é possível obter uma visão geral dos aplicativos nos ambientes de preparação e produção e realizar drill down para entender os relatórios de cobertura de código, de desempenho de teste e de segurança. Os painéis são preenchidos automaticamente com as informações mais recentes dos testes do {{site.data.keyword.DRA_short}} dos pipelines.

## Sobre o Deployment Risk
{: #about}

É possível usar o Deployment Risk para utilizar as normas de qualidade em sua cadeia de ferramentas por meio de políticas e portas. As políticas incluem conjuntos de regras; as portas utilizam políticas. Por exemplo, é possível criar uma política "Teste de unidade e Cobertura de teste" que requer que as construções atendam às normas de teste de unidade e de cobertura de teste. Em seguida, você inclui uma porta que se refere à política de seu processo de entrega contínua. As construções que não satisfizerem a política serão paradas nessa porta. 

O Deployment Risk funciona com o {{site.data.keyword.deliverypipeline}}, que faz parte do {{site.data.keyword.contdelivery_full}} e com projetos Jenkins. Em um alto nível, as instruções para usar um ou outro são semelhantes.  

Se você estiver usando o {{site.data.keyword.deliverypipeline}}, siga estas etapas:

1. [Crie políticas e regras](#policies_and_rules) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Prepare os estágios de seu pipeline](#integrate_pipeline) para integração ao {{site.data.keyword.DRA_short}}.

3. [Crie ou edite tarefas de teste](#configure_pipeline_jobs) no pipeline que façam upload de resultados no {{site.data.keyword.DRA_short}}.
4. [Inclua portas](#configure_pipeline_gates) no pipeline que tomem decisões de promoção com base nesses resultados e suas políticas.
5. Execute o pipeline e [visualize os resultados](#view_results).

Se estiver usando o Jenkins, siga estas etapas:

1. [Crie políticas e regras](#policies_and_rules) para o {{site.data.keyword.DRA_short}} gerenciar.
2. [Instale e configure o plug-in do Jenkins](#integrate_jenkins).
3. [Crie tarefas de teste e portas conforme descrito nas instruções do plug-in](#integrate_jenkins). Os testes fazem upload dos resultados no {{site.data.keyword.DRA_short}} para análise e as portas usam esses resultados para tomar decisões de promoção.
4. Execute o projeto e [visualize os resultados](#view_results). 

Independentemente de como você construir e implementar seu código, os resultados serão os mesmos: as construções que atenderem às normas serão movidas depois das portas do Deployment Risk e as construções que não atenderem às normas serão paradas. 

## Pré-Requisitos
{: #prerequisites}

O Deployment Risk requer alguma configuração além daquela descrita em [Introdução ao {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para usar o Deployment Risk, você precisa de duas coisas:

* Uma instância do {{site.data.keyword.deliverypipeline}} ou um projeto Jenkins
* Testes que você deseja usar para avaliar seu projeto

## Criando políticas e regras
{: #policies_and_rules}

As políticas são conjuntos de regras que controlam as portas em seu pipeline de entrega. Se o seu código não atender nem exceder uma política executada em uma porta específica, a implementação será interrompida para evitar que as mudanças de risco sejam liberadas.

As políticas são definidas no {{site.data.keyword.DRA_short}}. As políticas são criadas na organização (org.) do {{site.data.keyword.Bluemix_notm}} que contém o {{site.data.keyword.DRA_short}}. Qualquer aplicativo que estiver na mesma organização poderá usar a política. 

### Criando políticas
{: #create_policies}

Para criar uma política:

1. Na navegação à esquerda, clique em **Configurações**.

2. Clique em **Políticas**.

3. Clique em **Criar política** e, em seguida, digite um nome e uma descrição para a nova política.

4. Clique em **Avançar**.

4. Inclua pelo menos uma regra na política:
  1. Clique em **Incluir regra na política**.
  2. Selecione o tipo de regra.
  3. Insira detalhes e condições para a regra.
  4. Clique em **Salvar**.

5. Ao concluir a inclusão de regras na política, clique em **Concluído**.

### Criando regras
{: #creating_rules}

As regras definem os critérios que suas políticas usam para julgar o sucesso ou a falha. É possível criar uma política "Teste de unidade e Cobertura de teste" que contenha uma regra de teste de unidade que requeira um sucesso de 80% de teste de unidade e uma regra de cobertura de teste que requeira 100% de cobertura de código. Se você incluir uma porta que se refira a essa regra em um pipeline, a porta evitará que quaisquer construções que não satisfaçam a ambas as regras continuem. 

É possível requerer o sucesso sem importar o quê marcando os testes como críticos. Para criar uma regra, selecione uma política e, em seguida, clique em **Incluir regra na política**. 

#### Criando regras de teste de verificação funcional
{: #criteria_fvt}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


#### Criando regras de teste de unidade
{: #criteria_ut}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


#### Criando regras de cobertura de código
{: #criteria_codecoverage}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de cobertura de código que é necessária para ser declarada bem-sucedida.

3. Para monitorar para regressões de cobertura de código, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

4. Clique em **Salvar**.

#### Criando regras de varredura de segurança estática
{: #criteria_static}

É possível integrar o {{site.data.keyword.DRA_short}} ao IBM Application Security on Cloud para executar varreduras de código estático e de app dinâmico. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

#### Criando regras de varredura de segurança dinâmica
{: #criteria_dynamic}

É possível integrar o {{site.data.keyword.DRA_short}} ao {{site.data.keyword.appseccloudfull}} para executar varreduras de apps dinâmicos. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

## Configurando o {{site.data.keyword.deliverypipeline}} 
{: #configuration}

Depois de incluir o {{site.data.keyword.DRA_short}} em uma cadeia de ferramentas e definir as políticas que ele monitora, integre-o a um {{site.data.keyword.deliverypipeline}}. Para obter mais informações sobre pipelines, veja [a documentação oficial](/docs/services/ContinuousDelivery/pipeline_working.html).

### Preparando estágios de pipeline
{: #integrate_pipeline}

Para que o Deployment Risk analise seu projeto, deve-se definir estágios de preparação e de produção em seu pipeline. Você define os estágios usando propriedades do ambiente de texto, que podem ser localizadas no menu de configuração de cada estágio ![Ícone Configuração de estágio de pipeline](images/pipeline-stage-configuration-icon.png) em **Propriedades do ambiente**.

1. No estágio de preparação, configure a propriedade `LOGICAL_ENV_NAME` como `STAGING`. 

2. No estágio de produção, configure a propriedade `LOGICAL_ENV_NAME` como `PRODUCTION`. 

Também é possível incluir as propriedades a seguir em estágios que constroem ou implementam seu app:

* `LOGICAL_APP_NAME`, que define o nome do app no painel.
* `BUILD_PREFIX`, que define o texto que é incluído nas construções do estágio. Esse texto também é mostrado no painel. 

### Incluindo tarefas de teste
{: #configure_pipeline_jobs}

Você integra o {{site.data.keyword.DRA_short}} a seu pipeline usando dois tipos de tarefas de teste: aqueles que fazem upload dos resultados no {{site.data.keyword.DRA_short}} para análise e portas que agem nessa análise. 

Primeiramente, você inclui tarefas do Testador avançado em seu pipeline para executar testes e fazer upload dos resultados. 

**Nota:** se desejar atualizar uma tarefa de teste para fazer upload dos resultados no {{site.data.keyword.DRA_short}}, salve suas configurações em um local conveniente antes de continuar. Em seguida, abra seu menu de configuração de tarefa e vá para a etapa 3. 

1. No estágio no qual você deseja incluir a tarefa que faz upload dos resultados, clique no ícone **Configuração de estágio** ![Ícone Configuração de estágio de pipeline](images/pipeline-stage-configuration-icon.png). Clique em **Configurar
estágio**.
2. Crie uma tarefa de teste e digite um nome para ela. 
3. Para o tipo de tarefa, selecione **Testador avançado**.
4. Preencha os campos **Comando de teste** e **Diretório ativo** como você faria para uma tarefa de teste de pipeline normal. 
5. Preencha os campos restantes para fazer upload dos resultados de teste para um tipo de teste específico. 

 1. Escolha o tipo de métrica que corresponde ao que você definiu na política do {{site.data.keyword.DRA_short}} que deseja usar.
 2. Digite um local do arquivo de resultado. Esse local é relativo ao diretório ativo. 

6. Se desejar fazer upload dos resultados para um segundo tipo de teste na mesma tarefa, preencha os campos prefixados com *Adicional*.
7. Clique em **Salvar** para retornar para o pipeline.

Os valores para os campos de **Tipo de métrica** e de **Local do arquivo de resultado** devem corresponder ao formato
correto:

<table><thead>
<tr>
<th>Tipo de métrica</th>
<th>Formatos suportados</th>
</tr>
</thead><tbody>
<tr>
<td>Teste de verificação funcional</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Teste unitário</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura do Código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

A Figura 1 mostra uma tarefa de teste que está configurada para executar testes de unidade, fazer upload dos resultados no formato Mocha e fazer upload dos resultados da cobertura de código no formato Istanbul.

![Tarefa de upload do DevOps Insights](images/insights_upload_job.png)
*Figura 1. Resultados de upload para o DevOps Insights*

### Definindo portas
{: #configure_pipeline_gates}

As portas do {{site.data.keyword.DRA_short}} verificam se os resultados do teste obedecem à política definida. Se a política não for atendida, a porta do {{site.data.keyword.DRA_short}} falhará, por padrão. Também é possível configurar portas para agir em uma função consultiva para permitir a progressão de pipeline mesmo após falha.

O painel Deployment Risk depende da presença de uma porta após uma tarefa de implementação temporária. Se desejar usar o painel, certifique-se de que tenha uma porta depois de implementar no ambiente temporário, mas antes de implementar em um ambiente de produção.

Geralmente, as portas são colocadas antes da promoção de construção em seu pipeline. Esses locais são ideais para verificar a qualidade da construção com relação a suas políticas, para assegurar que é seguro promover de um ambiente para outro. No entanto, é possível
colocar portas em qualquer lugar no pipeline nas quais você deseja que um critério específico seja verificado. As portas que forem colocadas antes da implementação em um ambiente temporário continuarão a utilizar políticas, mas não aparecerão no painel Deployment Risk.

1. Em um estágio, clique no ícone **Configuração de estágio** ![Ícone Configuração
de estágio de pipeline](images/pipeline-stage-configuration-icon.png) e clique em Configurar estágio.
2. Clique em **Incluir Tarefa**. Para o tipo de tarefa, selecione **Teste**.
3. Para tipo de testador, selecione **Porta do {{site.data.keyword.DRA_short}}**.
4. Especifique o nome do ambiente. Certifique-se de que esse valor corresponda ao que foi definido em suas
[propriedades do ambiente](#toolchain_pipeline_props).
5. Insira o nome da política a ser verificado nessa porta.

 Esse nome deve corresponder exatamente a um dos nomes de política que você definiu. É possível especificar apenas políticas que são definidas na mesma
organização do {{site.data.keyword.Bluemix_notm}} que a sua cadeia de ferramentas.

6. Opcional: para fazer uma função de porta no modo consultivo, limpe a caixa de seleção **Parar a execução deste estágio se essa tarefa
falhar**. Em modo consultivo, o {{site.data.keyword.DRA_short}} conclui a mesma análise de política na porta e gera relatórios, mas, se uma falha
ocorrer, o pipeline não será parado.
7. Clique em **Salvar** para retornar para o pipeline.
8. Configure portas para todas as suas políticas do {{site.data.keyword.DRA_short}} repetindo estas etapas.

![Tarefa Mocha do Deployment Risk](images/insights_gate_job.png)
*Figura 2. Porta do DevOps Insights*

Após o seu pipeline estar configurado, comece a usar o {{site.data.keyword.DRA_short}}. Para obter instruções, consulte
[Executando o pipeline de entrega](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports).

## Configurando um projeto Jenkins
{: #integrate_jenkins}

Depois de incluir o {{site.data.keyword.DRA_full}} em uma cadeia de ferramentas aberta e definir as políticas que ele monitora, será possível integrá-lo a seu projeto Jenkins. 

O plug-in IBM Cloud DevOps para Jenkins integra projetos Jenkins a cadeias de ferramentas. Uma *cadeia de ferramentas* é um conjunto de integrações de ferramentas que suporta tarefas de desenvolvimento, de implementação e de operações. O
poder coletivo de uma cadeia de ferramentas é maior que a soma de suas integrações de ferramentas individuais. As cadeias de ferramentas abertas são parte do serviço {{site.data.keyword.contdelivery_full}}. Para saber mais sobre o serviço {{site.data.keyword.contdelivery_short}}, veja [sua documentação](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Depois de instalar o plug-in IBM Cloud DevOps, será possível publicar os resultados de teste no {{site.data.keyword.DRA_short}}, incluir portas de qualidade automatizadas e controlar o risco de implementação. Também é possível enviar notificações de tarefa para outras ferramentas em sua cadeia de ferramentas, como Slack e PagerDuty. Para ajudá-lo a controlar as implementações, a cadeia de ferramentas poderá incluir mensagens de implementação nas confirmações do Git e seus problemas Git ou JIRA relacionados. Também será possível visualizar suas implementações na página Conexões da cadeia de ferramentas. 

O plug-in fornece ações pós-construção e CLIs para suportar a integração. O {{site.data.keyword.DRA_short}} agrega e analisa os resultados de testes de unidade, testes funcionais, ferramentas de cobertura de código, varreduras de código de segurança estática e varreduras de código de segurança dinâmica para determinar se seu código atende às políticas predefinidas nas portas em seu processo de implementação. Se o seu código não atender nem exceder uma
política, a implementação será interrompida, impedindo que as mudanças de risco sejam liberadas. É possível usar o {{site.data.keyword.DRA_short}} como uma rede de segurança para o seu ambiente de entrega contínua, uma forma de implementar e melhorar padrões de qualidade ao longo do tempo e uma ferramenta de visualização de dados para ajudá-lo a entender o funcionamento do seu projeto.

### Pré-Requisitos
{: #jenkins_prerequisites}

Deve-se ter acesso a um servidor que esteja executando um projeto Jenkins.

### Criando uma cadeia de ferramentas
{: #jenkins_create}

Antes de ser possível integrar o {{site.data.keyword.DRA_short}} a um projeto Jenkins, deve-se criar uma cadeia de ferramentas. 

1. Para criar uma cadeia de ferramentas, acesse a [página Criar uma cadeia de ferramentas](https://console.ng.bluemix.net/devops/create) e siga as instruções nessa página. 

2. Depois de criar a cadeia de ferramentas, inclua o {{site.data.keyword.DRA_short}} nela. Para obter instruções, veja a [documentação do {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

### Instalando o plug-in
{: #jenkins_install}

Primeiro, faça download do plug-in do {{site.data.keyword.DRA_short}}.  

1. Na página Visão geral da cadeia de ferramentas, clique em **DevOps Insights**.
2. Clique em **Configurações** e, em seguida, em **Configuração do plug-in do Jenkins**.
3. Siga as instruções na página para fazer download do plug-in.

Em seguida, no servidor Jenkins, instale o plug-in.

1. Clique em **Gerenciar Jenkins &gt; Gerenciar plug-ins** e clique na guia **Avançado**.
2. Clique em **Escolher arquivo** e selecione o arquivo de instalação do plug-in IBM Cloud DevOps. 
3. Clique em **Carregar**.
4. Reinicie o Jenkins e verifique se o plug-in foi instalado.

### Configurando tarefas do Jenkins para o painel Deployment Risk
{: #jenkins_configure}

Após a instalação do plug-in, é possível integrar o {{site.data.keyword.DRA_short}} ao projeto Jenkins. 

Siga estas etapas para usar as portas e o painel do Deployment Risk com seu projeto.

1. Abra a configuração de quaisquer tarefas que você tenha, como construção, teste ou implementação.

2. Inclua uma ação pós-construção para o tipo correspondente:

   * Para tarefas de construção, use **Publicar informações de construção no IBM Cloud DevOps**.
   
   * Para tarefas de teste, use **Publicar o resultado do teste no IBM Cloud DevOps**.
   
   * Para tarefas de implementação, use **Publicar informações de implementação no IBM Cloud DevOps**.
   
3. Preencha os campos requeridos. Eles variarão, dependendo do tipo de tarefa. 

   * Na lista **Credenciais**, selecione o ID e a senha do {{site.data.keyword.Bluemix_notm}}. Se eles não estiverem salvos no Jenkins, clique em **Incluir** para incluí-los e salvá-los. Teste sua conexão com o {{site.data.keyword.Bluemix_notm}} clicando em **Conexão de teste**.
   
   * No campo **Nome da tarefa de construção**, especifique o nome de sua tarefa de construção exatamente como está no Jenkins. Se a construção ocorrer com a tarefa de teste, deixe esse campo vazio. Se a tarefa de construção ocorrer fora do Jenkins, marque a caixa de seleção **As construções estão sendo feitas fora do Jenkins** e especifique o número e a URL da construção.
   
   * Para o ambiente, se os testes estiverem em execução no estágio de construção, selecione apenas o ambiente de construção. Se os testes estiverem em execução no estágio de implementação, selecione o ambiente de implementação e especifique o nome do ambiente. Dois valores são suportados: `STAGING` e `PRODUCTION`.
   
   * Para o campo **Local do arquivo de resultado**, especifique o local do arquivo de resultado. Se o teste não gerar um arquivo de resultado, deixe esse campo vazio. O plug-in fará upload de um arquivo de resultado padrão com base no status da tarefa de teste atual.

   Estas imagens mostram configurações de exemplo:
   
   ![Fazer upload de informações de construção](images/Upload-Build-Info.png "Publicar informações de construção no DRA")
   *Publicar informações de construção*
   
   ![Fazer upload de resultado de teste](images/Upload-Test-Result.png "Publicar resultado de teste no DRA")
   *Publicar resultado de teste*
   
   ![Fazer upload de informações de implementação](images/Upload-Deployment-Info.png "Publicar informações de implementação no DRA")
   *Publicar informações de implementação*

4. Se desejar usar as portas de política do {{site.data.keyword.DRA_short}} para controlar uma tarefa de implementação de recebimento de dados, inclua uma ação pós-construção, **Porta do IBM Cloud DevOps**. Escolha uma política e especifique o escopo dos resultados de teste. Para permitir que as portas de política evitem implementações de recebimento de dados, marque a caixa de seleção **Falhar a construção com base nas regras de política**. A imagem a seguir mostra uma configuração de exemplo:

    ![Porta do DevOps Insights](images/DRA-Gate.png "Porta do DevOps Insights")

5. Execute a tarefa de construção do Jenkins.

6. Visualize o painel Deployment Risk acessando o [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), selecionando sua cadeia de ferramentas e clicando em **DevOps Insights**.

O painel Deployment Risk depende da presença de uma porta após uma tarefa de implementação temporária. Se desejar usar o painel, certifique-se de que tenha uma porta depois de implementar no ambiente temporário, mas antes de implementar em um ambiente de produção.
    
### Configurando as Notificações
{: #jenkins_notifications}

É possível configurar as tarefas do Jenkins para enviar notificações para ferramentas, como Slack ou PagerDuty, seguindo as instruções nos [Bluemix Docs](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Este exemplo mostra como configurar o `ICD_WEBHOOK_URL` para configurações de tarefa:
![Configurar o parâmetro ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Configurar WebHook parametrizado")

Este exemplo mostra como configurar ações pós-construção para notificações de tarefa:
![Ações pós-construção para notificação de WebHook](images/PostBuild-WebHookNotification.png "Configurar notificação de WebHook em ações pós-construção")

## Exibição de resultados
{: #view_results}

Após um pipeline ser executado, o {{site.data.keyword.DRA_short}} começa a coletar e analisar os resultados de teste a partir dele, para estabelecer uma referência. Dados de cada execução subsequente são coletados e comparados com resultados anteriores. Portas de decisão usam esses dados para determinarem quando
parar uma implementação. 

É possível ver seus dados de avaliação de implementação e de porta no painel Deployment Risk. Para abrir o painel, abra o {{site.data.keyword.DRA_short}} e, no menu lateral, clique em **Deployment Risk**.

Se você estiver usando um pipeline do {{site.data.keyword.contdelivery_short}}, será possível visualizar os relatórios de execução de porta individuais do próprio pipeline. Para visualizar o relatório de decisão de uma porta no pipeline:

1. No estágio que contém a porta a ser verificada, clique em **Visualizar logs e histórico**.

2. Na tarefa que contém a porta, clique no nome da porta.

3. Na visualização de log, localize a mensagem `Verifique o relatório do {{site.data.keyword.DRA_short}} aqui` e clique no link para abrir o relatório.






