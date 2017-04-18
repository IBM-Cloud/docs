---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Introdução ao {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

Última atualização: 15 de setembro de 2016
{: .last-updated}

Para automatizar suas construções e implementações no
{{site.data.keyword.Bluemix}}, use o IBM Continuous
{{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Estas informações se aplicam ao {{site.data.keyword.deliverypipeline}} e ao {{site.data.keyword.deliverypipeline}} Next.

Com o serviço {{site.data.keyword.deliverypipeline}}, é possível escolher
entre diversos tipos de construção. Forneça o script de construção
e o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} o executará; não é necessário
configurar sistemas de construção. Em seguida, com um clique, é possível implementar automaticamente seu app para um ou
vários espaços de {{site.data.keyword.Bluemix_notm}}, servidores públicos de Cloud Foundry ou contêineres Docker no IBM Containers para {{site.data.keyword.Bluemix_notm}}.  

Tarefas de construção compilam e compactam o código-fonte do app a partir de repositórios de gerenciamento de controle de fonte (SCM) Git ou Jazz. As tarefas de construção produzem artefatos implementáveis, como arquivos WAR ou contêineres Docker para IBM Containers. Além disso,
é possível executar testes de unidade automaticamente em sua construção. Sempre que o código-fonte for
alterado, uma construção será acionada.

Uma tarefa de implementação toma a saída de uma tarefa de construção e a implementa para servidores IBM Containers ou Cloud Foundry como {{site.data.keyword.Bluemix_notm}}.  

É possível implementar para uma ou várias regiões e serviços. Por exemplo, é possível configurar seu serviço de {{site.data.keyword.deliverypipeline}} para que
os artefatos de desenvolvimento usem IBM Containers, sejam testados em uma região e sejam implementados para produção em múltiplas regiões. Para obter informações adicionais, consulte
[Regiões](../../overview/index.html#ov_intro__reg).

Há várias maneiras de criar um pipeline, incluindo adicionar um pipeline para um aplicativo existente e criar um pipeline sem um aplicativo existente. Se você ainda não tem um serviço de {{site.data.keyword.deliverypipeline}} em sua organização, é possível acessar o catálogo. Clique em {{site.data.keyword.deliverypipeline}} ou
{{site.data.keyword.deliverypipeline}} Next e clique em Criar.

Conclua estas etapas para configurar um {{site.data.keyword.deliverypipeline}} para um aplicativo existente.    

1. No Painel do app {{site.data.keyword.Bluemix_notm}}, na guia Visão
geral, em **Entrega contínua**, crie um projeto hospedado pelo Git
para o app clicando em **Incluir repositório Git e pipeline** ou
**Incluir Git**, dependendo do contexto.
1. Certifique-se de que a caixa de seleção **Preencher o repositório com
o pacote do app starter e ativar o pipeline de Construção e implementação** esteja marcada e, em seguida, clique em
**CONTINUAR**. Talvez seja necessário verificar seu endereço de
e-mail para continuar.  
1. Depois que seu repositório Git
é criado, clique em **FECHAR**. O botão Incluir Git foi substituído por
um botão Editar código e sua URL do Git.  
1. Para abrir o pipeline, clique em **Editar código** e, em
seguida, clique em **Construir e implementar**. Para executar o
pipeline pela primeira vez, envie por push uma mudança para o repositório Git.

Após a inclusão desse serviço, é possível
criar um pipeline de implementação com vários estágios nos espaços do {{site.data.keyword.Bluemix_notm}},
configurando e executando estágios que contenham tarefas de construção, teste e
implementação. No Painel {{site.data.keyword.deliverypipeline}}, é possível ver seus projetos {{site.data.keyword.jazzhub_short}} e os estados em que eles estão. É possível verificar os status de construções, o app implementado e as implementações
recentes ou ver os logs e os detalhes de implementação mais recentes.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Links relacionados</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Links relacionados</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Abre em uma nova guia ou janela)">{{site.data.keyword.Bluemix_notm}} Pré-requisitos</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Abre em uma nova guia ou janela)">Método do IBM Bluemix Garage: Pipeline de entrega</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutoriais e amostras</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Abre em uma nova guia ou janela)">developerWorks: Serviço {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
