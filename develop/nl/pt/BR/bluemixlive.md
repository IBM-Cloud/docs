---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Se você estiver construindo um aplicativo Node.js, será possível usar o {{site.data.keyword.Bluemix}} Live Sync para atualizar rapidamente a instância do aplicativo no {{site.data.keyword.Bluemix_notm}} e desenvolver sem reimplementar manualmente.   
{: shortdesc}

Quando você
fizer uma mudança, será possível ver essa mudança no aplicativo {{site.data.keyword.Bluemix_notm}} em execução
imediatamente. O {{site.data.keyword.Bluemix_notm}} Live Sync funciona 
<!--from both the command line and -->
no Eclipse Orion Web IDE (Web IDE). É possível depurar aplicativos gravados em Node.js usando o {{site.data.keyword.Bluemix_notm}} Live Sync.  

O {{site.data.keyword.Bluemix_notm}} Live Sync consiste em dois recursos.
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

É possível fazer mudanças em um aplicativo Node.js em execução no {{site.data.keyword.Bluemix_notm}} e testá-las diretamente em seu navegador. As mudanças feitas no Web IDE são propagadas para o sistema de arquivos do aplicativo imediatamente.  

**Debug**  

Enquanto um aplicativo Node.js estiver no modo Live Edit, é possível executar shell nele
e depurá-lo. É possível editar o código dinamicamente, inserir pontos de interrupção,
percorrer o código, reiniciar o tempo de execução e muito mais usando o depurador Node Inspector.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

É possível usar o Live Edit para propagar as mudanças em sua área de trabalho de projeto
baseado em nuvem para seu aplicativo em execução. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Se você usar o Live Edit para colocar seu aplicativo no modo Live Edit, será possível depurar o aplicativo em execução.


O processo Bluemix Live Sync é ilustrado no diagrama a seguir.    

Figura 1. O processo do Bluemix Live Sync    

![Imagem do processo do Bluemix Live Sync](images/bluemix-live-sync.png)

Se você estiver desenvolvendo um aplicativo Java que esteja em execução no Liberty, será possível depurar remotamente usando o [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools).


## Live Edit {: #live-edit}

Se você estiver construindo um aplicativo Node.js, ao fazer mudanças no projeto usando o Web IDE, o recurso Live Edit do {{site.data.keyword.Bluemix_notm}} Live Sync pode atualizar rapidamente a instância de aplicativo em execução no {{site.data.keyword.Bluemix_notm}}. O Live Edit permite desenvolver como faria no desktop sem reimplementação.

O Live Edit é suportado para aplicativos Node.js apenas

No Eclipse Orion Web IDE (Web IDE), na barra de execução, clique em **Live Edit**.

![Imagem da barra Executar com Live Edit](images/bluemix-live-sync-light.png)

Live Edit permite visualizar rapidamente as mudanças nos aplicativos Node.js em execução no {{site.data.keyword.Bluemix_notm}}. Ao atualizar
seu código com o Live Edit ligado, é possível atualizar sua janela do navegador de aplicativo da Web para
ver essas mudanças refletidas segundos após criá-los.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Ao mudar os arquivos no Web IDE, eles são automaticamente reimplementados para seu aplicativo em execução no {{site.data.keyword.Bluemix_notm}}. Se você precisar reiniciar o aplicativo Node, então é possível usar o botão
**Reiniciar** na barra de execução.

**NOTA:** para uma experiência mais consistente ao usar o recurso Live Edit do {{site.data.keyword.Bluemix_notm}} Live Sync, memória adicional de 256 MB é necessária e
será incluída.

## {{site.data.keyword.Bluemix_notm}} Live
Debug {: #live-debug}

É possível acessar o recurso Debug do {{site.data.keyword.Bluemix_notm}} Live Sync quando o {{site.data.keyword.Bluemix_notm}} Live Sync está ativado para o app Node.js.

Com o Debug, é possível editar código dinamicamente, inserir pontos de interrupção, percorrer o código, reiniciar o tempo de execução e muito mais, tudo enquanto seu app está sendo entregue pelo {{site.data.keyword.Bluemix_notm}}. É possível desenvolver incrementalmente seu app com agilidade ao escolher
a partir da grande lista de serviços {{site.data.keyword.Bluemix_notm}}.

O {{site.data.keyword.Bluemix_notm}} Live
Debug inclui os recursos a seguir:

* Controle de tempo de execução do aplicativo
* Depuração usando o [node-inspector![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/node-inspector/node-inspector){:new_window}
* Acesso ao shell

### Controle de tempo de execução do aplicativo {: #app-runtime}

Com o controle de tempo de execução do aplicativo, é possível usar o Debug
para inspecionar o estado do app no horário de início. Esse recurso é útil
quando você está solucionando problemas de um app que trava no início.

Enquanto você está desenvolvendo seu app, é possível selecionar a partir das
ações a seguir:

* Executar uma reinicialização rápida do app
* Suspender o app antes da execução de qualquer código de app

### Depurar {: #debug}

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

### Shell {: #shell}

Essa ferramenta lhe concede acesso ao shell para o contêiner no qual
seu app está em execução. Usando esse terminal, é possível executar remotamente
os comandos shell de diagnóstico para administrar seu app.

Monitore o uso de memória e CPU na instância que usa comandos Linux padrão, como **top**, **ps** e **kill**.

### Configurando um app para ativar o {{site.data.keyword.Bluemix_notm}} Live
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

Envie por push o aplicativo e, em seguida, navegue para `https://app-host.mybluemix.net/bluemix-debug/manage` para acessar a interface com o usuário de depuração do
{{site.data.keyword.Bluemix_notm}}. Quando for solicitado que você autentique, insira o seu ID do usuário e o token de acesso pessoal ou a senha do ID IBM.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

### Restaurando configurações do app e desativando o Bluemix Live Debug {: #restore_live_debug}

1. Remova a variável de ambiente ENABLE_BLUEMIX_DEV_MODE do arquivo `manifest.yml` do app.

2. Restaure o comando inicial e o valor de memória originais do app.

3. Envie por push o app.


## Links Relacionados
{: #general}

* [Eclipse Tools for Bluemix![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
