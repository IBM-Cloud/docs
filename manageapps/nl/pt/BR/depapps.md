---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Implementando apps
{: #deployingapps}

É possível implementar aplicativos no
{{site.data.keyword.Bluemix}}
usando vários métodos, como a interface da linha de comandos e ambientes de
desenvolvimento integrados (IDEs). É possível também usar manifests do aplicativo para
implementar aplicativos. Ao usar um manifest do aplicativo, reduza o número de detalhes de implementação que
você deve especificar sempre que implementar um aplicativo no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Implementação do aplicativo
{: #appdeploy}

Implementar um aplicativo para {{site.data.keyword.Bluemix_notm}} inclui duas fases, preparação e início do aplicativo.

O Cloud Foundry suporta o Diego, que é a nova arquitetura de tempo de execução padrão que fornece um conjunto de recursos que aprimoram a experiência de desenvolvimento de aplicativo para hospedar e construir plataformas de nuvem. Essa atualização de arquitetura fornece uma melhoria na operação e desempenho gerais da plataforma Cloud Foundry. A nova arquitetura fornece suporte para várias tecnologias do contêiner de aplicativo, incluindo Garden e Windows, um pacote SSH que permite login direto ao contêiner de aplicativo e outras mudanças inovadoras. Para obter mais informações sobre o upgrade da arquitetura recente, veja [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego está ativo ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}.


Todos os novos aplicativos criados serão executados no Diego e deve-se iniciar a migração dos aplicativos existentes executados nos DEAs para a nova arquitetura Diego.

**Nota**: a arquitetura Cloud Foundry Diego afeta todos os ambientes da região {{site.data.keyword.Bluemix_notm}} Public. Os ambientes do {{site.data.keyword.Bluemix_notm}} Dedicated e do {{site.data.keyword.Bluemix_notm}} Local serão atualizados em uma data posterior.

### Preparando um aplicativo
{: #diego}

Durante a fase de preparação, o Diego cuida de todos os aspectos relacionados à orquestração do contêiner de aplicativo. Quando você envia um app por push, o Cloud Controller envia uma solicitação de preparação para o Diego, que controla a tarefa de alocar as instâncias do app. O backend do Diego orquestra contêineres de aplicativo de uma maneira a assegurar tolerância a falhas e consistência de longo prazo, que equilibra a carga entre uma série de máquinas virtuais chamadas células. Além disso, o Diego assegura que os usuários possam acessar os logs de seus apps. Todos os componentes do Diego são projetados para armazenamento em cluster, o que significa que é possível criar diferentes zonas de disponibilidade.

Para validar o funcionamento do app, o Diego suporta as mesmas verificações baseadas em PORT que são usadas para o DEA. No entanto, o Diego também é projetado para poder ter opções mais genéricas, como verificações de funcionamento baseadas em URL, que poderão ser ativadas no futuro.

#### Montando um novo app
{: #stageapp}

Todos os novos apps são implementados na arquitetura Diego. Para montar um novo aplicativo, implemente-o com o comando **cf push**:

  1. Implemente o aplicativo:
  ```
  $ cf push APPLICATION_NAME
  ```

Para obter mais detalhes sobre o comando **cf push**, veja [cf push](/docs/cli/reference/cfcommands/index.html#cf_push).

### Migrando um app existente para o Diego
{: #migrateapp}

Diego é a arquitetura padrão do Cloud Foundry para o {{site.data.keyword.Bluemix_notm}} e o suporte para os DEAs será removido, portanto, deve-se migrar todos os aplicativos existentes atualizando cada app. Inicie a migração de seus apps para o Diego atualizando o aplicativo com a sinalização do Diego. O aplicativo tentará imediatamente iniciar a execução no Diego e parará a execução nos DEAs.

Como seu aplicativo é atualizado da arquitetura do DEA para o Diego, talvez você passe por um curto tempo de inatividade ou por um tempo de inatividade prolongado, se o aplicativo não for compatível com o Diego. Para limitar o tempo de atividade, execute uma [blue-green deploy](/docs/manageapps/updapps.html#blue_green) implementando uma cópia de seu aplicativo no Diego e, em seguida, alternando rotas e reduzindo a escala no aplicativo DEA.

Conclua as etapas a seguir para migrar seu app para o Diego:

 1.  Instale a [cf CLI ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} e o [CLI do Plug-in Diego-Enabler![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}.
 2. Revise a [lista de problemas conhecidos](depapps.html#knownissues).
 3. Configure a sinalização do Diego para mudar seu app para execução no Diego:
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

Depois de atualizar o app, verifique se ele foi iniciado. Se o app migrado falhar ao iniciar, ele permanecerá off-line até você identificar e resolver o problema e, em seguida, reiniciar o app.

A IBM alertará sobre o próximo período de migração obrigatória quando o suporte de arquitetura do DEA for removido e, se você não tiver migrado seus apps, a equipe de operações migrará todos para você.

Para validar em qual backend o aplicativo está em execução, use o comando a seguir:

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Problemas conhecidos de migração do Diego
{: #knownissues}

A seguir estão os problemas conhecidos que podem precisar ser tratados ao migrar seus apps para o Diego:

  * Os aplicativos trabalhadores implementados com a opção `--no-route` não são relatados como saudáveis. Para evitar isso, desative a verificação de funcionamento baseada em porta com o comando `cf set-health-check APP_NAME none`.
  * O comando **cf files** não é mais suportado. A substituição é o comando **cf ssh**. Para obter mais detalhes sobre o comando **cf ssh**, veja [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh).
  * Alguns apps podem usar um número alto de descritores de arquivos (inodes). Caso encontre esse problema, deve-se aumentar a cota do disco para seu app com o comando `cf scale APP_NAME [-k DISK]`.

Para obter a lista abrangente de problemas conhecidos, veja a página de documentação do Cloud Foundry para [Migrando para o Diego ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}.

Até que o suporte para a arquitetura mais antiga do DEA seja removido, será possível executar o comando a seguir para fazer a transição de volta para os DEAs: `cf disable-diego APPLICATION_NAME`. Ainda será possível implementar novos apps na arquitetura do DEA até que o suporte seja removido:

**Nota**: a [cf CLI ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} e o [CLI do Plug-in Diego-Enabler![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} devem estar ambos instalados para usar o comando `disable-diego`.

1. Implemente o aplicativo sem iniciá-lo:
```
$ cf push APPLICATION_NAME --no-start
```
2. Execute o comando disable-diego:
```
$ cf disable-diego APPLICATION_NAME
```
3. Inicie o aplicativo:
```
$ cf start APPLICATION_NAME
```

### Iniciando um aplicativo
{: #startapp}

Quando um aplicativo é iniciado, a instância ou instâncias do contêiner de aplicativo são criadas. Para aplicativos em execução no Diego, é possível usar o comando **cf ssh** ou **cf scp** para acessar o sistema de arquivos do contêiner de aplicativo que inclui os logs. O comando **cf files** não funciona para apps em execução na arquitetura do Diego.

**Nota**: se você ainda tiver aplicativos em execução nos DEAs, será possível usar o comando **cf files** para visualizar os arquivos dentro do contêiner de aplicativo até que o suporte para os DEAs seja removido.

Se o aplicativo falhar ao ser iniciado, ele será interrompido e todo o conteúdo do contêiner de aplicativo será removido. Portanto, se um
aplicativo parar ou se o processo de preparação de um aplicativo falhar, os arquivos de
log não estarão disponíveis para uso.

Se os logs do aplicativo não estiverem mais disponíveis de modo que os comandos **cf ssh**, **cf scp** ou **cf files** não possam mais ser usados para ver a causa dos erros de preparação dentro do contêiner de aplicativo, será possível usar o comando **cf logs** no lugar. O comando **cf logs** usa o agregador de log
do Cloud Foundry para coletar os detalhes dos logs do aplicativo e do sistema; também é
possível ver o que foi armazenado em buffer no agregador de log. Para obter mais informações sobre o agregador de log, veja [Efetuando login no Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Nota**: o tamanho do buffer é limitado. Se um aplicativo for executado por um longo tempo e não for reiniciado, os logs poderão não ser exibidos quando você inserir o comando `cf logs appname --recent`, porque o buffer do log poderá ter sido limpo. Portanto, para depurar erros de preparação de um aplicativo grande, será possível inserir o comando `cf logs appname` em uma linha de comandos separada da interface da linha de comandos cf para rastrear os logs quando você implementar o aplicativo.

Se
você tiver problemas ao preparar seus aplicativos no
{{site.data.keyword.Bluemix_notm}}, é possível
seguir as etapas em
[Depurando
erros de preparação](/docs/debug/index.html#debugging-staging-errors) para resolver o problema.


## Implementando aplicativos usando o comando cf
{: #dep_apps}

Ao implementar seus aplicativos no
{{site.data.keyword.Bluemix_notm}}
pela interface de linha de comandos, um buildpack deve ser fornecido como o ambiente de
tempo de execução, de acordo com o idioma e a estrutura de seu aplicativo. Também é possível usar o serviço Delivery Pipeline para implementar aplicativos no {{site.data.keyword.Bluemix_notm}}.

O {{site.data.keyword.Bluemix_notm}} fornece buildpacks integrados que suportam Java e Node.js. Se você estiver usando esses idiomas e estruturas, não precisará especificar o
buildpack quando implementar o aplicativo usando a interface de linha de comandos. Como o
{{site.data.keyword.Bluemix_notm}}
é construído no Cloud Foundry, o comando é padronizado com esses buildpacks.

Se você usar um buildpack externo, deve-se especificar a URL do buildpack
usando a opção **-b** quando implementar seu aplicativo no
{{site.data.keyword.Bluemix_notm}}
a partir do prompt de comandos.

  * Para implementar os pacotes do servidor Liberty no {{site.data.keyword.Bluemix_notm}}, use o comando a seguir a partir de seu diretório de origem:

  ```
  cf push
  ```

  Para obter mais informações sobre
o Liberty Buildpack, consulte
[Liberty
for Java](/docs/runtimes/liberty/index.html).

  * Para implementar aplicativos Java Tomcat no {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * Para implementar pacotes do WAR no
{{site.data.keyword.Bluemix_notm}}, use o
comando a seguir:

  ```
  cf push appname -p app.war
  ```
  Ou
você pode especificar um diretório que contenha os arquivos de aplicativos usando o
comando a seguir:

  ```
  cf push appname -p "./app"
  ```

  * Para implementar aplicativos Node.js no
{{site.data.keyword.Bluemix_notm}},
use o comando a seguir:

  ```
  cf push appname -p app_path
  ```

Um
arquivo `package.json` deve estar no aplicativo Node.js para que o
aplicativo seja reconhecido pelo buildpack do Node.js. O arquivo `app.js` é
o script de entrada para o aplicativo e pode ser especificado no arquivo `package.json`. O exemplo a seguir mostra um arquivo `package.json` simples:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  Para obter mais informações sobre o arquivo `package.json`, veja [package.json ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}.

  * Para implementar aplicativos PHP, Ruby ou Python no {{site.data.keyword.Bluemix_notm}},
use o comando a seguir a partir do diretório que contém sua origem de aplicativo:

  ```
  cf push appname
  ```

### Implementando um app em vários espaços

Um app é específico para o espaço em que é implementado. Não é possível mover ou copiar um app de um espaço para outro no {{site.data.keyword.Bluemix_notm}}. Para implementar um app em vários espaços, deve-se implementar o app em cada
espaço em que você deseja usar o app de acordo com as etapas a seguir:

  1. Alterne para o espaço em que deseja implementar seu app
usando o comando **cf target** com a opção **-s**:

  ```
  cf target -s <space_name>
  ```

  2. Acesse seu diretório de app e implemente seu app usando o comando **cf push**, em que appname deve ser exclusivo dentro de seu domínio.

  ```
  cf push appname
  ```

## Manifest do aplicativo
{: #appmanifest}

Os manifests do aplicativo contêm opções que são aplicadas ao comando
**cf push**. É possível usar um manifest do aplicativo para reduzir o
número de detalhes de implementação que deve-se especificar toda vez que enviar por push
um aplicativo para o {{site.data.keyword.Bluemix_notm}}.

Nos manifests do aplicativo, é possível especificar opções como o
número de instâncias do aplicativo a serem criadas, a quantia de cotas de memória e de
disco a ser alocada para os aplicativos e outras variáveis de ambiente do aplicativo. É
possível também usar manifests do aplicativo para automatizar implementações de
aplicativos. O nome padrão de um arquivo manifest é `manifest.yml`.

### Opções suportadas no arquivo manifest

A tabela a seguir mostra as opções suportadas que é possível usar em um arquivo
manifest do aplicativo. Se você optar por usar um nome de arquivo diferente de
`manifest.yml`, deve-se usar a opção **-f** com o comando
**cf push**. No exemplo a seguir, `appManifest.yml` é o
nome do arquivo:

```
cf push -f appManifest.yml
```

<p>  </p>


|Opções	|Descrição	|Uso ou exemplo|
|:----------|:--------------|:---------------|
|**buildpack**	|A URL ou o nome do buildpack customizado.	|`buildpack: ` *buildpack_URL*|
|**disk_quota**	|A cota do disco que é alocada para um aplicativo. O valor padrão é 1 G.	|`disk_quota: 500M`|
|**domínio**	|O nome de domínio do aplicativo no {{site.data.keyword.Bluemix_notm}}.	|`domain:` ng.bluemix.net|
|**host**	|O nome do host do aplicativo no {{site.data.keyword.Bluemix_notm}}. Esse valor deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.	|`host: ` *host_name*|
|**name**	|O nome do aplicativo no {{site.data.keyword.Bluemix_notm}}. Esse valor deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.	|`name: ` *appname*|
|**path**	|O local do aplicativo. Esse valor pode ser um caminho relativo ou um caminho absoluto.	|`path: ` *path_to_application*|
|**command**	|O comando inicial customizado para seu aplicativo ou o comando para executar arquivos de script.	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|A quantia de memória a ser alocada para o aplicativo. O valor padrão é 1G.	|`memory: 512M`|
|**instances**	|O número de instâncias a serem criadas para seu aplicativo.	|`instances: 2`|
|**timeout**	|O período máximo de tempo em segundos usado para iniciar o aplicativo. O valor padrão é 60 segundos.	|`timeout: 80`|
|**no-route**	|Um valor booleano para evitar que uma rota seja designada ao aplicativo se ele estiver sendo executado apenas em segundo plano. O valor padrão é **false**.	|`no-route: true`|
|**random-route**	|Um valor booleano para designar uma rota aleatória para o aplicativo. O valor padrão é **false**.	|`random-route: true`|
|**Serviços**	|Os serviços a serem ligados ao aplicativo.	|`services:   - mysql_maptest`|
|**env**	|As variáveis de ambiente customizadas do aplicativo.|`env: DEV_ENV: production`|
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### Um arquivo manifest.yml de amostra

O exemplo a seguir mostra um arquivo manifest para um aplicativo Node.js que usa
o buildpack do Node.js da comunidade integrada no
{{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## `Variáveis de ambiente
{: #app_env}

Variáveis de ambiente contêm as informações do ambiente de um aplicativo
implementado no {{site.data.keyword.Bluemix_notm}}. Além das variáveis de ambiente configuradas pelo *Droplet
Execution Agent (DEA)* e buildpacks, é possível também configurar variáveis de
ambiente específicas do aplicativo para aplicativos no {{site.data.keyword.Bluemix_notm}}.

É possível visualizar as variáveis de ambiente a seguir de um aplicativo
{{site.data.keyword.Bluemix_notm}} em execução
utilizando o comando **cf env** ou a partir da interface com o usuário do
{{site.data.keyword.Bluemix_notm}}:

  * Variáveis definidas pelo usuário que são específicas de um aplicativo. Para obter informações sobre como incluir uma variável definida pelo usuário em um app, veja [Incluindo variáveis de ambiente definidas pelo usuário ![Ícone de link externo](../icons/launch-glyph.svg)](#ud_env){:new_window}.

  * A variável VCAP_SERVICES, que contém informações de conexão para acessar uma instância de serviço. Se o aplicativo estiver ligado a vários serviços, a variável VCAP_SERVICES incluirá as informações de conexão de cada instância de serviço. Por
exemplo:

  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

Também é possível acessar as variáveis de ambiente configuradas pelo DEA e por buildpacks.

As variáveis a seguir são definidas pelo DEA:

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>O diretório-raiz do aplicativo implementado.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>A quantidade máxima de memória que cada instância de seu aplicativo pode usar. É
possível especificar o valor em um arquivo <span class="ph filepath">manifest.yml</span> do
aplicativo ou na linha de comandos quando você envia por push o aplicativo.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>A porta no DEA para comunicação com o aplicativo. O DEA aloca uma porta para o
aplicativo no tempo de preparação.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>O diretório atualmente em funcionamento no qual o buildpack está em execução.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>O diretório no qual arquivos provisórios e de preparação são armazenados.</dd>
  <dt><strong>USER</strong></dt>
  <dd>O ID do usuário sob o qual o DEA é executado.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>O endereço IP do host DEA.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>Uma sequência JSON que contém informações sobre o aplicativo implementado. As
informações incluem nome do aplicativo, URIs, limites de memória, registro de data e hora
em que o aplicativo atingiu seu estado atual e assim por diante. Por exemplo:
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>Uma cadeia JSON que contém informações do serviço que está ligado ao aplicativo implementado. Por exemplo:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

As variáveis que são definidas por buildpacks são diferentes para cada buildpack. Veja [Buildpacks ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} para obter quaisquer outros buildpacks compatíveis.

<ul>
    <li>As variáveis a seguir são definidas pelo Buildpack do Liberty:

	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>O local de Java SDK que executa o aplicativo.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>As opções de Java SDK a serem usadas ao executar o aplicativo.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>O comando Java para inicializar uma instância de servidor do perfil Liberty no DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>O local de recursos compartilhados e definições do servidor ao inicializar uma
instância de servidor de perfil do Liberty no DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>O local da saída gerada, como arquivos de log e diretório ativo de uma instância de
servidor de perfil do Liberty em execução.</dd>
	  </dl>
</li>
<li>As variáveis a seguir são definidas pelo Buildpack do Node.js:
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>O diretório do ambiente de tempo de execução do Node.js.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>O diretório que o ambiente de tempo de execução do Node.js usa para armazenamento em cache.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>O caminho do sistema que é usado pelo ambiente de tempo de execução Node.js.</dd>
	</dl>
</li>
</li>
</ul>

É possível usar o código de amostra do Node.js a seguir para obter o valor da variável de ambiente VCAP_SERVICES:

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

Para obter mais informações sobre cada variável de ambiente, veja [Variáveis de ambiente do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Customizando implementações de aplicativos
{: #customize_dep}

É possível customizar as tarefas de implementação para seus aplicativos. Por
exemplo, é possível especificar os comandos iniciais de seus aplicativos e configurar o
ambiente de inicialização de seu aplicativo.
{:shortdesc}

### Especificando comandos iniciais

Para especificar os comandos iniciais de seu aplicativo, é possível usar uma
das maneiras a seguir. Os comandos iniciais que você especificar sobrescreverão os
comandos iniciais padrão que o buildpack fornece.

**Nota:** para que os comandos iniciais do buildpack tenham precedência, especifique **null** como o comando inicial.

  * Use o comando **cf push** e especifique o parâmetro -c. Por exemplo, ao implementar um aplicativo Node.js, é possível especificar o comando inicial **node app.js** no parâmetro -c:

  ```
  cf push appname -p app_path -c "node app.js"
  ```

  * Use o parâmetro de comando no arquivo `manifest.yml`. Por exemplo, ao implementar um aplicativo Node.js, é possível especificar o
comando inicial **node app.js** no arquivo manifest:

  ```
  command: node app.js
  ```


### Incluindo variáveis de ambiente definidas pelo usuário
{: #ud_env}

As variáveis de ambiente definidas pelo usuário são específicas de um aplicativo. Você tem as opções a seguir para incluir uma variável de ambiente definida pelo usuário em um app em execução:

  * Use a interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Conclua
as etapas a seguir:
    1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique no ladrilho do app. A página de detalhes do app é exibida.
	2. Clique em **Variáveis de ambiente**.
	3. Clique em **DEFINIDA PELO USUÁRIO** e, em seguida, clique em **INCLUIR**.
	4. Preencha os campos necessários e, em seguida, clique em **SALVAR**.
  * Use a interface de linha de comandos cf. Inclua uma variável definida pelo usuário usando o comando `cf set-env`. Por
exemplo:
    ```
    cf set-env appname env_var_name env_var_value
    ```

  * Use o arquivo `manifest.yml`. Inclua pares de valores no arquivo. Por
exemplo:
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```

Após incluir uma variável de ambiente definida pelo usuário, será possível usar o código de amostra do Node.js a seguir para obter o valor da variável definida:

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```

### Configurando o ambiente de inicialização

Para configurar o ambiente de inicialização de seu aplicativo, é possível
incluir shell scripts no diretório `/.profile.d`. O diretório
`/.profile.d` está sob o diretório de construção de seu aplicativo. Os
scripts no diretório `/.profile.d` são executados pelo
{{site.data.keyword.Bluemix_notm}} antes da
execução do aplicativo. Por exemplo, é possível configurar a variável de ambiente NODE_ENV como **production** colocando um arquivo `node_env.sh` que contém o conteúdo a seguir no diretório `/.profile.d`:

```
export NODE_ENV=production;
```

###Evitando o upload de arquivos e diretórios

Ao usar a interface de linha de comandos cf para implementar um
aplicativo, é possível economizar tempo de upload ignorando determinados arquivos e
diretórios que o {{site.data.keyword.Bluemix_notm}} pode
obter em outro lugar. Para evitar que esses arquivos e diretórios sejam transferidos por upload para o {{site.data.keyword.Bluemix_notm}},
é possível criar um arquivo `.cfignore` no diretório-raiz de seu aplicativo.

**Nota:** o arquivo `.cfignore` deve estar no formato UTF-8.

O arquivo `.cfignore`
contém os nomes de arquivos e diretórios que você deseja ignorar,
um nome por linha. É possível usar um asterisco (*) como um caractere curinga. Ao especificar um diretório, todos os arquivos e subdiretórios sob esse
diretório também são ignorados. Por exemplo, o conteúdo a seguir
no arquivo `.cfignore` indica que todos os arquivos `.swp`
e todos os arquivos e subdiretórios sob o diretório `tmp/`
não serão transferidos por upload para o {{site.data.keyword.Bluemix_notm}}.

```
*.swp
tmp/
```

# Links Relacionados
{: #rellinks notoc}

## Links Relacionados
{: #general}

* [Implementando com Manifests do aplicativo ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [Gerador de manifest do CF ![Ícone de link externo](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Introdução ao cf v6 ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Introdução ao IBM Continuous Delivery Pipeline for Bluemix](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
