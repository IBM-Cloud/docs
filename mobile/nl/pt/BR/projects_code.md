---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando um Iniciador de código para criar um projeto
{: #projects_code}

É possível usar um [Iniciador de código](starters.html#Code_Starter) no painel Móvel do {{site.data.keyword.Bluemix}} para criar um projeto no ambiente do {{site.data.keyword.Bluemix_notm}}. Esse procedimento não se aplica a projetos que usam os iniciadores de UI. Consulte [Criando um projeto com um iniciador de UI](projects_ui.html) para obter instruções sobre iniciadores de UI. 
{:shortdesc}

Conclua as etapas a seguir para criar um projeto com um iniciador de código:

1. Crie um novo projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

 Você inicia com a guia *Introdução* depois de selecionar o catálogo Móvel. Há descrições de iniciadores selecionados que podem ser usados e diferentes maneiras de criar um projeto que dependem do quanto de ajuda você precisa. Se desejar apenas começar, selecione **Criar projeto**.

 Se você já tiver projetos, poderá também iniciar com a guia *Projetos* selecionada. Na visualização **Projetos** do painel do {{site.data.keyword.Bluemix_notm}} Mobile, é possível selecionar um projeto com o qual trabalhar, usar as *Ações* para um projeto para excluí-lo ou fazer download do código para ele, ou criar um novo projeto.

	1. No Console do {{site.data.keyword.Bluemix_notm}}, selecione **Móvel** depois de expandir o menu com as três linhas ao lado do logotipo do {{site.data.keyword.Bluemix_notm}}. 
	
	2. Selecione **Criar projeto**. 

	  Como alternativa, é possível selecionar a guia **Projetos** para visualizar os projetos que já estão em seu ambiente móvel e criar um novo projeto clicando em **Criar projeto**.

	3. Clique em **Iniciadores de código**.  

	4. Selecione o iniciador que melhor corresponda ao tipo de app que você deseja criar e selecione **Criar projeto**. Existem **Iniciadores de UI (interface com o usuário)** e **Iniciadores de código**. Consulte [Iniciadores](starters.html) para obter mais informações sobre iniciadores e como usá-los. 
	
	5. Insira um nome para seu projeto e selecione **Criar**.
	
2. Faça suas seleções na tela **Visão geral do projeto**.  A tela **Visão geral do projeto** exibe informações sobre seu projeto e os serviços opcionais que podem ser incluídos no projeto, como {{site.data.keyword.mobilepushshort}} e Autenticação.  

	1. Opcional: selecione **Incluir** para incluir um dos serviços listados em seu projeto. Edite o **Nome do serviço** para seu serviço e clique em **Criar**. Ao incluir serviços em seu projeto, você é vinculado à página do {{site.data.keyword.Bluemix_notm}} para tal serviço. Configure o serviço fornecendo as informações que são requeridas para o serviço.
	
	2. Opcional: repita a etapa *a* para qualquer recurso adicional que você queira incluir em seu projeto.

3. Opcional: selecione **Dados** para se conectar a um banco de dados Cloudant NoSQL ou serviço de Armazenamento de objetos.
	1. Clique em **Criar** para configurar um novo Cloudant NoSQL DB ou serviço de Armazenamento de objetos.
	
	Nota: se criar uma instância do serviço de Armazenamento de objetos, você será guiado para fora do projeto para criá-lo e incluir as credenciais necessárias. Navegue de volta para o projeto depois de criá-lo e selecione **Incluir existente** para conectar o serviço ao projeto.
	
	Se já houver uma instância existente que não esteja conectada a outro projeto que você deseja conectar a este, selecione **Incluir existente**. 
	
	2. Verifique se o tile do Cloudant NoSQL DB ou do serviço de Armazenamento de objetos ao qual você está conectado é exibido na guia Dados de seu projeto.

4.  Faça download do projeto e conclua a configuração.

    1. Clique em **Fazer download do código** e selecione seu idioma preferencial.
   
    2. Extraia o archive e visualize o arquivo `README.md` em um visualizador de Redução de preço para concluir a configuração.

5.  Teste seu app! 


