---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Integrando uma Implementação no Fluxo do {{site.data.keyword.Bluemix_notm}} iFrame
{: #embed-d2bm-iframe}


É possível integrar a Implementação no fluxo do {{site.data.keyword.Bluemix_notm}} como um iFrame em vários tipos de conteúdo que suportam marcação. Por exemplo, é possível integrar o
iFrame em arquivos leia-me, blogs, artigos e em páginas da web.

{: shortdesc}

O fluxo do iFrame é útil quando você desejar manter a marca da sua empresa. Quando as pessoas clicam em seu
iFrame integrado, elas permanecem em seu conteúdo em vez de serem redirecionadas ao website do bluemix.net. Se você não estiver preocupado com a marca da empresa, será possível inserir um botão padrão [Implementar no {{site.data.keyword.Bluemix_notm}}](/docs/develop/deploy_button.html) em seu conteúdo, em vez do iFrame.

##Etapas no fluxo do iFrame {: #iframe-steps}

1. Se você não tiver uma conta ativa do {{site.data.keyword.Bluemix_notm}}, crie uma conta para teste.

2. É possível selecionar uma região, uma organização (org), um espaço e um nome de app. O nome do app sugerido é construído a partir do nome anterior do app, do seu nome de usuário e do horário.

3. A ramificação principal do repositório Git público original é clonada em um projeto
{{site.data.keyword.jazzhub_short}} novo e privado com um novo repositório Git.

4. Se o app requer um arquivo de construção, o arquivo de construção é detectado automaticamente e o app é construído.

5. O app é implementado na organização do {{site.data.keyword.Bluemix_notm}}.

##Exemplo do fluxo do iFrame {: #iframe-example}

<p>
A <a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(Abre em uma nova guia ou janela)">Amostra do
IBM Bluemix D2BM iFrame<img class="image" src="../icons/launch-glyph.svg" alt="Ícone de link externo"/></a> fornece um exemplo de fluxo do iFrame para um repositório Git público.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Implementar na amostra do fluxo de iFrame do Bluemix" /></div>
</p>

<p>
Para visualizar a origem dessa amostra, clique em <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(Abre em uma nova guia ou janela)">origem<img class="image" src="../icons/launch-glyph.svg" alt="Ícone de link externo"/></a>.
</p>

##Integrando o fluxo do iFrame {: #embed-iframe}  

<ol>
<li>Carregue o utilitário JavaScript em <a class="xref" href="https://bluemix.net/deploy/embed.js" target="_blank" title="(Abre em uma nova guia ou janela)">https://bluemix.net/deploy/embed.js<img class="image" src="../icons/launch-glyph.svg" alt="Ícone de link externo"/></a>. Esse utilitário depende do jQuery e é carregado incluindo a tag de script a seguir em seu documento:
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Instancie o construtor <code>DeployToBluemixIFrame</code>, usando estes argumentos:

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">O ID do domNode em que você deseja inserir o iFrame em seu conteúdo.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">Esse argumento é chamado quando o fluxo de iFrame é concluído ou se ocorrer um erro. O argumento responde ao
resultado. O fragmento de código a seguir mostra um retorno de chamada de resultado bem-sucedido:</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">O objeto que contém parâmetros de entrada para o widget. Esses parâmetros estão disponíveis:

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">O repositório Git a ser usado como origem para clonagem e implementação. Esse valor é necessário.</dd>

<dt class="pt dlterm">app_name</dt>
<dd class="pd">O nome do app padrão a ser usado como o valor especificado no campo <strong>app_name</strong>
no iFrame. Esse valor é opcional.</dd>


<dt class="pt dlterm">region_id</dt>
<dd class="pd">O ID da região de destino padrão. Por exemplo: <code>ibm:yp:us-south</code>. Esse valor é opcional.</dd>

<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">O identificador exclusivo global da organização de destino padrão. Para localizar esse valor, clique em <strong>Gerenciar organizações</strong> >
<i>nome_da_organização</i>. A URL para a organização contém o identificador exclusivo global para essa organização. Esse valor é opcional.</dd>

<dt class="pt dlterm">space_guid</dt>
<dd class="pd">O guid é o espaço de destino padrão. Para localizar esse valor, clique em <strong>Gerenciar organizações</strong> > <i>space_name</i>. A URL para o espaço contém o
guid para esse espaço. Esse valor é opcional.</dd>

<dt class="pt dlterm">auto_login</dt>
<dd class="pd">Especifica se o iFrame efetua login do usuário automaticamente. O valor padrão é
<code>true</code>. Esse valor é opcional.</dd>

<dt class="pt dlterm">width</dt>
<dd class="pd">A largura do iFrame. Esse valor é opcional. O valor padrão é <code>620</code>.</dd>

<dt class="pt dlterm">height</dt>
<dd class="pd">A altura do iFrame. Esse valor é opcional. O valor padrão é <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Dica:** para minimizar a interação com o iFrame, é possível preencher os campos **app_name**, **region_id**, **organization_guid**, **space_guid** e **auto_login**.
