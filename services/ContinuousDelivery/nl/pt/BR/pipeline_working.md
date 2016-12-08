---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Trabalhando com {{site.data.keyword.deliverypipeline}} {: #pipeline-working}  

Última atualização: 18 de novembro de 2016
{: .last-updated}

Para automatizar suas construções e implementações no
{{site.data.keyword.Bluemix}}, use o
{{site.data.keyword.deliverypipeline}} para
{{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Com o {{site.data.keyword.deliverypipeline}}, é possível escolher
entre diversos tipos de construção. Forneça o script de construção
e o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} o executará; não é necessário
configurar sistemas de construção. Em seguida, com um clique, é possível implementar automaticamente seu app para um ou
vários espaços de {{site.data.keyword.Bluemix_notm}}, servidores públicos de Cloud Foundry ou contêineres Docker no IBM Containers para {{site.data.keyword.Bluemix_notm}}.  

Tarefas de construção compilam e compactam o código-fonte do app a partir de
repositórios Git. As tarefas de construção produzem artefatos implementáveis, como arquivos WAR ou contêineres Docker para IBM Containers. Além disso,
é possível executar testes de unidade automaticamente em sua construção. É possível configurar suas tarefas de construção para que a cada confirmação enviada por push, uma construção seja acionada.

Uma tarefa de implementação toma a saída de uma tarefa de construção e a implementa para servidores IBM Containers ou Cloud Foundry como {{site.data.keyword.Bluemix_notm}}.  

É possível implementar para uma ou várias regiões e serviços. Por exemplo, é
possível configurar seu {{site.data.keyword.deliverypipeline}} para usar um ou
mais serviços, testar em uma região e implementar para produção em múltiplas regiões. 
Para obter informações adicionais, consulte
[Regiões](/docs/overview/whatisbluemix.html#ov_intro_reg).

Há várias maneiras de criar um pipeline, incluindo adicionar um pipeline para um aplicativo existente e criar um pipeline sem um aplicativo existente. Se
você ainda não tem um serviço de {{site.data.keyword.deliverypipeline}} em sua
organização, será possível acessar o catálogo, clicar em
{{site.data.keyword.deliverypipeline}} e clicar em Criar.

Conclua estas etapas para configurar um {{site.data.keyword.deliverypipeline}} para um aplicativo existente.    

1. No Painel do app {{site.data.keyword.Bluemix_notm}}, clique em seu app.
1. No menu de hamburger da barra de menus do
{{site.data.keyword.Bluemix_notm}}, clique em **Serviços** e,
em seguida, clique em **DevOps**.
1. Clique em **Pipelines** e depois clique em **Criar um pipeline**.

Para [criar um
pipeline (o link é aberto em uma nova janela)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} que esteja
configurado para implementar um aplicativo Cloud Foundry, siga estas etapas:    

1. Clique em **Cloud Foundry**.  
1. Se você desejar usar um nome diferente para o pipeline, mude o nome padrão. 
1. Se você desejar usar um nome diferente para o aplicativo, mude o nome padrão. Esse nome é o aplicativo no qual o pipeline é implementado. 
1. Se você não tiver uma cadeia de ferramentas, será criada uma com um nome padrão. Se você desejar usar um nome diferente para a cadeia de ferramentas, mude o nome. Com a cadeia de ferramentas, é possível ampliar os recursos de seu pipeline por meio da integração com outras ferramentas e serviços. 

 **Dica**: os pipelines e as cadeias de ferramentas pertencem às
organizações (orgs). Se você pertencer a uma organização que tenha cadeias de ferramentas,
será possível usar essas cadeias de ferramentas mesmo que você não as tenha criado.
 
1. Selecione a cadeia de ferramentas que deseja usar ou digite um nome para a nova cadeia de ferramentas que deseja criar.
1. Forneça o local de seu repositório GitHub.

 **Dica**: se você não estiver autorizado o {{site.data.keyword.Bluemix_notm}} a acessar o GitHub, será solicitado a clicar em **Autorizar** para acessar o website do GitHub. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix_notm}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.

   * Se você tiver um repositório GitHub e desejar usá-lo, para o tipo de repositório, selecione **Link**. Procure o local do repositório e selecione-o na lista de repositórios disponíveis.
   
   * Se você desejar criar um repositório GitHub vazio, para o tipo de repositório, selecione **Novo**. Digite um nome para o repositório.
   
   * Se você desejar criar um clone de um repositório GitHub, para o tipo de
repositório, selecione **Copiar**. Procure o local do repositório e
selecione-o na lista de repositórios disponíveis.
   
   * Se desejar bifurcar um repositório GitHub para que possa contribuir com as mudanças por meio de solicitações pull, selecione **Bifurcar**. Procure o local do repositório e selecione-o na lista de repositórios disponíveis.
 
1. Clique em **Criar**. O pipeline é criado, configurado e exibido na página Visão geral da cadeia de ferramentas.
 ![Título do pipeline](images/cd_pipeline.png)

Para criar um
[pipeline
vazio (o link é aberto em uma nova janela)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sem qualquer estágio
pré-configurado:

1. Clique em **Customizado**.
1. Se você desejar usar um nome diferente para o pipeline, mude o nome padrão. 
1. Se você não tiver uma cadeia de ferramentas, será criada uma com um nome padrão. Se você desejar usar um nome diferente para a cadeia de ferramentas, mude o nome. Com a cadeia de ferramentas, é possível ampliar os recursos de seu pipeline por meio da integração com outras ferramentas e serviços. 
1. Selecione a cadeia de ferramentas que deseja usar ou digite um nome para a nova cadeia de ferramentas que deseja criar.
1. Clique em **Criar**. Um pipeline vazio é criado e
representado como um quadro na página Visão geral da cadeia de ferramentas.

No quadro do {{site.data.keyword.deliverypipeline}}, mude a configuração,
verifique o status das construções, o app implementado e as implementações recentes;
consulte os logs mais recentes e os detalhes da implementação ou exclua seu pipeline.  

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
