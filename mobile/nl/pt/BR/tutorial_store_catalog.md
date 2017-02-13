---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# Tutorial - Iniciador de UI (interface com o usuário) de catálogo de loja
{: #tutorial_store_catalog}

O Iniciador de UI (interface com o usuário) de catálogo de loja do {{site.data.keyword.Bluemix}} fornece uma estrutura básica de app de vendas que é possível customizar e dá a você pontos de integração para cada um dos serviços do {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisitos
{: #tutorial_requirements}

* Uma conta do [Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net "Ícone de link externo")


## Guia de Introdução
{: #tutorial_gs}

Para colocar em funcionamento rapidamente o Iniciador de UI (interface com o usuário) de catálogo de loja, siga estas etapas:

1. Crie um projeto do painel Móvel no {{site.data.keyword.Bluemix_notm}}.

   1. Na página **Introdução** no painel Móvel, clique em **Criar projeto**.

      Como alternativa, clique em **Criar projeto** na página **Projetos**.

   2. Selecione **Iniciadores de UI (interface com o usuário)** se não tiver selecionado ainda.

   3. Selecione **Catálogo de loja** e clique em **Criar projeto**.

   4. Insira o nome do projeto e clique em **Criar**.

2. Opcional: inclua o recurso {{site.data.keyword.mobilepushshort}}.

   1. Clique em **Incluir** para o **{{site.data.keyword.mobilepushshort}}** na página **Visão geral do projeto**.

      Como alternativa, é possível clicar em **Criar** na página **{{site.data.keyword.mobilepushshort}}**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Para iOS, [configure o Apple Push Notification Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_ios.html "Ícone de link externo"){: new_window}.

   4. Para Android, [configure o Google Cloud Messaging ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobilepush/t_push_provider_android.html "Ícone de link externo"){: new_window}.

3. Opcional: inclua outros recursos.

   1. Clique em **Incluir** para o
recurso na página **Visão geral do projeto**.

   2. Insira o nome do serviço e clique em **Criar**.

   3. Siga as instruções que são fornecidas com o serviço
para configurá-lo.

4. Projete seu app.

   1. Selecione **Construtor de UI (interface com o usuário)** no menu de navegação para
customizar o design de seu app.
   
		**Dica:** para visualizar uma visão
geral rápida do Construtor de UI, selecione **Mostre-me
como funciona** na navegação após selecionar o Construtor
de UI.

   2. Selecione a guia **Design** na navegação.

      Há uma área de trabalho para o design de seu app e uma visualização simulada da aparência do seu app.

   3. Como opção, inclua novas telas selecionando **Criar
tela**. Nomeie uma nova tela para facilitar a consulta em seu app. As novas telas são criadas no
mesmo nível que a tela principal, independentemente do que estiver selecionado na árvore. É possível selecionar dentre os tipos de
telas a seguir:
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

	  Aviso: se você importar dados que não correspondem à estrutura dos dados
padrão, ative a régua de controle *Substituir esquema*. Um exemplo disso é
um arquivo .csv que tem menos colunas do que os dados que são fornecidos com seu
iniciador.
	  
   6. Selecione **Navegação** para customizar as ações de navegação em seu app. Isso é opcional porque as ações de navegação para muitas telas são criadas automaticamente com base nos relacionamentos das telas. É possível mudar a tela de destino selecionando primeiro a tela ou o campo *a partir do qual* você deseja navegar na lista de itens de Menu. Em seguida, selecione a tela *para a qual* deseja navegar no campo da tela de Destino. 

   7. Selecione **Acesso do usuário** na navegação para modificar os
requisitos de acesso de seu projeto. É possível ativar e desativar o acesso do usuário
com o comutador. Quando o acesso do usuário está ativado, é possível configurar o
tempo limite de usuário inativo e as credenciais dos usuários que podem acessar o app.

   8. Selecione **Configurações** no menu de navegação para
modificar as informações gerais e as cores do projeto. Essa tela é onde você insere sua
chave API do Google, se for necessário para os serviços que você incluiu em seu projeto. Essa
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
que são necessárias para criar seu app móvel. É possível inserir seu identificador de Pacote configurável para
iOS e o identificador de Aplicativo para Android.

       Se você estiver criando um app iOS, deverá obter o Identificador de pacote
configurável, o Certificado de distribuição como um arquivo *.p12* e o
Perfil de fornecimento como um arquivo *.mobileprovision* no portal de
fornecimento da Apple. Os três devem ser criados ao mesmo tempo e com o mesmo computador
que você planeja usar quando postar seu aplicativo na Apple store. O Certificado de
distribuição e o Perfil de fornecimento devem ser baseados no Identificador de pacote configurável. 	

5. Faça download do seu projeto.

   1. Clique em **Código** e selecione sua plataforma ou linguagem de programação preferencial.

   2. Para Android, é possível escolher dentre as opções a seguir após o código ser gerado:

      * Fazer download do código

      * Fazer download do APK

      * Fazer download com o Código Quick Response

   3. Para iOS, é possível escolher dentre as opções a seguir após o código ser gerado:

      * Fazer download do código

6. Execute seu app no dispositivo ou no simulador.


## O que Fazer a Seguir
{: #tutorial_next}

[Teste-o! ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "Ícone de link externo"){: new_window}


### Tutoriais do iniciador de UI (interface com o usuário)
{: #tutorials_UI}

* [Tutorial - Catálogo de loja](tutorial_store_catalog.html)


### Tutoriais do iniciador de código
{: #tutorials_Code}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Idioma do Watson](tutorial_watson_language.html)
* [Tutorial - Clima](tutorial_weather.html)

