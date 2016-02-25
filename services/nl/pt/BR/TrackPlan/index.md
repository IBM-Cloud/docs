{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Introdução ao serviço {{site.data.keyword.trackplan}} {: #track-plan}  

*Última modificação: 21 de janeiro de 2016*

Para visualizar, editar e planejar tarefas, use o {{site.data.keyword.trackplanlong}} (o serviço {{site.data.keyword.trackplan}}). É possível controlar seu trabalho e o trabalho de sua equipe, criar defeitos, ver o que está previsto, manter sua lista não processada e planejar o trabalho para sprints futuros.
{: shortdesc}

O serviço do {{site.data.keyword.trackplan}} vincula planos e
código, para que os planos permaneçam sincronizados com o progresso da equipe de desenvolvimento. Com o serviço, é possível criar histórias, tarefas
e defeitos para descrever e controlar o serviço do projeto. Também
é possível planejar e gerenciar a lista não processada, as liberações e os sprints de produtos.

1. Efetue login no {{site.data.keyword.Bluemix_notm}}
e selecione uma organização e um espaço para seu app.
1. No painel do {{site.data.keyword.Bluemix_notm}}, clique em **CRIAR UM APP**.
1. Selecione um modelo de app móvel ou da web, selecione um iniciador e clique em
**CONTINUAR**. Dê um nome ao app e, em seguida, clique em
**CONCLUIR**.
1. Na página Iniciar codificação, role para baixo e clique em **VISUALIZAR VISÃO GERAL DO APP**.
1. No painel do app {{site.data.keyword.Bluemix_notm}}, crie um projeto hospedado em Git para o aplicativo clicando em **INCLUIR GIT**. Assegure-se de que a caixa de seleção **Preencher o repositório com o pacote do aplicativo iniciador e ativar Pipeline de Entrega (Compilação & Implementar)** esteja selecionada e, em seguida, clique em **CONTINUAR**. Após a criação do
					repositório Git, clique em **FECHAR**. O link INCLUIR GIT será substituído por um link EDITAR CÓDIGO e sua URL Git.
1. Inclua o serviço {{site.data.keyword.trackplan}}
no espaço para que seja possível gerenciar o trabalho de sua equipe.
    1. No painel do app {{site.data.keyword.Bluemix_notm}}, clique em **INCLUIR UM SERVIÇO OU API**. Para a categoria, selecione
**DevOps** e, no catálogo, clique
em **Track & Plan**.
    2. Na página do {{site.data.keyword.trackplan}},
							selecione um plano e clique em **CRIAR**.    
1. Na lista de apps, na coluna Estado, altere o estado do serviço {{site.data.keyword.trackplan}} clicando no
estado atual, que nesse caso é **DESATIVADO**. A página Configurações do projeto é aberta em {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}.
    1. Selecione a opção para ativar o serviço {{site.data.keyword.trackplan}}. Se necessário, atualize sua região, organização ou espaço
    2. Clique em **SALVAR**.  
1. Retorne ao painel do {{site.data.keyword.Bluemix_notm}} e clique no quadro de serviço {{site.data.keyword.trackplan}}. O estado para o serviço {{site.data.keyword.trackplan}} é alterado
para **ATIVADO** para o app.
1. Na lista de apps, na coluna Item de trabalho, clique em
**CRIAR** para começar a usar o serviço {{site.data.keyword.trackplan}}.  

No painel do {{site.data.keyword.Bluemix_notm}} Dashboard, é possível ver seus projetos {{site.data.keyword.jazzhub_short}} e suas contagens de membros, visibilidade e se eles têm o serviço {{site.data.keyword.trackplan}} ativado. É possível
criar itens de trabalho para qualquer um dos projetos do {{site.data.keyword.jazzhub_short}} ou ir para suas
ferramentas de planejamento.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="pt-BR" id="rellinks">
<h2 class="topictitle2" id="d68e338">Links relacionados</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Links relacionados</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(É aberto em uma nova guia ou janela)">Pré-requisitos do {{site.data.keyword.Bluemix_notm}}</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutoriais e amostras</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(É aberto em uma nova guia ou janela)">Clonar, editar e implementar um app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(É aberto em uma nova guia ou janela)">Desenvolver e implementar um app Node.js</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(É aberto em uma nova guia ou janela)">Desenvolver e implementar um app Java</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(É aberto em uma nova guia ou janela)">developerWorks: {{site.data.keyword.Bluemix_notm}} serviço {{site.data.keyword.trackplan}}</a></li>
</ul>
</div>
</aside>
</article>
