---

copyright:
  years: 2016

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

# Construindo e implementando a partir de pipelines
{: #deliverypipeline_build_deploy}
Última atualização: 29 de agosto de 2016
{: .last-updated}

O serviço {{site.data.keyword.deliverypipeline}} do IBM&reg; Bluemix&reg; permite que você implemente um processo repetido de integração contínua e entrega contínua.
{:shortdesc}

Conclua as tarefas a seguir para criar e configurar um pipeline.

## Incluindo um estágio
{: #deliverypipeline_add_stage}

1. Na página Pipeline: Todos os estágios, clique em **INCLUIR
ESTÁGIO**. A página Configuração do estágio é aberta.
2. Configure o estágio.
  1. Na guia **ENTRADA**, selecione uma entrada para o estágio.
  2. Na guia **TAREFAS**, inclua e configure pelo menos uma
tarefa. O primeiro estágio normalmente tem pelo menos uma tarefa de construção.
3. Clique em **SALVAR**.

## Incluindo uma tarefa em um estágio
{: #deliverypipeline_add_job}

1. No estágio, clique no ícone **Configuração do estágio** e,
em seguida, clique em **Configurar estágio**.
2. Clique na guia **TAREFAS**.
3. Clique em **INCLUIR TAREFA**. Selecione o tipo de tarefa a
ser incluído.
4. Configure a tarefa.
5. Clique em **SALVAR**.

![Incluindo uma tarefa em um estágio](./images/AddJob.png)

## Executando um estágio
{: #deliverypipeline_run_stage}

É possível executar manualmente um estágio clicando no ícone **Executar estágio** na página Pipeline: Todos os estágios.

![Clicando no ícone Executar estágio em um estágio](./images/RunStage.png)

É possível também solicitar construções e implementações sob demanda na página de
histórico de construções de uma de duas maneiras:
* Arraste uma construção para a caixa que está sob um estágio configurado.
* Ao lado de uma construção, clique no ícone **Enviar para** e, em seguida, selecione um espaço no qual implementar.
  ![O estágio de Execução com este ícone de construção](./images/deploy_to.png)

Para cancelar um estágio em execução, no estágio, clique em **Visualizar
logs e histórico**. Na lista de tarefas, clique no número da tarefa em
execução e, em seguida, clique em **CANCELAR**. É possível também
cancelar tarefas individualmente clicando em uma tarefa e, em seguida, clicando em
**CANCELAR** ou clicando no ícone **Parar** ao
lado de uma tarefa em seu estágio.

## Implementando um app
{: #deliverypipeline_deploy}

Uma tarefa de implementação configurada adequadamente implementa um app no destino
sempre que é executada. Para executar manualmente uma tarefa de implementação, clique no
ícone **Executar estágio** do estágio em que a tarefa está.

###Revisões de entrada
Quando você executar um estágio manualmente ou se ele for executado porque o
estágio antes dele foi concluído, o estágio em execução seleciona sua revisão de entrada. Normalmente,
a revisão de entrada é um número de construção. Para selecionar a revisão de entrada, o
estágio segue este processo:

1. Se uma revisão específica for selecionada, use-a.
2. Se uma revisão específica não for especificada, procure estágios anteriores até que seja encontrado um estágio que use a mesma entrada. Localize e use a última revisão executada com sucesso dessa entrada.
3. Se uma revisão específica não for especificada e nenhum outro estágio usar a
origem especificada como entrada, use a revisão mais recente da entrada.

**Dica:** é possível implementar uma construção anterior. No
estágio que contém a construção, clique em **Visualizar logs e histórico**. Na
página que é aberta, clique para expandir o número da execução e, em seguida, clique na
tarefa de construção. Clique em **ENVIAR PARA** e selecione um
destino.

###Incluindo serviços em apps
É possível incluir serviços em seus apps e gerenciá-los no Painel do Bluemix ou na
interface da linha de comandos (CLI) do Cloud Foundry. É possível também emitir
comandos da CLI do Cloud Foundry em scripts para tarefas do pipeline de serviços DevOps. Por
exemplo, é possível incluir um serviço em um app no script de uma tarefa de implementação. Para
obter mais informações sobre como incluir serviços, consulte
[Incluindo
um serviço em seu aplicativo](https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service).

## Exibindo logs
{: #deliverypipeline_view_logs}

É possível visualizar os logs para tarefas e visualizar os estágios conforme eles
estão sendo executados na página Histórico de estágios.

Para visualizar o log de uma tarefa, clique na tarefa. Como alternativa, em um estágio, clique em **Visualizar logs e histórico**.

Para visualizar o log de tempo de execução de um aplicativo implementado, clique em **Visualizar log de tempo de execução**.

![Áreas em um quadro de estágio que pode ser clicado para abrir os logs relevantes](./images/view_logs_and_history.png)

Além dos logs de tarefas, é possível visualizar resultados de testes, artefatos
gerados e mudanças de código para qualquer tarefa de construção.

É possível também executar, cancelar ou configurar um estágio na página Histórico
de estágios. Na parte superior da página, clique em **EXECUTAR** para
executar um estágio ou **CONFIGURAR** para configurar um estágio. Enquanto
um estágio está em execução, é possível cancelá-lo clicando no número da execução e
depois clicando em CANCELAR.

![Clicando no número da execução de um estágio para selecioná-lo na página Histórico de estágios](./images/click_stage_run_number.png)

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg

-->
