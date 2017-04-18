---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Editando código com o Eclipse Orion {{site.data.keyword.webide}}
{: #web_ide}

Última atualização: 9 de setembro de 2016
{: .last-updated}

O Eclipse Orion {{site.data.keyword.webide}} é um ambiente de desenvolvimento baseado em navegador no qual é possível desenvolver para a web. É possível desenvolver em JavaScript, HTML e CSS com a ajuda de assistência de conteúdo, conclusão de código e verificação de erro. O {{site.data.keyword.webide}} funciona com praticamente qualquer idioma e oferece destaque da sintaxe para a maioria dos tipos de arquivos [ (O link é aberto em uma nova janela)](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. O controle de fonte é construído por meio do Git ou Jazz SCM e é possível implementar código localmente para testar e depurar os seus aplicativos.
{:shortdesc}

O melhor de tudo, o {{site.data.keyword.webide}} é desenvolvido com a web. Você não tem nada para instalar, nada para manter e nada para escalar. É possível desenvolver em qualquer lugar no qual haja uma conexão de Internet.

## Configurando o editor
{: #editorsetup}

O {{site.data.keyword.webide}} é customizável de maneira que é possível escolher os esquemas de cores, as ferramentas técnicas e configurações que atendam às necessidades de desenvolvimento. Para visualizar e modificar configurações, a partir do menu à esquerda, clique no ícone **Configurações** <img class="inline" src="./images/webide_settings_icon.png"  alt="O ícone configurações">.

Se muitas vezes você precisar mudar certas configurações enquanto edita, será possível acessar essas configurações de forma rápida a partir do ícone **Configurações do editor local** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="ícone Configurações do editor local"> no canto superior direito do editor

![Configurações do editor local](images/webide_local_editor_settings.png)

Por padrão, as configurações para o estilo de editor e o tamanho da fonte são sempre mostradas. Para incluir outras configurações do editor no menu, siga estas etapas:

1. Clique no ícone **Configurações do editor local** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="ícone Configurações do editor local">.

2. Clique em **Configurações do editor**.

3. Para incluir ou excluir uma configuração a partir do menu de **Configurações do editor local**, clique no círculo que está próximo da configuração.

![Botão de alternância de Configurações do editor](images/webide_editor_settings_toggle.png)


## Editando código
{: #editcode}

O {{site.data.keyword.webide}} tem duas seções. A primeira seção é o navegador de arquivo à esquerda, que mostra os seus arquivos de projeto em uma estrutura em árvore. A partir do navegador de arquivo, é possível criar, renomear, excluir e gerenciar os seus arquivos e pastas.

**Dica:** para fazer upload de arquivos no navegador de arquivo, arraste-os a partir de seu computador para o navegador de arquivo.

A segunda seção é a área de janela do editor à direita. O editor fornece vários recursos de codificação, incluindo assistência de conteúdo e validação de sintaxe.

![IDE da Web](images/webide.png)

### Trabalhando com múltiplos arquivos
1. Para trabalhar com dois arquivos ao mesmo tempo, clique no ícone **Mudar modo do editor de divisão** <img class="inline" src="./images/webide_split_editor_icon.png"  alt="ícone Editor de divisão"> na parte superior do editor.
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

O {{site.data.keyword.webide}} é integrado com ferramentas de gerenciamento de código-fonte. Para trabalhar com o seu repositório Git, clique no ícone **Repositório Git ** <img class="inline" src="./images/webide_git_icon.png"  alt="O ícone Repositório Git">. Para obter mais informações, consulte [Controle de fonte com Git (O link é aberto em uma nova janela)](https://hub.jazz.net/docs/git/){: new_window}.


## Implementando um aplicativo a partir de sua área de trabalho
{: #deploy}

1. Para implementar o seu aplicativo, a partir da barra de execução, selecione ou [crie (O link é aberto em uma nova janela)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} uma configuração de ativação.
1. Clique no ícone de implementação <img class="inline" src="./images/webide_deploy_button.png"  alt="O ícone de implementação">. Uma instância de seu aplicativo é implementada usando os conteúdos atuais de sua área de trabalho e o ambiente que está definido em sua configuração de ativação. 
2. Após o seu aplicativo ser implementado, é possível usar a barra de execução para parar, reiniciar ou depurar o seu aplicativo, visualizar logs e mais.
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

Para usar um editor além do {{site.data.keyword.webide}}, configure o {{site.data.keyword.Bluemix_live}} para que seja possível trabalhar diretamente com os seus arquivos de projeto em qualquer ferramenta. O {{site.data.keyword.Bluemix_live_notm}} é um aplicativo de linha de comandos que sincroniza as mudanças em seu sistema de arquivos local com a sua área de trabalho de nuvem no {{site.data.keyword.jazzhub}}. 

### Antes de Começar 

Faça download e instale a interface da linha de comandos do [{{site.data.keyword.Bluemix_live_notm}} (O link é aberto em uma nova janela)](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Sincronizando o seu ambiente local com o {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Abra uma janela de linha de comandos.
2. Conecte-se ao {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. Quando você for avisado, insira o seu ID IBM e senha.
4. Visualize uma lista de seus projetos do {{site.data.keyword.Bluemix_notm}}: 

	```
	bl projects
	```
	{: pre}

4. Sincronize o seu ambiente local com os seus projetos no {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

Em que `projectName` é o seu nome do aplicativo {{site.data.keyword.Bluemix_notm}}.

Quando você concluir a edição, insira `q` para terminar a sincronização.

### Ativando o recurso Desktop Sync para editar código localmente

O recurso Desktop Sync é como o modo Live Edit para a linha de comandos. Você precisa do recurso Desktop Sync para depurar a linha de comandos.
1. Em uma outra linha de comandos, ative o recurso Desktop Sync:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use a configuração de ativação que você criou no {{site.data.keyword.webide}}. Após você selecionar a configuração de ativação, o recurso Desktop Sync será ativado em seu ambiente local. Na
janela de linha de comandos que você acaba de abrir, é possível visualizar a URL do aplicativo, a URL de depuração, a URL de gerenciamento e visualizar o estado do
{{site.data.keyword.Bluemix_live_notm}}.

3. Atualize o navegador e verifique se você pode ver as mudanças que salvou nos arquivos estáticos na área de trabalho local. 

### Desativando o recurso Desktop Sync

1. Na segunda janela de linha de comandos, insira `bl stop`.
2. Na primeira janela de linha de comandos, insira `q`.
