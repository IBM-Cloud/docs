---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando um Iniciador de UI para criar um projeto
{: #projects_ui}

É possível usar um
[Iniciador de UI](starters.html#UI_Starter) no
painel Móvel do {{site.data.keyword.Bluemix}} para criar
um projeto no ambiente do {{site.data.keyword.Bluemix_notm}}. Esse procedimento não se aplica a projetos
que usam os iniciadores de código. Consulte [Criando um
projeto com um iniciador de código](projects_code.html) para obter instruções sobre iniciadores de
código.
{:shortdesc}

Conclua as etapas a seguir para criar um projeto com um iniciador de UI (interface com o usuário):

1. Crie um novo projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

 Você inicia com a guia *Introdução* depois de selecionar o catálogo Móvel. Há descrições de iniciadores selecionados que podem ser usados e diferentes maneiras de criar um projeto que dependem do quanto de ajuda você precisa. Se você desejar apenas começar com ajuda mínima, selecione **Criar projeto**.

 Se você já tiver projetos, será possível selecionar a guia *Projetos* enquanto
você está na guia *Introdução*. Na visualização
**Projetos** do painel do {{site.data.keyword.Bluemix_notm}}
Mobile, é possível selecionar um projeto com o qual trabalhar, usar as
*Ações* para um projeto para excluí-lo ou fazer download do código para ele,
ou criar um novo projeto. Se o projeto começou a partir de um iniciador de UI (interface com o usuário), você
também poderá abrir o projeto no Construtor de UI (interface com o usuário) diretamente no *Ações*. 

	1. No Console do {{site.data.keyword.Bluemix_notm}}, selecione **Móvel** depois de expandir o menu com as três linhas ao lado do logotipo do {{site.data.keyword.Bluemix_notm}}. 
	
	2. Selecione **Criar projeto**. 

	  Como alternativa, é possível selecionar a guia **Projetos** para visualizar os projetos que já estão em seu ambiente móvel e criar um novo projeto clicando em **Criar projeto**. 

	3. Selecione o iniciador que melhor corresponda ao tipo de app que você deseja criar e selecione **Criar projeto**. Existem **Iniciadores de UI (interface com o usuário)** e **Iniciadores de código**. Consulte [Iniciadores](starters.html) para obter mais informações sobre iniciadores e como usá-los. 
	
	4. Insira um nome para seu projeto e selecione **Criar**.
	
2. Faça suas seleções na tela **Visão geral do projeto**.  A tela **Visão geral do projeto** exibe informações sobre o projeto e os recursos opcionais que podem ser incluídos no projeto, como {{site.data.keyword.mobilepushshort}}.  

	1. Opcional: selecione **Incluir** para incluir um dos
recursos listados em seu projeto. Edite o **Nome do serviço** para seu serviço e clique em **Criar**. Ao incluir serviços em seu projeto, você é vinculado à página do {{site.data.keyword.Bluemix_notm}} para tal serviço. Configure
o serviço fornecendo as informações que são requeridas para o
serviço.
	
	2. Opcional: repita a etapa *a* para qualquer recurso adicional que você queira incluir em seu projeto. 

3. Projete sua interface com o usuário usando o Construtor de UI (interface com o usuário).

   **Nota:** como os Iniciadores de código não têm uma interface com o usuário customizável, a guia *Design* não está disponível.

    1. Selecione **Construtor de UI (interface com o usuário)** no menu de navegação para
customizar o design de seu app. 
	
		**Dica:** para visualizar uma visão
geral rápida do Construtor de UI, selecione **Mostre-me
como funciona** na navegação após selecionar o Construtor
de UI. 
	
	2. Customize o layout do seu app na guia **Telas**.
	
	3. Inclua novas telas selecionando **Criar tela**. Nomeie uma nova tela para
facilitar a consulta em seu app. É possível selecionar entre os tipos de tela a seguir: 
		* Menu
		* Listar
		* Map
		* Customizado 
		* Diagrama
		
	4. É possível mudar o título do menu de seu app selecionando a caixa de texto
*Menu* na seção **Layout** de sua
interface e substituindo o conteúdo no campo **Data a serem
exibidos**. Visualize suas atualizações na seção de dispositivo simulado.
	
		Atualize os itens de design selecionando cada um e atualizando as informações,
conforme necessário. Esses itens são exibidos em um formato de árvore. É possível mudar a
ordem ou o local dos itens de menu arrastando um item para um novo local. Todos os filhos
do item também são movidos com o pai. As informações textuais nos itens da árvore que são
exibidas nos campos **Dados a serem exibidos** referenciam conteúdo na
planilha de origem de dados. *Não mude esses itens na visualização
**Design** porque eles serão sobrescritos pelo conteúdo nas
Origens de dados que são identificadas na visualização **Dados**.* 
		
		Um item identificado na árvore como *Formulário* é independente e
pode ser modificado sequencialmente. Ele não faz referência a informações de Origem de dados.
	
	5. Selecione **Dados** na navegação para visualizar os dados que estiverem sendo
usados pelo app. Há informações padrão no modelo; no entanto, é possível mudar a origem dos dados selecionando
**Criar novo**. É
possível referenciar mais de uma origem de dados; por isso, forneça um nome para cada uma
que você usar. É possível selecionar dentre as opções de origem de dados a seguir:
		* Cloud
		* Local
		* Cloudant
		* Google Sheet
		* Excel Online
		* Google Drive
	
		É possível também importar, exportar ou modificar o conteúdo que está na tabela,
se ele for local, usando os botões e selecionando o conteúdo na tabela.
	     
		**Nota:** se você importar dados que não correspondem à estrutura dos dados padrão, ative a régua de controle *Substituir esquema*. Um exemplo disso é
um arquivo .csv que tem menos colunas do que os dados que são fornecidos com seu
iniciador.
		 
	6. Selecione **Navegação** para customizar as ações de navegação em seu app. Isso é opcional porque as ações de navegação para muitas telas são criadas automaticamente com base nos relacionamentos das telas. É possível mudar a tela de destino selecionando primeiro a tela ou o campo *a partir do qual* você deseja navegar na lista de itens de Menu. Em seguida, selecione a tela *para a qual* deseja navegar no campo da tela de Destino. 
		 
	7. Selecione **Acesso do usuário** na navegação para modificar os
requisitos de acesso de seu projeto. É possível ativar e desativar o acesso do usuário
com o comutador. Quando o acesso do usuário está ativado, é possível configurar o
tempo limite de usuário inativo e as credenciais dos usuários que podem acessar o app.
	
	8. Selecione **Configurações** no menu de navegação para
modificar as informações gerais e as cores do projeto. Essa tela é onde você insere sua
chave API do Google, se for necessário para os recursos que você incluiu em seu projeto. Essa
tela é também onde você inclui seu identificador de pacote configurável exclusivo que é
registrado na Apple Store ou Google Play Store.
	
		Se você desejar incluir o IBM MobileFirst Foundation SDK em seu projeto, ative
o comutador.
		
	9. Se você alternou o comutador para incluir o IBM MobileFirst Platform
Foundation em seu projeto na tela *Configurações*, uma seleção
**Foundation** será exibida na navegação. Selecione
**Foundation** e conclua as informações necessárias que são
específicas do IBM MobileFirst Platform Foundation.
	
	10. Selecione **Publicar** no menu de navegação para inserir as informações finais
para criar seu app móvel. É possível inserir seu identificador de Pacote configurável para iOS e o
identificador de Aplicativo para Android.
	
		Se você estiver criando um app iOS, deverá obter o Identificador de pacote
configurável, o Certificado de distribuição como um arquivo `.p12` e o
Perfil de fornecimento como um arquivo `.mobileprovision` no portal de
fornecimento da Apple. Os três devem ser criados ao mesmo tempo e com o mesmo computador
que você planeja usar quando postar seu aplicativo na Apple store. O Certificado de
distribuição e o Perfil de fornecimento devem ser baseados no Identificador de pacote configurável. 	
4. Volte para a tela *Visão geral do projeto* para recuperar o
código de seu app e teste-o! É possível fazer download do código diretamente para os
sistemas operacionais iOS ou Android, ou varrendo um código QR para o sistema operacional
Android. 


