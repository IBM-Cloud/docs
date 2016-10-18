---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao Cloudant
{: #getting-started-with-cloudant}
Última atualização: 12 de agosto de 2016
{: .last-updated}

O {{site.data.keyword.cloudant}} é um banco de dados de documentos como serviço
(DBaaS) que armazena dados no JSON.
Ele é construído com escalabilidade, alta disponibilidade e durabilidade em mente.
Ele é fornecido com uma grande variedade de opções de indexação incluindo map-reduce,
Cloudant Query, indexação de texto total e indexação geoespacial.
Os recursos de replicação facilitam a manutenção de dados em sincronia entre os
clusters de banco de dados, PCs desktop e dispositivos móveis.
{:shortdesc}

É possível ativar o console do {{site.data.keyword.cloudant}} a partir da página
de ativação de serviço no painel do Bluemix.

Para usar o serviço, siga estas etapas:
<ol>
<li>Crie uma instância de serviço usando o painel do Bluemix ou
a interface da linha de comandos CloudFoundry.
<p>Para criar uma instância usando o painel, siga estas etapas:
<ol>
<li>Efetue logon no Bluemix.</li>
<li>No painel, clique no link '<code>Trabalhar com dados</code>' no painel
Dados e Analytics.</li>
<li>Clique no botão '<code>Novo serviço</code>'.</li>
<li>Na lista de serviços, clique no botão {{site.data.keyword.cloudant}}.</li>
<li>Na página de informações {{site.data.keyword.cloudant}},
clique no botão '<code>Escolher {{site.data.keyword.cloudant}}</code>'.</li>
<li>Na página do catálogo {{site.data.keyword.cloudant}},
preencha os detalhes para o serviço necessário.
Clique no botão '<code>Criar</code>' quando estiver pronto para continuar.</li>
<li>Quando a instância Cloudant tiver sido criada, você será apresentado com o painel
para tal instância.
Clique no link '<code>Credenciais de serviço</code>' para ver todos os detalhes necessários
para acessar sua instância.</li>
</ol>
</p>
<p>Para criar uma instância usando a interface da linha de comandos CloudFoundry,
siga estas etapas:
<ol>
<li>Instale a ferramenta <code>cf</code> da CloudFoundry em seu sistema.
Instruções sobre como fazer isso podem ser localizadas no <a href="https://console.ng.bluemix.net/docs/cli/index.html">guia da CLI e ferramentas de desenvolvimento Bluemix</a>.</li>
<li>Crie uma nova instância de serviço usando o comando:<br/>
<pre><code>cf create-service</code></pre></li>
<li>Você será apresentado com uma lista de serviços disponíveis.
Escolha um, em seguida, insira um nome exclusivo da instância e
planeje o serviço.
Um nome aleatório é sugerido para a instância, mas se você preferir, será
possível mudá-la para algo diferente. </li>
<li>Após criar o serviço, você poderá obter uma lista de todos os serviços criados:<br/>
<pre><code>cf services</code></pre></li>
<li>Antes de usar um serviço em um aplicativo, deve-se ligar o serviço ao seu aplicativo.
Faça isso usando o comando:<br/>
<pre><code>cf bind-service</code></pre>
Na lista resultante, selecione um dos aplicativos e um dos serviços.
O comando <code>cf</code> o notifica quando a ação de ligação é bem-sucedida.</li>
</ol>
</p>
</li>
<li><p>Após criar uma instância de serviço, dados JSON semelhantes aos seguintes serão
exibidos e poderão ser visualizados no painel do Bluemix:<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>Os dados também são adicionados à variável de ambiente <code>VCAP_SERVICES</code> de qualquer aplicativo Bluemix ao qual o serviço esteja vinculado.</p>
<p>Credenciais de serviço estão armazenadas em um objeto JSON contendo os campos a seguir:
<ul>
<li><code>key</code>: o nome do serviço (cloudantNoSQLDB)</li>
<li><code>name</code>: o nome fornecido pelo usuário da instância de serviço</li>
<li><code>host</code>: o nome de host do servidor</li>
<li><code>port</code>: o número da porta em que o serviço está em execução, geralmente 443</li>
<li><code>username</code>: o nome do usuário para autenticação</li>
<li><code>password</code>: a senha para autenticação</li>
<li><code>url</code>: a URL da instância de serviço</li>
</ul></li>
<li><p>Em seus aplicativos Bluemix, leia as credenciais da variável de ambiente
<code>VCAP_SERVICES</code>.</p>
<p>Em aplicativos que são executados fora do Bluemix ou em uma região geográfica diferente
dentro do Bluemix, é possível recuperar as credenciais do painel Bluemix e incluí-las na
configuração do seu aplicativo.</p>
</li>
<li>Para acessar o banco de dados, o mecanismo básico é enviar solicitações para o host
e a porta fornecidos HTTPS, usando o nome do usuário e a senha para autenticar.
Suas solicitações podem ser enviadas usando uma variedade de linguagens de aplicativos
e plataformas, incluindo:
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C e Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... e muitos outros.
Para obter mais informações, veja a <a href="https://cloudant.com/for-developers/">página
inicial do Cloudant</a> e a lista de <a href="http://docs.cloudant.com/libraries.html">Bibliotecas
do cliente</a>.
</li>
<li>Quando seu aplicativo estiver pronto, será possível implementá-lo no ambiente
Bluemix para verificação.
Para implementar um aplicativo, use o comando:<br/>
<pre><code>cf push</code></pre></li>
<li>Para desvincular uma instância de serviço de um aplicativo,
use o comando:<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>Para excluir uma instância de serviço, use
o comando:<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

Mais informações sobre como autenticar o banco de dados e fazer solicitações estão disponíveis na [Referência de API](https://docs.cloudant.com/api.html).

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Bibliotecas do cliente Cloudant](https://docs.cloudant.com/libraries.html)
* [Usando Cloudant com Liberty no Bluemix](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Guias do Cloudant](https://docs.cloudant.com/guides.html)

## Referência da API
{: #api}

* [Referência de API do Cloudant](https://docs.cloudant.com/api.html)

## Links relacionados
{: #general}

* [Site e painel do Cloudant](https://cloudant.com/)
* [Blog do Cloudant](https://cloudant.com/blog)
