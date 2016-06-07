---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Implementando apps
{: #deployingapps}

*Última atualização: 9 de maio de 2016*

É possível implementar aplicativos no
{{site.data.keyword.Bluemix}}
usando vários métodos, como a interface da linha de comandos e ambientes de
desenvolvimento integrados (IDEs). É possível também usar manifests do aplicativo para
implementar aplicativos. Ao usar um manifest do aplicativo, reduza o número de detalhes de implementação que
você deve especificar sempre que implementar um aplicativo no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

##Implementação do aplicativo
{: #appdeploy}

Implementar um aplicativo para {{site.data.keyword.Bluemix_notm}} inclui duas fases, preparação e início do aplicativo.

###Preparando um aplicativo

Durante a fase de preparação, um
Droplet Execution Agent (DEA) usa as informações que você fornece na interface de linha
de comandos cf ou o arquivo `manifest.yml` para
decidir o que criar para preparação do aplicativo. O DEA seleciona um buildpack
apropriado para preparar o aplicativo e o resultado do processo de preparação é um droplet. Para obter mais informações sobre a implementação de um aplicativo no {{site.data.keyword.Bluemix_notm}}, consulte Arquitetura do [{{site.data.keyword.Bluemix_notm}}, Como o {{site.data.keyword.Bluemix_notm}} funciona](../public/index.html#publicarch).

Durante
o processo de preparação, o DEA verifica se o buildpack corresponde ao aplicativo. Por
exemplo, um tempo de execução do Liberty para um arquivo .war, ou um tempo de execução do
Node.js para arquivos .js. O DEA então cria um contêiner isolado que contém o buildpack e
o código do aplicativo. O contêiner é gerenciado pelo componente Warden. Para
obter mais informações, consulte
[Como
os aplicativos são preparados](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}.

###Iniciando um aplicativo

Quando um aplicativo é iniciado, a
instância ou as instâncias do contêiner warden são criadas. É possível usar o comando
**cf files** para ver os arquivos que estão armazenados no sistema de
arquivos do contêiner Warden, como os logs. Se o aplicativo falha ao ser iniciado, o DEA
para o aplicativo e o conteúdo inteiro do contêiner Warden é removido. Portanto, se um
aplicativo parar ou se o processo de preparação de um aplicativo falhar, os arquivos de
log não estarão disponíveis para uso.

Se os logs do aplicativo não estiverem mais
disponíveis de modo que o comando **cf files** não pode mais ser usado
para ver a causa dos erros de preparação, será possível usar o comando **cf
logs** em seu lugar. O comando **cf logs** usa o agregador de log
do Cloud Foundry para coletar os detalhes dos logs do aplicativo e do sistema; também é
possível ver o que foi armazenado em buffer no agregador de log. Para obter mais informações sobre o agregador de log, consulte
[Efetuando
login no Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Nota**: o tamanho do buffer é limitado. Se um aplicativo for executado por um longo período e não for reiniciado, os logs poderão não ser exibidos quando você inserir `cf logs appname --recent` porque o buffer do log pode ter sido limpo. Portanto, para depurar erros de preparação para um aplicativo grande, é possível inserir `cf logs appname` em uma linha de comandos separada da interface de linha de comandos cf para rastrear os logs quando você implementar o aplicativo.

Se
você tiver problemas ao preparar seus aplicativos no
{{site.data.keyword.Bluemix_notm}}, é possível
seguir as etapas em
[Depurando
erros de preparação](../debug/index.html#debugging-staging-errors) para resolver o problema.

##Implementando aplicativos usando o comando cf
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
for Java](../runtimes/liberty/index.html).
  
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
    
  Para obter mais informações sobre o arquivo `package.json`, consulte
[package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}.
  
  * Para implementar aplicativos PHP, Ruby ou Python no {{site.data.keyword.Bluemix_notm}},
use o comando a seguir a partir do diretório que contém sua origem de aplicativo:
  
  ```
  cf push appname
  ```

###Implementando um app em vários espaços

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
  
##Manifest do aplicativo
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

###Opções suportadas no arquivo manifest

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
*Tabela 1. Opções suportadas no arquivo manifest.yml*

###Um arquivo `manifest.yml` de amostra

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

##`Variáveis de ambiente
{: #app_env}

Variáveis de ambiente contêm as informações do ambiente de um aplicativo
implementado no {{site.data.keyword.Bluemix_notm}}. Além das variáveis de ambiente configuradas pelo *Droplet
Execution Agent (DEA)* e buildpacks, é possível também configurar variáveis de
ambiente específicas do aplicativo para aplicativos no {{site.data.keyword.Bluemix_notm}}.

É possível visualizar as variáveis de ambiente a seguir de um aplicativo
{{site.data.keyword.Bluemix_notm}} em execução
utilizando o comando **cf env** ou a partir da interface com o usuário do
{{site.data.keyword.Bluemix_notm}}:
	
  * Variáveis definidas pelo usuário que são específicas de um aplicativo. Para obter informações sobre como incluir uma variável definida pelo usuário em um app, veja [Incluindo variáveis de ambiente definidas pelo usuário](#ud_env){:new_window}.
	 
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
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
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

As variáveis que são definidas por buildpacks são diferentes para cada buildpack. Consulte
[Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}
para obter qualquer outro buildpack compatível.

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

Para obter mais informações sobre cada variável de ambiente, consulte
[Variáveis
de ambiente do Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

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
	2. Na área de janela de navegação à esquerda, clique em **Variáveis de ambiente**.
	3. Clique em **DEFINIDA PELO USUÁRIO** e, em seguida, clique em **INCLUIR**.
	4. Preencha os campos necessários e, em seguida, clique em **SALVAR**.
  * Use a interface de linha de comandos cf. Inclua uma variável definida pelo usuário usando o comando `cf set-env`. Por exemplo: 
    ```
    cf set-env appname env_var_name env_var_value
    ```
	
  * Use o arquivo `manifest.yml`. Inclua pares de valores no arquivo. Por exemplo: 
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
{: #rellinks}

## Links Relacionados
{: #general}

* [Implementando com manifests do aplicativo](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [Gerador de manifest CF](http://cfmanigen.mybluemix.net/){:new_window}
* [Introdução ao cf v6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Introdução ao IBM Continuous Delivery Pipeline for Bluemix](../services/DeliveryPipeline/index.html#getstartwithCD)
