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

# Gerenciando Pipelines
{: #deliverypipeline_managing}
Última atualização: 30 de agosto de 2016
{: .last-updated}

É possível administrar, configurar e estender as integrações de {{site.data.keyword.deliverypipeline}} do IBM&reg; Bluemix&reg;.
{:shortdesc}

Conclua as tarefas a seguir para administrar, configurar e estender um pipeline.

## Controlando acesso
{: #deliverypipeline_access}

É possível restringir quem pode executar estágios ou modificar um pipeline. Para
fazer isso, acesse a página Configurações de pipeline, que pode ser acessada clicando
no ícone **Configuração do estágio** na página Pipeline: Todos os
estágios.

![O ícone de engrenagem de configurações de pipeline](./images/pipeline_settings.png)

## Propriedades e recursos do ambiente
{: #deliverypipeline_envprop}

É possível usar as propriedades e os recursos pré-instalados do ambiente para interagir com o serviço {{site.data.keyword.deliverypipeline}}. Por exemplo, você poderá incorporá-los em um script de tarefa ou comando de teste. Para obter mais informações, consulte [Propriedades e recursos do ambiente para o serviço {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

É possível incluir suas próprias propriedades do ambiente em um estágio a partir
de sua guia **PROPRIEDADES DO AMBIENTE**. As propriedades do ambiente
estão disponíveis a cada tarefa de um estágio.

É possível incluir quatro tipos de propriedades na guia Propriedades do ambiente:
* **Texto**: uma chave de propriedade com um valor de linha única.
* **Área de texto**: uma chave de propriedade com um valor multilinhas.
* **Seguro**: uma chave de propriedade com um valor de linha única. O valor é exibido como asteriscos.
* **Propriedades**: um arquivo no repositório do projeto. Esse
arquivo pode conter diversas propriedades. Cada propriedade deve estar em sua própria
linha. Para separar os pares de chave/valor, use o sinal de igual (=).

## Estendendo os recursos do pipeline
{: #deliverypipeline_extend}

É possível estender os recursos do pipeline de Construção e Implementação
configurando as tarefas para usar serviços suportados. Por exemplo, as tarefas de teste
executam varreduras de código estático e as tarefas de construção podem globalizar as
sequências.

Para obter mais informações sobre como estender os recursos do pipeline, consulte [Estendendo os recursos do serviço {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
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
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
