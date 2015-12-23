{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Implementando seu app com a interface da linha de comandos Cloud Foundry
*Última atualização: 11 de novembro de 2015*

É possível usar a interface de linha de comandos Cloud Foundry para implementar e modificar aplicativos e instâncias de serviço.
{:shortdesc}

Antes de iniciar, instale a interface de linha de comandos cf.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_cf_commandline.svg" alt="Fazer download da interface de linha de comandos do Cloud Foundry" /> </a>
</p>

**Restrição:** A interface de linha de
comandos do Cloud Foundry não é suportada por
Cygwin. Use a interface de linha de comandos do Cloud Foundry
em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

Após a instalação da interface de linha de comandos cf, é possível
começar:

  1. Faça o download de seu código de início.
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_starter-code.svg" alt="Fazer download do código de início" /> </a>
</p>
  
  {:download}
  2. Extraia o pacote em um novo diretório para configurar seu
ambiente de desenvolvimento.
  3. Alter para o seu novo diretório.
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
  4. Conecte-se ao {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. Efetue login no {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  6. Implemente seu aplicativo no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre o comando cf push, consulte [Fazendo upload do seu aplicativo](upload_app.html#upload_app__push).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  7. Acesse o app inserindo a URL a seguir no
navegador:
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
