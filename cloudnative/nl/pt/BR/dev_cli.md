---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

O {{site.data.keyword.dev_cli_long}} fornece uma abordagem extensível orientada por comandos para criar, desenvolver e implementar um projeto da web com o plug-in `dev`. Ideal para desenvolvedores que gostariam de usar o controle da linha de comandos ao desenvolver aplicativos de microsserviço de ponta a ponta.

{: shortdesc}

A {{site.data.keyword.dev_cli_notm}} usa dois contêineres para facilitar a construção e o teste do aplicativo. O primeiro é o contêiner de ferramentas que contém os utilitários necessários para construir e testar o aplicativo. O Dockerfile para esse contêiner é definido pelo parâmetro [dockerfile-tools](#command-parameters). Talvez você o considere um contêiner de desenvolvimento, pois contém as ferramentas normalmente úteis para o desenvolvimento de um tempo de execução específico.

O segundo contêiner é o contêiner de execução. Esse contêiner tem um formato adequado para ser implementado para uso, por exemplo, no {{site.data.keyword.Bluemix}}. Como resultado, esse contêiner geralmente terá um ponto de entrada definido que inicia o aplicativo. Quando você selecionar para executar o aplicativo por meio da {{site.data.keyword.dev_cli_short}}, ele usará esse contêiner. O Dockerfile para esse contêiner é definido pelo parâmetro [dockerfile-run](#run-parameters).


## Incluindo a {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### Pré-requisitos
{: #prereq}

São necessários alguns pré-requisitos para explorar totalmente e usar corretamente a {{site.data.keyword.dev_cli_short}}, uma vez que é altamente extensível e permite aproveitar tecnologias complementares adicionais.

1. Instale o [Cloud Foundry CLI ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#getting-started).

2. Instale o [{{site.data.keyword.Bluemix}} CLI ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://clis.ng.bluemix.net/ui/home.html).

3. Obtenha um ID do [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net).

4. Opcional: se planeja executar e depurar aplicativos localmente, deve-se também instalar o [Docker ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.docker.com/get-docker). Isso é necessário apenas para projetos não móveis.


### Installing
{: #installation}

1. Instale a [{{site.data.keyword.dev_cli_short}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window} executando o comando a seguir:
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	Valide a instalação bem-sucedida executando o comando a seguir:  
 
	```
	bx dev
	```
	{: codeblock}
	

### Antes de Come╬ar
{: #before-install}
	
1. Efetue login no {{site.data.keyword.Bluemix_notm}}.

	```
	bx login
	```
	{: codeblock}
	
	**Nota:** se as suas credenciais forem rejeitadas, é possível que você esteja usando um ID federado. Siga estas etapas para se autenticar usando um ID federado:
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. Efetue login no [{{site.data.keyword.iamshort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.bluemix.net/iam/#/apikeys){: new_window}.
	2. Selecione **Criar chave API**.
		* Insira um nome e uma descrição da apiKey
	3. Faça download da apiKey.
	4. Abra o arquivo e copie o valor do campo `apiKey`.
	5. Efetue login usando o seguinte comando:
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## Comandos
{: #commands}

Use os comandos a seguir para criar, implementar, depurar e testar um projeto.

### Compilação
{: #build}

É possível construir o aplicativo usando o comando `build`. O elemento de configuração `build-cmd-run` é usado para construir o aplicativo. Os comandos `test`, `debug` e `run` executam uma construção da mesma maneira que esse comando como parte de sua operação normal e, assim, executar esse comando antes deles não é necessário.

Execute o comando a seguir no diretório de projeto atual para construir seu aplicativo:  

```
bx dev build
```
{: codeblock}


[Parâmetros do comando de construção](#command-parameters)


### Código
{: #code}

O comando `code` permite fazer download do código do aplicativo após a implementação para que você possa revisar localmente ou fazer mudanças adicionais.

Execute o comando a seguir para fazer download do código de um projeto especificado.

```
bx dev code <projectName>
```
{: codeblock}


### criar
{: #create}

Crie um novo projeto, solicitando todas as informações necessárias, incluindo a linguagem, o nome do projeto e o tipo padrão de app. O projeto será criado no diretório atual. 

Para criar um novo projeto no diretório de projeto atual e associar serviços a ele, execute o comando a seguir:

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

É possível depurar o aplicativo por meio do comando `debug`. Uma construção é concluída primeiramente no projeto usando o elemento de configuração `build-cmd-debug` como a instrução de construção. Um contêiner é então iniciado expondo uma porta ou portas de depuração, conforme definido no `container-port-map-debug`. Conecte sua ferramenta de depuração favorita à porta ou portas e será possível depurar seu aplicativo normalmente.

**Limitação**: atualmente, os projetos Swift não estão disponíveis para depuração.

Execute o comando a seguir no diretório de projeto atual para depurar seu aplicativo:

```
bx dev debug
```
{: codeblock}	

Para sair da sessão de depuração, use `CTRL-C`.


#### Parâmetros do comando de depuração
{: #debug-parameters}

Os parâmetros a seguir são exclusivos para o comando `debug` e
ajudam na depuração de um aplicativo.

##### `container-port-map-debug`
{: #port-map-debug}

* Mapeamentos de porta para a porta de depuração. O primeiro valor é a porta a ser usada no OS do host, a segunda é a porta no contêiner (host:container).
* Uso: `bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* Usado para construir código para DEBUG.
* Uso: `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* Usado para depurar código no contêiner de ferramentas. Isso será opcional se o `build-cmd-debug` for iniciar seu aplicativo na depuração.
* Uso: `bx dev debug debug-cmd /the/debug/command`

#### Depuração de aplicativo local:
{: #local-app-dev}

Para obter mais informações sobre a depuração de aplicativo local, veja [Depuração de aplicativo local](docs/cloudnative/dev_cli_local_debug.html#local-debug).


### Apagar
{: #delete}

Esse comando permite remover projetos do espaço do {{site.data.keyword.Bluemix}}.

Execute o comando a seguir para excluir seu projeto do {{site.data.keyword.Bluemix}}:

```
bx dev delete <projectName>
```
{: codeblock}
 

**Nota** os serviços do {{site.data.keyword.Bluemix}} **não** são removidos.


### Help
{: #help}

Por padrão, se nenhuma ação ou argumento for passado ou se a ação 'ajuda' for fornecida, esse comando mostrará um texto "Ajuda" geral. A ajuda geral exibida inclui uma descrição dos argumentos de base, bem como uma listagem das ações disponíveis.  

Execute o comando a seguir para exibir informações da ajuda Geral:

```
bx dev help
```
{: codeblock}


### Listar
{: #list}

É possível listar todos os projetos do {{site.data.keyword.Bluemix_notm}} em um espaço.

Execute o comando a seguir para listar seus projetos:

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Run
{: #run}

É possível executar seu aplicativo por meio do comando `run`. Uma construção é concluída primeiramente no projeto usando o elemento de configuração `build-cmd-run` como a instrução de construção. O contêiner de execução é então iniciado e expõe as portas, conforme definido no `container-port-map`. O `run-cmd` poderá ser usado para chamar o aplicativo se o contêiner de execução não contiver um ponto de entrada para concluir essa etapa. 

Execute o comando a seguir no diretório de projeto atual para iniciar seu aplicativo:

```
bx dev run
```
{: codeblock}

Para sair da sessão, use `CTRL-C`.


#### Parâmetros de Execução
{: #run-parameters}

Os parâmetros a seguir são exclusivos para o comando `run` e
ajudam no gerenciamento do aplicativo dentro do contêiner de execução.

##### `container-name-run`
{: #container-name-run}
	
* Nome do contêiner para o contêiner de execução.
* Uso: `bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* Local no contêiner para compartilhar na execução.
* Uso: `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* Local no sistema host para compartilhar no contêiner na execução.
* Uso: `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* Arquivo Docker para o contêiner de execução.
* Uso: `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* Imagem a ser criada do dockerfile-run.
* Uso: `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* Parâmetro opcional usado para executar código no contêiner de execução. Isso será opcional se a imagem for iniciar seu aplicativo.
* Uso: `bx dev run run-cmd [/the/run/command]`
	
### Status do
{: #status}

É possível consultar o status dos contêineres usados pela {{site.data.keyword.dev_cli_short}}, conforme definido por `container-name-run` e `container-name-tools`. 

Execute o comando a seguir no diretório de projeto atual para verificar o status do contêiner:

```
bx dev status
```
{: codeblock}


[Parâmetros do comando de status](#command-parameters)


### Stop
{: #stop}

É possível parar um contêiner por meio do comando `stop`. O parâmetro `container-name` permite especificar o contêiner a ser parado. Se isso não for especificado, o comando stop parará o contêiner de execução, conforme definido por `container-name-run`. 

Execute o comando a seguir no diretório de projeto atual para parar um contêiner:

```
bx dev stop
```
{: codeblock}


#### Parâmetro de parada adicional: 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* O nome do contêiner para o contêiner de ferramentas.
* Uso: `bx dev stop container-name <demo-tools>` 

### Testar (Test)
{: #test}

É possível testar o aplicativo por meio do comando `test`. Uma construção é concluída primeiramente no projeto usando o elemento de configuração `build-cmd-run` como a instrução de construção. O contêiner de ferramentas é então usado para chamar o `test-cmd` para o aplicativo.

Execute o comando a seguir para testar seu aplicativo: 

```
bx dev test
```
{: codeblock}


[Parâmetros do comando de teste](#command-parameters)


## Parâmetros para construir, depurar, executar e testar
{: #command-parameters}

Os parâmetros a seguir podem ser usados junto aos comandos `build|debug|run|test` e podem ser especificados por meio da linha de comandos e/ou atualizando o arquivo `cli-config.yml` do projeto diretamente. Há parâmetros adicionais disponíveis para os comandos [`debug`](#debug-parameters) e [`run`](#run-parameters) e estão documentados em suas respectivas seções.

**Nota**: os parâmetros de comando inseridos na linha de comandos têm precedência sobre a configuração de `cli-config.yml`.

##### `container-name-tools`  
{: #container-name-tools}

* O nome do contêiner para o contêiner de ferramentas.
* Uso: `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* Local no host a ser compartilhado para construção, depuração, teste.
* Uso: `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* Local no contêiner a ser compartilhado para construção, depuração, teste.
* Uso: `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* Mapeamentos de porta para o contêiner. O primeiro valor é a porta a ser usada no OS do host, a segunda é a porta no contêiner (host:container).
* Uso: `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* Arquivo Docker para o contêiner de ferramentas.
* Uso: `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* Imagem a ser criada do dockerfile-tools.
* Uso: `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* Comando para construir código para todos os usos, exceto DEBUG.
* Uso: `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* Comando para testar código no contêiner de ferramentas.
* Uso: `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

