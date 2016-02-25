{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#Introdução ao {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*Última atualização: 21 de janeiro de 2016*

Para automatizar suas construções e implementações para {{site.data.keyword.Bluemix}}, use o IBM Continuous {{site.data.keyword.deliverypipeline}} para {{site.data.keyword.Bluemix_notm}} (o serviço de {{site.data.keyword.deliverypipeline}}).
{: shortdesc} 

Ao desenvolver
um app na nuvem, é possível escolher dentre vários tipos de construção. Forneça o script de construção
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

1. Efetue login no {{site.data.keyword.Bluemix_notm}}
e selecione uma organização e um espaço para seu app.
1. No Painel {{site.data.keyword.Bluemix_notm}}, clique em **CRIAR UM APP**.
1. Selecione um modelo de app móvel ou da web, selecione um iniciador e clique em
**CONTINUAR**. Nomeie o app e, em seguida, clique em
**CONCLUIR**.  
1. Na página Iniciar codificação, role para baixo e clique em **VISUALIZAR VISÃO GERAL DO APP**.  
1. No Painel do app {{site.data.keyword.Bluemix_notm}}, crie um projeto hospedado por Git para o app, clicando em **INCLUIR GIT**. Certifique-se de
que a caixa de seleção **Preencher o repositório com o pacote do app iniciador e ativar {{site.data.keyword.deliverypipeline}} (Construir & Implementar)**
esteja selecionada e, em seguida, clique em **CONTINUAR**.   
1. Depois que seu repositório Git
é criado, clique em **FECHAR**. O link ADD GIT é substituído por um link EDIT CODE e sua URL Git.  
1. Inclua o serviço de {{site.data.keyword.deliverypipeline}} no espaço ou espaços associados. Após a inclusão desse serviço, é possível
criar um pipeline de implementação com vários estágios nos espaços do {{site.data.keyword.Bluemix_notm}},
configurando e executando estágios que contenham tarefas de construção, teste e
implementação.
    1. No Painel do app {{site.data.keyword.Bluemix_notm}}, clique em **INCLUIR UM SERVIÇO OU API**. Para a categoria,
marque a caixa de seleção **DevOps** e, no catálogo, clique em **Pipeline de entrega**.
    2. Selecione um plano e clique em **CRIAR**. O Painel {{site.data.keyword.deliverypipeline}} se abre mostrando o app que você criou anteriormente.     
  
No Painel {{site.data.keyword.deliverypipeline}}, é possível ver seus projetos {{site.data.keyword.jazzhub_short}} e os estados em que eles estão. É possível verificar os status de construções, o app implementado e as implementações
recentes ou ver os logs e os detalhes de implementação mais recentes.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">Links relacionados</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Links relacionados</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Abre em uma nova guia ou janela)">{{site.data.keyword.Bluemix_notm}} Pré-requisitos</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutoriais e amostras</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Abre em uma nova guia ou janela)">Clonar, editar e implementar um app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Abre em uma nova guia ou janela)">Desenvolver e implementar um app Node.js</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Abre em uma nova guia ou janela)">Desenvolver e implementar um app Java</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Abre em uma nova guia ou janela)">developerWorks: Serviço {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
