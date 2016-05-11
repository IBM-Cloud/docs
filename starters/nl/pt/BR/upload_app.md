---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Fazendo upload do seu aplicativo
*Última atualização: 17 de fevereiro de 2016*

Depois de ter efetuado login no {{site.data.keyword.Bluemix}}, é possível fazer upload do aplicativo com o comando cf push.
{:shortdesc}

Antes de iniciar, deve-se:
  1. Instale as interfaces de linha de comandos do {{site.data.keyword.Bluemix}} e do Cloud Foundry.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_bx_commandline.svg" alt="Fazer download da interface da linha de comandos do {{site.data.keyword.Bluemix}} " /></a> <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_cf_commandline.svg" alt="Fazer download da interface da linha de comandos do Cloud Foundry" /> </a> 

  2. Conecte-se ao {{site.data.keyword.Bluemix}}.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  3. Efetue login no {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

Quando
um comando **cf push** é emitido, a interface de linha de comandos
**cf** fornece o diretório ativo para o ambiente do
{{site.data.keyword.Bluemix_notm}} que
usa um buildpack para construir e executar o aplicativo.

  1. Em seu diretório de aplicativo, insira o comando **cf push** com o nome do aplicativo. O nome do
app deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</pre>
  
  O {{site.data.keyword.Bluemix_notm}} inclui buildpacks integrados. Em alguns casos, mesmo para os buildpacks integrados, deve-se também fornecer uma opção -c para especificar o comando que é usado para iniciar o aplicativo. Por exemplo, é necessário usar a opção -c para enviar por push o aplicativo Node.js:
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</pre>
  
  Além disso, o aplicativo Node.js deve conter um arquivo package.json válido.

  Todos os outros buildpacks externos devem ser enviados por push usando a opção -b. Por
exemplo:

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</pre>
  
  **Dica:** ao usar o comando **cf push**, a interface da linha de comandos **cf** copia todos os arquivos e diretórios de seu diretório atual para o Bluemix. Assegure-se
de que você tenha apenas os arquivos necessários em seu diretório de aplicativo.

  O comando cf push faz upload e implementa o aplicativo no {{site.data.keyword.Bluemix_notm}}. Consulte [Comandos cf](../cli/reference/cfcommands/index.html) para obter mais informações sobre cf push. Consulte [Usando buildpacks da comunidade](../cfapps/byob.html) para obter informações sobre buildpacks.

  2. Se você mudar seu aplicativo, será possível fazer upload dessas mudanças inserindo o comando cf push novamente. A
interface da linha de comandos cf usa as opções anteriores e as respostas
aos prompts, para atualizar todas as instâncias em execução de seu aplicativo
com os novos bits de código.

**Dica:** também é possível fazer upload ou implementar um aplicativo a partir do DevOps Services. Veja [Desenvolvendo um aplicativo do {{site.data.keyword.Bluemix_notm}} no Node.js com o Web IDE.](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
