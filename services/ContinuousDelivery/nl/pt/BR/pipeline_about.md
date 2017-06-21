---

copyright:
  years: 2016, 2017
lastupdated: "2017-4-4"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Sobre o Delivery Pipeline
{: #deliverypipeline_about}

O serviço {{site.data.keyword.deliverypipeline}} do IBM&reg; Bluemix&reg;, também conhecido como pipeline, automatiza a implementação contínua dos seus projetos Bluemix. Em um pipeline, as sequências de estágios recuperam a entrada e executam tarefas, como construções, testes e implementações.
{:shortdesc}

As seções a seguir descrevem os detalhes conceituais por trás dos pipelines.

## Estágios
{: #deliverypipeline_stages}

Os estágios organizam a entrada e as tarefas conforme o código é construído, implementado e testado. Os estágios aceitam entrada de repositórios de controle de fonte (repositórios SCM) ou tarefas de construção (artefatos de construção) em outros estágios. Ao criar seu primeiro estágio, as configurações padrão são definidas para você na guia **ENTRADA**.

A entrada de um estágio é passada para as tarefas que ele contém e cada tarefa recebe um contêiner limpo no qual é executada. As tarefas em um estágio não podem passar artefatos entre si.

É possível definir as propriedades do ambiente do estágio que podem ser usadas em todas as tarefas. Por exemplo, é possível definir uma propriedade `TEST_URL` que passe uma única URL para as tarefas de implementação e teste em um único estágio. A tarefa de implementação seria implementada nessa URL e a tarefa de teste testaria o app de execução na URL.

Por padrão, em um estágio, construções e implementações são executadas automaticamente toda vez que mudanças são entregues no repositório SCM de um projeto. Os estágios e as tarefas são executados em série; eles ativam o controle
de fluxo para seu trabalho. Por exemplo, você poderá colocar um estágio de teste antes de
um estágio de implementação. Se os testes no estágio de teste falharem, o estágio de
implementação não será executado.

Você talvez queira restringir o controle de um estágio específico. Se você não
quiser que um estágio seja executado toda vez que uma mudança ocorrer na sua entrada,
será possível desativar o recurso. Na guia **ENTRADA**, na seção
Acionador de estágio, clique em **Executar tarefas somente quando este estágio
for executado manualmente**.

![A guia ENTRADA](images/input_tab_only_execute.png)

## Tarefas
{: #deliverypipeline_jobs}

Uma tarefa é uma unidade de execução dentro de um estágio. Um estágio contém
diversas tarefas e as tarefas de um estágio são executadas sequencialmente. Por padrão,
se uma tarefa falhar, as tarefas subsequentes do estágio não serão executadas.

![Tarefas de construção e teste dentro de um estágio](images/jobs.png)

Tarefas executadas em diretórios ativos discretos dentro dos contêineres do Docker
que são criados para cada pipeline executado. Antes da execução de uma tarefa, seu
diretório ativo é preenchido com a entrada que é definida no nível do estágio. Por
exemplo, talvez você tenha um estágio que contém uma tarefa de teste e uma tarefa de
implementação. Se você instalar dependências de uma tarefa, elas não estarão disponíveis
à outra tarefa. Entretanto, se você tornar as dependências disponíveis na entrada do
estágio, elas estarão disponíveis a ambas as tarefas.

Exceto tarefas de construção do tipo simples, ao configurar uma tarefa, é possível
incluir shell scripts do UNIX que incluam comandos de construção, teste ou implementação. Como
as tarefas são executadas em contêineres ad hoc, as ações de uma não podem afetar os
ambientes de execução das outras, mesmo que essas tarefas façam parte do mesmo estágio.

Além disso, as tarefas de pipeline podem executar apenas os comandos a seguir como `sudo`:
  * `/usr/sbin/service`
  * `/usr/bin/apt-get`
  * `/usr/bin/apt-key`
  * `/usr/bin/dpkg`
  * `/usr/bin/add-apt-repository`
  * `/opt/IBM/node-v0.10.40-linux-x64/npm`
  * `/opt/IBM/node-v0.12.7-linux-x64/npm`
  * `/opt/IBM/node-v4.2.2-linux-x64/npm`
  * `/usr/bin/Xvfb`
  * `/usr/bin/pip`


Após a execução de uma tarefa, o contêiner que foi criado para ela é descartado. Os resultados da execução de uma tarefa podem persistir, mas o ambiente no qual ela foi executada não.

**Nota**: as tarefas podem ser executadas por até 60 minutos. Quando
as tarefas excedem esse limite, elas falham. Se uma tarefa estiver excedendo o limite,
divida-a em várias tarefas. Por exemplo, se uma tarefa executar três trabalhos, você
poderá dividi-la em três tarefas: uma para cada trabalho.

Para saber como incluir uma tarefa em um estágio, veja [Incluindo uma tarefa em um estágio](/docs/services/ContinuousDelivery/pipeline_build_deploy.html#deliverypipeline_add_job){: new_window}.

### Tarefas de construção

As tarefas de construção compilam seu projeto em preparação para implementação. Elas geram artefatos que podem ser enviados para um diretório de archive de construção, embora por padrão, os artefatos sejam colocados no diretório-raiz do projeto.

As tarefas que tomam a entrada das tarefas de construção devem referenciar os artefatos de construção na mesma estrutura em que eles foram criados. Por exemplo, se uma tarefa de construção arquivar artefatos de construção em um diretório `output`, um script de implementação consultaria o diretório `output` em vez do diretório-raiz do projeto para implementar o projeto compilado. É
possível especificar o diretório para archive inserindo o nome do diretório no campo
**Construir diretório de archive**. Deixar o campo em branco, arquiva o diretório raiz.

**Nota**: se você selecionar o tipo de construtor **Simples** para uma tarefa de construção, irá ignorar o processo de construção. Nesse caso, o código não será compilado, mas enviado para o estágio de implementação no estado em que se encontra. Para construir e implementar, selecione um tipo de construtor diferente de **Simples**.

#### Propriedades do ambiente para scripts de construção
É possível incluir as propriedades do ambiente nos comandos shell de construção de uma tarefa de construção. As propriedades fornecem acesso a informações sobre o ambiente de execução da tarefa. Para obter mais informações, veja [Propriedades e recursos do ambiente para o serviço {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Tarefas de implementação

As tarefas de implementação fazem upload do seu projeto para o Bluemix como um app e são acessíveis a partir de uma URL. Depois que um projeto é implementado, é possível localizar o app implementado no painel do Bluemix.

As tarefas de implementação podem implementar novos apps ou atualizar os existentes. Mesmo
que você tenha primeiro implementado um app usando outro método, como a interface da
linha de comandos do Cloud Foundry ou a barra de execução no IDE da web, é possível
atualizar o app usando uma tarefa de implementação. Para atualizar um app, na tarefa de
implementação, use o nome desse app.

É possível implementar para uma ou várias regiões e serviços. Por exemplo, é
possível configurar seu {{site.data.keyword.deliverypipeline}} para usar um ou
mais serviços, testar em uma região e implementar para produção em múltiplas regiões. Para obter informações adicionais, consulte
[Regiões](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

#### Propriedades do ambiente para scripts de implementação

É possível incluir propriedades do ambiente no script de implementação de uma
tarefa de implementação. Essas propriedades fornecem acesso a informações sobre o
ambiente de execução da tarefa. Para obter mais informações, veja [Propriedades e recursos do ambiente para o serviço {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Tarefas de teste
Para requerer que as condições sejam atendidas, inclua tarefas de teste antes ou
após suas tarefas de construção e implementação. É possível customizar as tarefas de
teste para serem simples ou complexas, conforme necessário. Por exemplo, você poderá
emitir um comando cURL e esperar uma resposta específica. Também será possível executar um conjunto de testes de unidade ou executar testes funcionais com serviços de teste de terceiros, como o Sauce Labs.

Se os seus testes produzirem arquivos de resultado no formato XML JUnit, um
relatório baseado nos arquivos de resultado será mostrado na guia
**Testes** de cada página de resultado do teste. Se um teste falhar, a
tarefa também falhará.

#### Propriedades do ambiente para scripts de teste

É possível incluir propriedades do ambiente no script de uma tarefa de teste. As
propriedades fornecem acesso a informações sobre o ambiente de execução da tarefa. Para obter mais informações, veja [Propriedades e recursos do ambiente para o serviço {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

## Arquivos Manifest
{: #deliverypipeline_manifest}

Arquivos manifest, que são nomeados `manifest.yml` e armazenados
no diretório-raiz do projeto, controlam como seu projeto é implementado no Bluemix. Para obter informações sobre a criação de arquivos manifest de um projeto, veja a [documentação do Bluemix sobre manifests de aplicativos](/docs/manageapps/depapps.html#appmanifest). Para integração com o
Bluemix, seu projeto deve ter um arquivo manifest em seu diretório-raiz. No entanto, não é necessário implementar com base nas informações no arquivo.

No pipeline, é possível especificar tudo o que um arquivo manifest pode fazer usando
argumentos do comando `cf push`. Os argumentos do comando `cf
push` são úteis em projetos com diversos destinos de implementação. Se diversas
tarefas de implementação tentarem todas usar a rota especificada no arquivo manifest do
projeto, um conflito ocorrerá.

Para evitar conflitos, é possível especificar uma rota usando `cf
push` seguido pelo argumento de nome do host, `-n`, e o nome de
uma rota. A modificação do script de implementação para estágios individuais possibilita
evitar conflitos de rota ao implementar em vários destinos.

Para usar os argumentos do comando `cf push`, abra as definições
de configuração para uma tarefa de implementação e modifique o campo **Script
de implementação**. Para obter mais informações, veja a [documentação Push do Cloud Foundry ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push){: new_window}.

## Um pipeline de exemplo
{: #deliverypipeline_example}

Um pipeline simples pode conter três estágios:

1. Um estágio de construção que compila e executa processos de construção em um app.
2. Um estágio de teste que implementa uma instância do app e, em seguida, executa testes nele.
3. Um estágio de produção que implementa uma instância de produção do app testado.

Esse pipeline é mostrado no diagrama conceitual a seguir:

![Um diagrama conceitual de estágios e tarefas em um pipeline](images/diagram.jpg)

*Um modelo conceitual de um pipeline de três estágios*

Os estágios tomam suas entradas dos repositórios e das tarefas de construção e as
tarefas dentro de um estágio são executadas de maneira sequencial e independente umas das
outras. No pipeline de exemplo, os estágios são executados sequencialmente, mesmo que os
estágios de Teste e Produção assumam a saída do estágio de Construção como sua entrada.
