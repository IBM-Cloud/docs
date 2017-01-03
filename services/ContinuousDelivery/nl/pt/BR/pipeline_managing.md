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
Última atualização: 17 de novembro de 2016
{: .last-updated}

É possível administrar, configurar e estender as integrações de {{site.data.keyword.deliverypipeline}} do IBM&reg; Bluemix&reg;.
{:shortdesc}

Conclua as tarefas a seguir para administrar, configurar e estender um pipeline.

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

É possível ampliar os recursos de seu pipeline configurando suas tarefas para usar
serviços suportados. Por exemplo, as tarefas de teste
executam varreduras de código estático e as tarefas de construção podem globalizar as
sequências.

Para obter mais informações sobre como estender os recursos do pipeline, consulte [Estendendo os recursos do serviço {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

