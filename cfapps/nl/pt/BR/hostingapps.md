---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Hospedando apps no {{site.data.keyword.Bluemix_notm}}

*Última atualização: 9 de maio de 2016*

<!--The whole topic is staging only -->

Com o {{site.data.keyword.Bluemix}},
é possível criar aplicativos, assim como hospedar seus aplicativos existentes. É possível migrar seus apps para o {{site.data.keyword.Bluemix_notm}},
desde que ele esteja pronto para nuvem. O {{site.data.keyword.Bluemix_notm}} fornece várias maneiras de executar seus aplicativos, por exemplo, Cloud Foundry, IBM Containers e Virtual Machines.

##Tornando seus apps prontos para nuvem
{: #cloud-readyapps}

Um aplicativo pronto para nuvem segue os princípios da plataforma em nuvem,
quando o aplicativo é designado e construído. Um aplicativo pronto para nuvem
pode usar as capacidades fornecidas pela plataforma em nuvem.

Se todos os princípios a seguir forem observados em seu aplicativo, o aplicativo estará pronto para nuvem e poderá
ser migrado para {{site.data.keyword.Bluemix_notm}}. Se um princípio for violado em seu aplicativo, geralmente, será possível modificar
o aplicativo para aderir aos princípios.

* Não codifique seu aplicativo diretamente para uma topologia específica.

  Em
um ambiente que não for de nuvem, o aplicativo poderá usar uma topologia de implementação
específica. No entanto, a topologia do aplicativo pode ser mudada nos aplicativos
em nuvem, porque os aplicativos e serviços prontos para nuvem permitem
mudanças de escalabilidade imediatas. As mudanças de escalabilidade incluem ajuste de escala dinâmico
e redimensionamento manual do número de instâncias de um aplicativo.

  Construa
seu aplicativo para ser o mais genérico e stateless possível, para impedir
que o aplicativo seja afetado pelas mudanças de escalabilidade.

* Não assuma que o sistema de arquivos local seja permanente.

  Como
uma instância do aplicativo pode ser movida, excluída ou duplicada a qualquer
momento na nuvem, não confie nos arquivos que são gravados no sistema
de arquivos. Se um aplicativo usar o sistema de arquivos local como um cache de
informações usadas frequentemente, incluindo logs do aplicativo, as informações
serão perdidas quando a instância for encerrada e reiniciada em um local
ou uma máquina virtual diferentes.

  É possível armazenar informações em um serviço,
como um banco de dados SQL ou NoSQL em vez do sistema de arquivos local. Em um ambiente de nuvem dinâmico, também é essencial que seus logs estejam
disponíveis em um serviço que prolongue as instâncias do aplicativo onde os
logs são gerados.

* Não armazene o estado de sessão em seu aplicativo.

  O estado de
seu sistema é definido pelos bancos de dados e pelo armazenamento compartilhado e não
por cada indivíduo que esteja executando a instância do aplicativo. A condição de stateful de qualquer
classificação limita a escalabilidade de um aplicativo. Tente minimizar o
impacto do estado da sessão armazenando-a em um local centralizado no
servidor.

  Se não for possível eliminar o estado de sessão completamente, envie-o
para um disponível altamente disponível que seja externo ao seu servidor
de aplicativos. Os armazenamentos incluem IBM WebSphere Extreme Scale, Redis ou
Memcached ou um banco de dados externo.

* Não use dependência de infraestrutura específica.

  Esse é um princípio geral
que possui diversas manifestações. Por exemplo, não presuma que os
serviços que seu aplicativo usa sejam nomes do host ou
endereços IP específicos alocados. Como os serviços podem ser realocados ou regenerados
em seu ambiente de nuvem, os nomes do host e endereços IP também podem
ser mudados.

  A extração de dependências específicas do ambiente para um
conjunto de arquivos de propriedade é uma melhoria, mas ainda é inadequada. A melhor prática é usar um registro de serviço externo para resolver
terminais em serviço ou delegar a função de roteamento inteira para um barramento de serviço
ou um balanceador de carga com um nome virtual.

* Não use APIs de infraestrutura em seu aplicativo.

  Se você contar com uma API de infraestrutura específica em seu
aplicativo, mudar a infraestrutura será mais desafiador, porque uma API de infraestrutura
pode referir-se a muitas camadas diferentes em sua pilha de software.

  Em vez disso, é
possível contar com o software livre ou produtos comerciais existentes, e
deixar as soluções PaaS na camada PaaS para mantê-las fora do código do
aplicativo.

* Não use protocolos obscuros.

  Não use protocolos obscuros que
requeiram configuração extra para resiliência.

  Os aplicativos baseados
em protocolos padrão são mais resilientes com os itens de configuração
delegados para a plataforma. Os protocolos padrão incluem HTTP, SSL,
banco de dados padrão, enfileiramento e conexões de serviço da web.

* Não conte com recursos específicos do sistema operacional

  Se você já usou
recursos específicos do sistema operacional, será possível corrigir esse problema usando bibliotecas de
compatibilidade, por exemplo, Cygwin e Mono. Cygwin é uma biblioteca de compatibilidade que fornece um conjunto de ferramentas Linux em um ambiente do Windows. Mono é uma biblioteca de compatibilidade que fornece recursos .NET do Windows no Linux.

  Evite as dependências específicas do sistema operacional;
em vez disso, use serviços que sejam fornecidos pela infraestrutura de middleware
ou por provedores de serviços.

* Não instale seu aplicativo manualmente.

  Seu aplicativo pode
ser instalado frequentemente por demanda no ambiente de nuvem dinâmico. O processo de instalação deve ser por script e confiável, e os dados da configuração
devem ser exteriorizados a partir dos scripts.

  No mínimo, capture
a instalação do aplicativo como um conjunto uniforme de scripts que sejam
independentes do sistema operacional. Mantenha a instalação do aplicativo
pequena e móvel para adaptar-se a diferentes técnicas de automação. Além disso,
minimize as dependências necessárias para a instalação do aplicativo.

Para obter mais informações sobre aplicativos prontos para nuvem, consulte [O aplicativo
de 12 fatores](http://12factor.net/){:new_window}.

##Migrando seus apps
{: #ht_hostapp}

É possível migrar seus aplicativos para o {{site.data.keyword.Bluemix_notm}}
de uma maneira incremental, em vez de deslocar o aplicativo completamente
para o ambiente de nuvem. É possível migrar uma parte de seu aplicativo
primeiro e conectar aos dados existentes ou sistema de registros usando
o serviço de Integração de nuvem.

Em seus aplicativos em nuvem, poderá ser necessário acessar os dados ou serviços
de backend, por exemplo, um sistema de registro. No {{site.data.keyword.Bluemix_notm}},
é possível usar o serviço Secure Gateway para estabelecer um túnel seguro
entre uma organização do {{site.data.keyword.Bluemix_notm}}
e a rede de backend corporativa. O serviço permite que os aplicativos
no {{site.data.keyword.Bluemix_notm}}
acessem os dados e serviços da rede de backend. Para obter detalhes, consulte [Atingindo backend corporativo com o Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

Para implementar seu aplicativo no {{site.data.keyword.Bluemix_notm}} como
um aplicativo Cloud Foundry, selecione um tempo de execução no catálogo {{site.data.keyword.Bluemix_notm}}. O tempo de execução contém um aplicativo iniciador Hello World que pode ser substituído por seu próprio aplicativo. Se não for possível localizar um iniciador que forneça o tempo de execução desejado, será possível trazer um buildpack customizado compatível com Cloud Foundry para o {{site.data.keyword.Bluemix_notm}} usando a opção –b com o comando cf push. Para obter detalhes, consulte [Usando buildpacks da comunidade](../cfapps/byob.html).

É possível usar as ferramentas e serviços a seguir que o {{site.data.keyword.Bluemix_notm}} fornece:

*Tabela 1. Ferramentas do {{site.data.keyword.Bluemix_notm}}*

| Ferramenta	| Método |
|:------|:--------|
|Interface da linha de comandos do Cloud Foundry (cf cli)	|Gerencie seu código no cliente local e use a interface
da linha de comandos do Cloud Foundry para enviar o seu aplicativo por push para o {{site.data.keyword.Bluemix_notm}} manualmente. Para obter mais informações, consulte [Fazendo upload de seus apps](../starters/upload_app.html).|
|Eclipse	|Gerencie seu código no Eclipse e use o IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} para enviar seu aplicativo por push.|
|Integração Git	|Gerencie seu código no GitHub e Git integrado
no {{site.data.keyword.Bluemix_notm}}. É possível colaborar com outros desenvolvedores. Seu aplicativo será implementado
no {{site.data.keyword.Bluemix_notm}} automaticamente,
quando você confirmar as mudanças no código. Não é necessário enviar o aplicativo por push
manualmente.|
|{{site.data.keyword.Bluemix_notm}} DevOps
Delivery Pipeline	|Gerencie seu código no repositório DevOps GitHub
e implemente o aplicativo para {{site.data.keyword.Bluemix_notm}}
usando o DevOps Delivery Pipeline.|


Se a plataforma Cloud Foundry não suportar os requisitos de
seu aplicativo, será possível usar um contêiner ou máquina virtual em que o tempo de execução é
instalado, configurado e mantido com mais opções customizadas.

##Fazendo upload de apps usando cf cli
{: #ht_cfcli}

É
possível gerenciar seu código no cliente local e usar a interface da linha de comandos Cloud Foundry
para fazer upload de seu aplicativo para o {{site.data.keyword.Bluemix_notm}} manualmente. Se você alterar o código, deverá enviar o aplicativo por push para o {{site.data.keyword.Bluemix_notm}} novamente,
para executar o código atualizado.

Execute as etapas a seguir para migrar seu aplicativo.

<ol>
<li>Instale a interface de linha de comandos do Cloud Foundry. Assegure-se
de usar a versão mais recente da interface da linha de comandos cf.
<ol>
<li>Faça download do programa de instalação para seu sistema
operacional.</li>
<li>Siga o assistente de ferramenta para instalar a linha de comandos.</li>
<li>Use o comando a seguir para verificar a versão da interface
da linha de comandos cf:
<pre>cf -v</pre></li>
</ol>
</li>

<li>Opcional: se desejar especificar e salvar os detalhes da implementação antes de enviar um aplicativo por push para o {{site.data.keyword.Bluemix_notm}}, será possível incluir o manifest do aplicativo executando as etapas a seguir:
<ol>
<li>Acesse o diretório ativo de seu aplicativo e crie um arquivo intitulado manifest.yml, que é o nome padrão.</li>
<li>Especifique detalhes da implementação no arquivo manifest. O exemplo a seguir mostra um arquivo manifest para um aplicativo Java™.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>Para obter mais informações sobre as opções suportadas que podem ser usadas nesse arquivo, consulte [Manifest do aplicativo](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Envie por push o seu aplicativo. É possível fazer upload de seu aplicativo
usando o comando cf push.
<ol>
<li>Conecte e efetue login no {{site.data.keyword.Bluemix_notm}}
executando o seguinte comando. Selecione sua organização e espaço
quando solicitado.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>No diretório do aplicativo, insira o comando cf push
com o nome do aplicativo. O nome do aplicativo deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.
<pre>cf push appname</pre></li>
<li>Opcional: se você usar um buildpack externo, deverá usar a opção -b com o comando cf push. Por exemplo:
<pre>cf push appname -b buildpack_URL</pre>
<p>Consulte
Usando buildpacks de comunidade para obter detalhes.</p>
</li></ol>
</li>

<li>Opcional: se você mudar seu aplicativo, deverá fazer upload dessas mudanças inserindo o comando cf push novamente. A
interface da linha de comandos cf usa as opções anteriores e as respostas
aos prompts, para atualizar todas as instâncias em execução de seu aplicativo
com os novos bits de código.</li>
</ol>

**Notas:**

* Ao usar o comando cf push, a interface de linha de comandos cf copia todos os arquivos e diretórios de seu diretório atual para o {{site.data.keyword.Bluemix_notm}}. Assegure-se
de que você tenha apenas os arquivos necessários em seu diretório de aplicativo.
* Assegure-se de que sua organização tenha memória suficiente para todas as instâncias
de seu aplicativo. Para visualizar a cota de memória de sua organização, use cf org org_name.
* Para obter mais informações sobre cf push, consulte [Comandos cf](../cli/reference/cfcommands/index.html).

##Migrando seus dados e usando serviços
{: #ht_service}

Depois
de fazer upload de seu aplicativo para o {{site.data.keyword.Bluemix_notm}},
selecione o serviço ao qual o aplicativo está conectado, no catálogo do {{site.data.keyword.Bluemix_notm}},
crie uma instância de serviço, vincule as instâncias ao seu aplicativo
e depois reinicie o aplicativo.

A variável de ambiente VCAP_SERVICES de seu aplicativo é um objeto JSON que contém informações sobre como interagir com uma instância de serviço no {{site.data.keyword.Bluemix_notm}}. As informações incluem o nome da instância de serviço, credenciais e
a URL de conexão com a instância de serviço.

Para executar o código no {{site.data.keyword.Bluemix_notm}},
deve-se incluir a lógica de código para analisar a variável VCAP_SERVICES,
a fim de obter informações sobre a conexão de serviços. Modifique seu aplicativo
para obter o host e a porta designados dinamicamente da instância de serviço
através das variáveis de ambiente. O exemplo a seguir mostra como
obter as credenciais de uma instância de serviço Postgre SQL em um aplicativo Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

Para assegurar que seu aplicativo possa ser executado em um ambiente local
depois de modificar o aplicativo para o {{site.data.keyword.Bluemix_notm}},
verifique a presença da variável de ambiente VCAP_SERVICES,
a qual está configurada para todos os aplicativos {{site.data.keyword.Bluemix_notm}} Cloud
Foundry.


# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Máquinas virtuais](../virtualmachines/vm_index.html)
* [Introdução ao Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Implementando apps com IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html)
* [O app de doze fatores](http://12factor.net/){:new_window}
* [Atingindo o backend corporativo com o Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
