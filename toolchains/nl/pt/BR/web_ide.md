---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Editando código com o {{site.data.keyword.webide}} do Eclipse Orion
{: #web_ide}

Última atualização: 22 de julho de 2016
{: .last-updated}

O {{site.data.keyword.webide}} do Eclipse Orion é um ambiente de desenvolvimento baseado no navegador no qual você pode desenvolver para a web. É possível desenvolver em JavaScript, HTML e CSS
com a ajuda do assistente de conteúdo, da conclusão de código e da verificação de erro. O {{site.data.keyword.webide}} funciona com quase qualquer idioma e oferece destaque da sintaxe
[para a maioria dos tipos de arquivos](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. O controle de origem é construído por meio de Git ou Jazz SCM e é possível
implementar código localmente para testar e depurar os seus aplicativos.
{:shortdesc}

O melhor de tudo, o {{site.data.keyword.webide}} é desenvolvido com a web. Você não tem nada a instalar, nada para manter e nada para escalar. É possível desenvolver em qualquer lugar que você
tenha uma conexão de Internet.

## Configurando o editor
{: #editorsetup}

O {{site.data.keyword.webide}} é customizável para que seja possível escolher os esquemas de cores, as ferramentas técnicas e as configurações que atendem às necessidades de desenvolvimento. Para visualizar e modificar as configurações, a partir do menu à esquerda, clique no ícone **Configurações** <img class="inline" src="./images/webide_settings_icon.png"  alt="O ícone de Configurações">.

<!-- LH: I don't think we need to include the following table, so I'm commenting it out. When you're viewing the settings in the Web IDE, this information should be obvious -->

<!--| Categories | Description  |
|---|---|
| Cloud Foundry  | Define a Cloud Foundry API and Manage URL  |
| CSS Validation | Define the severities for CSS linting rules that you use to check your code  |
| Editor Settings  | Configure editor-specific settings for key bindings, editor behavior, layout, and more  |
| Editor Styles  | Configure color schemes for the languages that you use, or import a theme from another editors  |
| Git  | Configure general settings for Git  |
| Globalization | Define globalization settings for your code |
| JavaScript Validation  | Define the severities for the JavaScript linting rules that you use to check your code  |
| Plug-ins  | Install, disable, or remove plug-ins from the editor  | -->

Se você frequentemente precisar mudar certas configurações enquanto edita, será possível acessar essas configurações rapidamente a partir do ícone **Configurações do editor local**
<img class="inline" src="./images/webide_local_settings_icon.png"  alt="ícone Configurações do editor local"> no canto superior direito do editor

![Configurações do editor local](images/webide_local_editor_settings.png)

Por padrão, as configurações para o estilo e o tamanho da fonte do editor são sempre mostradas. Para incluir outras configurações do editor no menu, siga estas etapas:

1. Clique no ícone **Configurações do editor local** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="ícone Configurações do editor local">.

2. Clique em **Configurações do editor**.

3. Para incluir ou excluir uma configuração a partir do menu **Configurações do editor local**, clique no círculo que está próximo à configuração.

![alternar Configurações do editor](images/webide_editor_settings_toggle.png)


## Editando código
{: #editcode}

O {{site.data.keyword.webide}} tem duas seções principais. A primeira seção é o navegador de arquivo à esquerda, que mostra os seus arquivos de projeto em uma estrutura em árvore. A partir do
navegador de arquivo, é possível criar, renomear, excluir e gerenciar os seus arquivos e pastas.

**Dica:** para fazer upload de arquivos no navegador de arquivo, arraste-os do seu computador para o navegador de arquivo.

A segunda seção é a área de janela do editor à direita. O editor fornece vários recursos de codificação, incluindo assistente de conteúdo e validação de sintaxe.

![Web IDE](images/webide.png)

### Trabalhando com múltiplos arquivos
1. Para trabalhar com dois arquivos ao mesmo tempo, clique ícone **Mudar modo de editor de divisão** <img class="inline" src="./images/webide_split_editor_icon.png"  alt="ícone Editor de divisão"> na parte superior do editor.
2. No menu que é aberto, selecione uma visualização.

 Depois de selecionar uma visualização, se um arquivo já foi aberto no editor, ele será mostrado em ambas as visualizações do editor.

 Para abrir ou mudar um arquivo que é mostrado em uma das visualizações do editor:
 1. Mova o cursor para a visualização do editor que você deseja mudar.
 2. No navegador de arquivo, clique em um arquivo.

### Atalhos do teclado
A maioria dos comandos no {{site.data.keyword.webide}} é acessível somente por meio de atalhos de teclado.

Para ver uma lista dos atalhos de teclado no editor, pressione Alt+Shift+?. Se você estiver usando um Mac OS, pressione Ctrl+Shift+?.

## Gerenciamento de código fonte
{: #sourcecontrol}

O {{site.data.keyword.webide}} é integrado com ferramentas de gerenciamento de código-fonte. Para trabalhar com o seu repositório Git, clique no ícone **Repositório Git**
<img class="inline" src="./images/webide_git_icon.png"  alt="O ícone Repositório Git">. Para obter mais informações, consulte [Controle de fonte com
Git](https://hub.jazz.net/docs/git/){: new_window}.


## Implementando um aplicativo a partir de sua área de trabalho
{: #deploy}

1. Para implementar o seu aplicativo, a partir da barra de execução, selecione ou
[crie](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} uma
configuração de ativação.
1. Clique no ícone implementar <img class="inline" src="./images/webide_deploy_button.png"  alt="O ícone implementar">. Uma instância de seu aplicativo é implementada usando os conteúdos atuais de
sua área de trabalho e o ambiente que está definido em sua configuração de ativação. 
2. Após o seu aplicativo ser implementado, será possível usar a barra de execução para parar, reiniciar ou depurar o seu aplicativo, visualizar logs e mais.
![Barra de execução](images/webide_runbar.png)

<!-- LH: I'm commenting out the following list because I think this information is obvious from the UI. I also updated the preceding sentence to mention a few things that you can do from the run bar.

 * Stop the app: <img  class="inline" src="./images/webide_stop_button.png"  alt="The stop icon">
 * Open the deployed app: <img class="inline" src="./images/webide_open_app_url.png"  alt="The open app URL icon">
 * View the logs of the deployed app: <img class="inline" src="./images/webide_view_logs.png"  alt="The view logs icon">
 * Open the app's Dashboard: <img  class="inline" src="./images/webide_open_dashboard.png"  alt="The open dashboard icon">
 * If you are developing a Node.js app, enable Live Edit mode: <img  class="inline"  src="./images/webide_enable_live_edit.png"  alt="The enable live edit slider">
 * With Live Edit mode enabled, restart the app quickly, without redeployment: <img  class="inline" src="./images/webide_live_edit_restart.png"  alt="The Live Edit restart icon">
 * With Live Edit mode enabled, access the debugger: <img  class="inline" src="./images/webide_debug_icon.png"  alt="The debug icon"> -->

 ## Editando fora do {{site.data.keyword.webide}}
{: #editlocal}

Para usar um editor além do {{site.data.keyword.webide}}, configure o {{site.data.keyword.Bluemix_live}} para que você possa trabalhar diretamente com os seus arquivos de projeto em
qualquer ferramenta. O {{site.data.keyword.Bluemix_live_notm}} é um aplicativo de linha de comandos que sincroniza as mudanças em seu sistema de arquivos local com a sua área de trabalho de nuvem no
{{site.data.keyword.jazzhub}}. 

### Antes de começar 

[Faça download e instale a interface da linha de comandos do {{site.data.keyword.Bluemix_live_notm}}](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Sincronizando o seu ambiente local com o {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Abra uma janela de linha de comandos.
2. Conecte-se ao {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. Quando solicitado, insira o seu ID IBM e senha.
4. Visualize uma lista de seus projetos do {{site.data.keyword.Bluemix_notm}}: 

	```
	bl projects
	```
	{: pre}

4. Sincronize o seu ambiente local com o seu projeto no {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

em que `projectName` é o nome do seu aplicativo {{site.data.keyword.Bluemix_notm}}.

Quando você tiver concluído a edição, insira `q` para terminar a sincronização.

### Ativando o recurso do Desktop Sync para editar código localmente

O recurso do Desktop Sync é como o modo Live Edit para a linha de comandos. É necessário o recurso do Desktop Sync para depuração na linha de comandos.
1. Em outra janela de linha de comandos, ative o recurso do Desktop Sync:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use a configuração de ativação que você criou no {{site.data.keyword.webide}}. Após você selecionar a configuração de ativação, o recurso do Desktop Sync será ativado em seu ambiente
local. Na janela de linha de comandos que você acaba de abrir, é possível visualizar a URL do aplicativo, a URL de depuração, a URL de gerenciamento e visualizar o estado
do {{site.data.keyword.Bluemix_live_notm}}.

3. Atualize o navegador e verifique se você pode ver as mudanças que salvou em arquivos estáticos na área de trabalho local. 

### Desativando o recurso do Desktop Sync

1. Na segunda janela de linha de comandos, insira `bl stop`.
2. Na primeira janela de linha de comandos, insira `q`.
