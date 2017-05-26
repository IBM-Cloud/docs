---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Desenvolvendo com o Eclipse Orion Web IDE
{: #web_ide}

O Eclipse Orion {{site.data.keyword.webide}} é um ambiente de desenvolvimento baseado em navegador no qual é possível desenvolver para a web. É possível desenvolver em JavaScript, HTML e CSS com a ajuda de assistência de conteúdo, conclusão de código e verificação de erro. O {{site.data.keyword.webide}} funciona com praticamente qualquer linguagem e oferece destaque da sintaxe para a maioria de tipos de arquivos. O controle de versão é construído e é possível implementar código localmente para testar e depurar os apps.
{:shortdesc}

O melhor de tudo, o {{site.data.keyword.webide}} é desenvolvido com a web. Você não tem nada para instalar, nada para manter e nada para escalar. É possível desenvolver em qualquer lugar no qual haja uma conexão de Internet.

## Configurando o IDE
{: #editorsetup}

O {{site.data.keyword.webide}} é customizável de maneira que é possível escolher os esquemas de cores, as ferramentas técnicas e configurações que atendam às necessidades de desenvolvimento. Para visualizar e modificar as configurações, no menu à esquerda, clique no ícone **Configurações** <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="O ícone de configurações">.

Se for necessário mudar com frequência certas configurações ao editar, será possível acessar essas configurações rapidamente por meio do ícone **Configurações do editor local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Ícone Configurações do editor local">. 

![Configurações do editor local](images/webide_local_editor_settings_light.png)

Por padrão, as configurações para o estilo de editor e o tamanho da fonte são sempre mostradas. Para incluir outras configurações do editor no menu, siga estas etapas:

1. Clique no ícone **Configurações do editor local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Ícone Configurações do editor local">.

2. Clique em **Configurações do editor**.

3. Para incluir ou excluir uma configuração do menu **Configurações do editor local**, clique na estrela próxima a cada configuração.

![alternar Configurações do editor](images/webide_editor_settings_toggle_light.png)


## Editando código
{: #editcode}

O {{site.data.keyword.webide}} tem duas seções. A primeira seção é o navegador de arquivo, que mostra os arquivos de projeto em uma estrutura em árvore. A partir do navegador de arquivo, é possível criar, renomear, excluir e gerenciar os seus arquivos e pastas.

**Dica:** para fazer upload de arquivos no navegador de arquivo, arraste-os a partir de seu computador para o navegador de arquivo.

A segunda seção é a área de janela do editor. O editor fornece vários recursos de codificação, incluindo assistência de conteúdo e validação de sintaxe.

![IDE da web](images/webide_light.png)

### Trabalhando com múltiplos arquivos
1. Para trabalhar com dois arquivos ao mesmo tempo, clique no ícone **Mudar modo do editor de divisão** <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="Ícone Editor de divisão">.
2. A partir do menu que é aberto, selecione uma visualização.

 Após você selecionar uma visualização, se um arquivo já foi aberto no editor, ele será mostrado em ambas as visualizações do editor.

 Para abrir ou mudar um arquivo que é mostrado em uma das visualizações do editor:
 1. Mova o cursor para a visualização do editor que você deseja mudar.
 2. No navegador de arquivo, clique em um arquivo.

### Atalhos pelo Teclado
A maioria dos comandos no {{site.data.keyword.webide}} é acessível somente por meio de atalhos do teclado.

Para ver uma lista de atalhos do teclado no editor, pressione Alt+Shift+?. Se você estiver usando um Mac OS, pressione Ctrl+Shift+?.

## Gerenciamento de código fonte
{: #sourcecontrol}

O {{site.data.keyword.webide}} é integrado com ferramentas de gerenciamento de código-fonte. Para trabalhar com o repositório Git, clique no ícone **Repositório Git** <img class="inline" src="images/webide_git_icon_light_small.png"  alt="O ícone Repositório Git">. 

 **Dica**: se você estiver usando o {{site.data.keyword.webide}} com cadeias de ferramentas abertas, sua área de trabalho será previamente preenchida com os repositórios GitHub, {{site.data.keyword.ghe_short}} ou Git Repos and Issue Tracking. Os repos associados a sua cadeia de ferramentas atual são destacados.


## Implementando um aplicativo a partir de sua área de trabalho
{: #deploy}

1. Para implementar seu app, na barra de execução, selecione ou crie uma configuração de ativação.
1. Clique no ícone de implementação <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="O ícone de implementação">. Uma instância de seu aplicativo é implementada usando os conteúdos atuais de sua área de trabalho e o ambiente que está definido em sua configuração de ativação. 
2. Após o seu aplicativo ser implementado, é possível usar a barra de execução para parar, reiniciar ou depurar o seu aplicativo, visualizar logs e mais.
![Barra de execução](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
