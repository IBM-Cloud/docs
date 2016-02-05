{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Última atualização: 8 de dezembro de 2015*  

Se você estiver construindo um aplicativo Node.js, será possível usar o {{site.data.keyword.Bluemix}} Live Sync para atualizar rapidamente a instância do aplicativo no {{site.data.keyword.Bluemix_notm}} e desenvolver da forma usual na área de trabalho sem reimplementar.   
{: shortdesc} 

Quando você
fizer uma mudança, será possível ver essa mudança no aplicativo {{site.data.keyword.Bluemix_notm}} em execução
imediatamente. O {{site.data.keyword.Bluemix_notm}} Live Sync funciona a partir da linha de comandos e no Web IDE. É possível depurar aplicativos gravados em Node.js usando o {{site.data.keyword.Bluemix_notm}} Live Sync.  

O {{site.data.keyword.Bluemix_notm}} Live Sync consiste em três recursos. 

**Desktop Sync**  
    É possível sincronizar qualquer árvore de diretórios da área de trabalho com uma área de trabalho de projeto baseada em nuvem, semelhante ao modo de funcionamento do Dropbox. O Web IDE edita diretamente a mesma área de trabalho baseada em nuvem, para que ambas permaneçam em sincronização. O Desktop Sync funciona para qualquer tipo de aplicativo. Para usar
o Desktop Sync, você precisa fazer download e instalar a interface da linha de comandos BL.  
	
**Live Edit**	
    É possível fazer mudanças em um aplicativo Node.js em execução no {{site.data.keyword.Bluemix_notm}} e testá-las diretamente em seu navegador. As mudanças feitas em um diretório de área de trabalho sincronizado ou no Web IDE são propagadas para o sistema de arquivos do aplicativo imediatamente.  
	
**Debug**  
    Enquanto um aplicativo Node.js estiver no modo Live Edit, é possível executar shell nele
e depurá-lo. É possível editar o código dinamicamente, inserir pontos de interrupção,
percorrer o código, reiniciar o tempo de execução e muito mais usando o depurador Node Inspector.  

É possível usar o Desktop Sync para manter sua área de trabalho de desktop em sincronização com a área de trabalho do projeto baseado em nuvem que você edita diretamente com o Web IDE. É possível usar o Live Edit para propagar as mudanças em sua área de trabalho de projeto
baseado em nuvem para seu aplicativo em execução. É possível usar um ou ambos os recursos. E se você usar o Desktop Sync ou o Live Edit para colocar seu aplicativo no modo
Live Edit, poderá depurar seu aplicativo em execução.

O processo Bluemix Live Sync é ilustrado no diagrama a seguir.	

*Figura 1. O processo Bluemix Live Sync*
![Imagem do processo Bluemix Live Sync](images/bluemix-live-sync.png)
 
Se você estiver desenvolvendo um aplicativo Java que esteja em execução no Liberty, será possível depurar remotamente usando o [Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools).

##Desktop Sync {: #desktop-sync} 

É possível usar o recurso Desktop Sync do Bluemix Live Sync para atualizar rapidamente a instância de aplicativo no {{site.data.keyword.Bluemix_notm}} e desenvolver da forma usual na área de trabalho. 

O Desktop Sync tem as considerações a seguir: 
* O Desktop Sync é executado nestes sistemas operacionais: 
  * Windows 7 ou 8
  * Mac OS X versão 10.9 ou mais recente
**Nota:** o Windows requer .NET Framework versão 4.5. Se o .NET não estiver instalado, sua instalação será solicitada durante a instalação da interface de linha de comandos (CLI) do {{site.data.keyword.Bluemix_notm}} Live Sync.  
* Não é necessário clonar seu repositório Git. 
* Não importa o tipo de aplicativo que você está desenvolvendo, é possível sincronizar seu projeto de desktop com a área de trabalho de nuvem. 
* Se seu aplicativo for gravado em Node.js, será possível propagar as mudanças para aplicativos em execução.

Para obter mais detalhes sobre os comandos, consulte a [doc da CLI do Bluemix Live Sync](../cli/reference/bl/index.html). 

<ol>
<li>Faça download e instale a linha de comandos bl do {{site.data.keyword.Bluemix_notm}} Live Sync.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Fazer download do botão da linha de comandos bl do Windows" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Fazer download do botão da linha de comandos bl do Mac" /> </a>
</p>  

<strong>Importante:</strong> a ferramenta de linha de comandos bl está disponível somente para Windows 7 e 8 e Mac OS X versão 10.9 ou posterior. </li>
<li>Em uma linha de comandos, efetue login usando o comando a seguir. Você será solicitado a fornecer o ID e a senha IBM.  
<pre class="codeblock">bl login</pre>
</li>

<li>Consulte a lista de projetos que estão disponíveis para sincronização do {{site.data.keyword.Bluemix_notm}} Live Sync, inserindo o comando a seguir: 
<pre class="codeblock">bl projects</pre>
<p>Localize o nome do projeto
na lista que corresponde ao seu aplicativo. O nome do projeto tem o formato de seu <i>alias</i> | <i>nome do seu aplicativo</i>. </p>
</li>
<li>Sincronize seu ambiente local com o projeto no {{site.data.keyword.Bluemix_notm}}, inserindo o comando a seguir. Se você for o proprietário do projeto, só precisará especificar o nome do seu aplicativo para projectName. 
<pre class="codeblock">bl sync projectName -d localDirectory --verbose</pre>
<p>Esse comando continua em execução (e a sincronização continua) até que você insira um
"q". A opção --verbose exibe as informações de criação de log e de status. Se algum de seus argumentos
contiver um espaço, precisará colocar o nome entre aspas. </p></li>
<li>Em outra janela da linha de comandos, em seu diretório local, implemente o aplicativo para
{{site.data.keyword.Bluemix_notm}} no modo Live Edit, inserindo o comando a seguir:
<pre class="codeblock">bl start</pre>
</li>
</ol>

Ao alterar os arquivos em seu diretório local, as mudanças são automaticamente propagadas para ambos,
o aplicativo que está sendo executado no {{site.data.keyword.Bluemix_notm}} e a área de trabalho de nuvem do projeto. Se for necessário reiniciar o aplicativo Node,
é possível usar o comando a seguir:
```
bl start --restart 
```

##Live Edit {: #live-edit} 

Se você estiver construindo um aplicativo Node.js, ao fazer mudanças no projeto usando o Web IDE, o recurso Live Edit do {{site.data.keyword.Bluemix_notm}} Live Sync pode atualizar rapidamente a instância de aplicativo em execução no {{site.data.keyword.Bluemix_notm}}. O Live Edit permite desenvolver como faria no desktop sem reimplementação. 

O Live Edit é suportado para aplicativos Node.js apenas 

No Web IDE, na barra de execução, clique em **Live Edit**. 

![Imagem da barra Executar com Live Edit](images/run-bar-live-edit.png) 

Live Edit permite visualizar rapidamente as mudanças nos aplicativos Node.js em execução no {{site.data.keyword.Bluemix_notm}}. Ao atualizar
seu código com o Live Edit ligado, é possível atualizar sua janela do navegador de aplicativo da Web para
ver essas mudanças refletidas segundos após criá-los. 

Para obter um tutorial sobre o uso do recurso Live Edit do {{site.data.keyword.Bluemix_notm}} Live Sync, consulte o tutorial [Testar e depurar um app Node.js com o Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

Ao mudar os arquivos no Web IDE, eles são automaticamente reimplementados para seu aplicativo em execução no {{site.data.keyword.Bluemix_notm}}. Se você precisar reiniciar o aplicativo Node, então é possível usar o botão
**Reiniciar** na barra de execução.

##{{site.data.keyword.Bluemix_notm}} Live
Debug {: #live-debug}

É possível acessar o recurso Debug do {{site.data.keyword.Bluemix_notm}} Live Sync quando o {{site.data.keyword.Bluemix_notm}} Live Sync está ativado para o app Node.js. 

Com o Debug, é possível editar código dinamicamente, inserir pontos de interrupção, percorrer o código, reiniciar o tempo de execução e muito mais, tudo enquanto seu app está sendo entregue pelo {{site.data.keyword.Bluemix_notm}}. É possível desenvolver incrementalmente seu app com agilidade ao escolher
a partir da grande lista de serviços {{site.data.keyword.Bluemix_notm}}. 

O {{site.data.keyword.Bluemix_notm}} Live
Debug inclui os recursos a seguir:

* Controle de tempo de execução do aplicativo
* Depuração usando o [node-inspector](https://github.com/node-inspector/node-inspector)
* Acesso ao shell 

###Controle de tempo de execução do aplicativo {: #app-runtime} 

Com o controle de tempo de execução do aplicativo, é possível usar o Debug
para inspecionar o estado do app no horário de início. Esse recurso é útil
quando você está solucionando problemas de um app que trava no início.

Enquanto você está desenvolvendo seu app, é possível selecionar a partir das
ações a seguir:

* Executar uma reinicialização rápida do app
* Suspender o app antes da execução de qualquer código de app

###Depurar {: #debug} 

O Debug inclui os recursos a seguir:

**Restrição:** o Google Chrome é necessário.

* Veja os pontos de interrupção no código do app para pausar a execução em uma linha
específica.
* Edite as condições do ponto de interrupção para pausar a execução somente quando
determinados critérios forem atendidos. 
* Inspecione o estado das variáveis e dos campos locais. 
* Visualize a saída de depuração das chamadas `console.log()` imediatamente. Essa ação
é mais rápida do que monitorar logs cf.
* Use o editor de código-fonte integrado para fazer mudanças imediatas, ou mesmo
temporárias, no código do app em execução.

###Shell {: #shell} 

Essa ferramenta lhe concede acesso ao shell para o contêiner no qual
seu app está em execução. Usando esse terminal, é possível executar remotamente
os comandos shell de diagnóstico para administrar seu app. 

Monitore o uso de memória e CPU na instância que usa comandos Linux padrão, como **top**, **ps** e **kill**. 

###Configurando um app para ativar o {{site.data.keyword.Bluemix_notm}} Live
Debug {: #configure_app_debug} 

O app deve usar o buildpack do IBM SDK for Node.js. Não há suporte para buildpacks customizados. 

1. Permita que o buildpack detecte o comando inicial do app. O comando inicial deve ser detectado automaticamente pelo buildpack, não configurado no arquivo `manifest.yml`.  
    
    a. Assegure-se de que o arquivo `package.json` contenha um script de início que inclua um comando inicial para o app.  
    b. Se o arquivo `manifest.yml` do app contiver um comando, configure-o como nulo.  

2. Configure a variável de ambiente.  
    
    a. No arquivo `manifest.yml`, inclua esta variável: 
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. Aumente a memória.  
    
    a. No arquivo `manifest.yml` do app, inclua 128 M ou mais no valor especificado para o atributo de memória. 
	
Após a instalação do {{site.data.keyword.Bluemix_notm}} Live
Debug, é possível usar as ferramentas de depuração.

Envie por push o app e, em seguida, procure em `https://app-host.mybluemix.net/bluemix-debug/manage` para acessar a interface com o usuário de depuração do {{site.data.keyword.Bluemix_notm}}. Quando solicitado, insira seu ID e senha IBM para autenticação. 

###Restaurando configurações do app e desativando o Bluemix Live Debug {: #restore_live_debug} 

1. Remova a variável de ambiente ENABLE_BLUEMIX_DEV_MODE do arquivo `manifest.yml` do app.

2. Restaure o comando inicial e o valor de memória originais do app. 

3. Envie por push o app.


># Links Relacionados {:class="linklist"}
>## Tutoriais e Amostras {:id="samples"}
>* [Testar e depurar um app Node.js com o Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Links Relacionados {:class="linklist"}
>## links relacionados {:id="general"}
>* [Comandos bl](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
