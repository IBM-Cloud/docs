---



copyright:

  years: 2015，2017

lastupdated: "2016-03-02"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Iniciar a codificação com Git

É possível criar um repositório Git hospedado que é implementado no {{site.data.keyword.Bluemix}} automaticamente. Em seguida, é possível modificar o código que é executado em seu app enviando por push as mudanças
para o repositório Git.
{:shortdesc}

1. Para iniciar, na página Visão geral do app, clique em **Incluir repositório Git e pipeline** ou, em {{site.data.keyword.Bluemix_notm}} Classic Experience, clique em **INCLUIR GIT**.
2. Na janela que é aberta, certifique-se de que a caixa de seleção **Preencher o repositório com o pacote inicial do app e ativar o pipeline Construir e implementar** esteja selecionada. O repositório Git é criado. Se o código de início estiver disponível,
ele será carregado no repositório. Além disso, o aplicativo é implementado pelo serviço Delivery Pipeline em execução no {{site.data.keyword.jazzhub}}.
3. Para atualizar seu app, é possível usar a linha de comandos ou o Web IDE.
   **Se você usar a linha de comandos:**
   a. Clone seu repositório Git por meio da URL do Git na página Visão geral do app.
   b. Em seu editor favorito, atualize o código.
   c. Na interface da linha de comandos do Git, envie suas mudanças por push.

   **Se você usar o Web IDE:**
   a. Na página Visão geral do app, clique em **Editar código**. Seu projeto é aberto no Web IDE.
   b. Faça as mudanças necessárias e, em seguida, envie por push usando o suporte integrado do Git.

O app atualizado é reimplementado no {{site.data.keyword.Bluemix_notm}}.

Para obter direções passo a passo, veja [Configurar a integração e a implementação automática do Git no DevOps Services ![Ícone de link externo](../icons/launch-glyph.svg)](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment){: new_window}.

## Git incluído? Tente o {{site.data.keyword.Bluemix_notm}} Live Sync

Se você estiver construindo um app Node.js, será possível usar o {{site.data.keyword.Bluemix_notm}} Live Sync para atualizar rapidamente a instância do app no {{site.data.keyword.Bluemix_notm}} e desenvolver da forma usual na área de trabalho.

Para saber mais sobre o {{site.data.keyword.Bluemix_notm}} Live Sync, consulte [{{site.data.keyword.Bluemix_notm}} Live Sync](/docs/develop/bluemixlive.html). Para obter mais detalhes sobre os comandos, veja a [Documentação de CLI do {{site.data.keyword.Bluemix_notm}} Live Sync](/docs/cli/reference/bl/index.html). Para usar o {{site.data.keyword.Bluemix_notm}} Live Sync com o Web IDE, consulte [Live Edit.](/docs/develop/bluemixlive.html).

Antes de iniciar, faça download e instale a linha de comandos bl do
{{site.data.keyword.Bluemix_notm}} Live Sync.

**Importante:** a ferramenta de linha de comandos bl está disponível somente para Windows 7 e 8 e Mac OS X versão 10.9 ou posterior.

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Fazer download do botão da linha de comandos bl do Windows" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Fazer download do botão da linha de comandos bl do Mac" /> </a>
</p>

1. Em uma linha de comandos, efetue login inserindo o comando a seguir:
```
bl login
```
Quando solicitado, insira o {{site.data.keyword.ibmid}} e a senha.

2. Consulte a lista de projetos que estão disponíveis para sincronização do {{site.data.keyword.Bluemix_notm}} Live Sync, inserindo o comando a seguir:
```
bl projects
```
Localize o nome do projeto
na lista que corresponde ao seu aplicativo. O nome do projeto tem o formato de seu *alias* | *nome do seu aplicativo*.

3. Sincronize seu ambiente local com o projeto no {{site.data.keyword.Bluemix_notm}}, inserindo o comando a seguir. Se você for o proprietário do projeto, só precisará especificar o nome do seu aplicativo para projectName.
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
Esse comando continua em execução (e a sincronização continua) até que você insira um
"q". A opção --verbose exibe as informações de criação de log e de status. Se algum de seus argumentos
contiver um espaço, precisará colocar o nome entre aspas.

4. Em outra janela da linha de comandos, em seu diretório local, implemente o aplicativo para
{{site.data.keyword.Bluemix_notm}} no modo Live Edit, inserindo o comando a seguir:
```
bl start
```

Ao alterar os arquivos em seu diretório local, as mudanças são automaticamente propagadas para ambos,
o aplicativo que está sendo executado no {{site.data.keyword.Bluemix_notm}} e a área de trabalho de nuvem do projeto. Se for necessário reiniciar o aplicativo Node,
é possível usar o comando a seguir:
```
bl start --restart
```
