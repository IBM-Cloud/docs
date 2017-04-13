---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Apps e tutoriais de amostra
{: #1stanchor}


As amostras a seguir demonstram como os aplicativos e o chaincode funcionam em uma rede de teste do IBM Blockchain. Para saber mais sobre o código do Hyperledger Fabric v0.6, que suporta redes do IBM Blockchain, visite [Documentos do Fabric](https://github.com/hyperledger/fabric/tree/v0.6/docs) do Hyperledger Project da Linux Foundation.  
{:shortdesc}

Para experimentar os aplicativos chaincode em ação, é possível implementar imediatamente a demo do Marbles, Commercial Paper ou Car Lease abaixo (clique em um botão Implementar no Bluemix). Ou continue lendo para explorar o tutorial Hello Chaincode.

- [![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## Aprender sobre o chaincode - Tutorial
{: #hellocc}
Esse tutorial conduz você por meio do uso de blocos de construção de configuração básica para codificar um aplicativo chaincode elementar. Você irá construir incrementalmente um chaincode de trabalho que criará recursos genéricos para trocar em uma rede. Em seguida, você irá interagir com o seu chaincode através da API de rede. Após concluir este tutorial, você será capaz de responder as perguntas a seguir:
- O que é chaincode?
- Como eu implemento o chaincode?
- Quais dependências existem?
- Quais são as funções principais?
- Como passo valores diferentes para os meus argumentos?
- Como inscrevo um usuário em minha rede com segurança?
- Como compilo o meu chaincode?
- Como interajo com o meu chaincode por meio da API REST?

### O que é chaincode?
Chaincode é código Go (Golang) ou Java que permite que os usuários interajam com uma rede de blockchain. Sempre que você 'chamar' uma transação na rede, estará chamando uma função em chaincode que lê e grava valores no livro razão.  

<br>
## Configurando o Ambiente de Desenvolvimento
Para iniciar o desenvolvimento do chaincode, primeiro instale as seguintes dependências e ferramentas recomendadas:

### Git

- [Página de download do Git](https://git-scm.com/downloads)
- [Manual do Pro Git](https://git-scm.com/book/en/v2)
- [Desktop do Git (uma alternativa para a CLI do Git)](https://desktop.github.com/)

Git é uma ferramenta de controle de versão rápida e poderosa para desenvolvimento do chaincode e para desenvolvimento de software em geral. Bash Git, que é instalado com o Git para Windows, é o terminal da linha de comandos recomendado.

Após concluir as instalações do Git, verifique se o Git está instalado:

```
$ git version
git version 2.9.0.windows.1
```

Depois de ter instalado o Git, crie uma conta para você mesmo em [GitHub](https://github.com/). O serviço IBM Blockchain on Bluemix requer que o chaincode esteja em um repositório do GitHub para implementação por meio da API REST.  

## Go

Go é atualmente o único idioma suportado para escrever o chaincode no Bluemix. A instalação do Go inclui um conjunto de ferramentas de CLI úteis para escrever o chaincode. Por exemplo, o comando `go build` permite compilar seu chaincode antes de tentar implementá-lo em uma rede. Instale o Go v1.6, que é a versão usada para desenvolver o Hyperledger Fabric v0.6:  

- [Instalação do Go 1.6](https://golang.org/dl/#go1.6.3)
- [Instruções de instalação do Go](https://golang.org/doc/install)
- [Documentação e tutoriais do Go](https://golang.org/doc/)

Verifique se o Go está corretamente instalado executando os seguintes comandos. A saída do comando `go version` pode variar, dependendo do seu sistema operacional:

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

A variável de ambiente `GOPATH` não precisa corresponder ao exemplo anterior, mas deve-se usar um diretório válido em seu sistema de arquivos. Quando você executa `go build` para verificar se o seu chaincode é compilado, o Go aparece no diretório `$GOPATH/src` para quaisquer dependências não padrão que você listar no bloco `import`
em seu chaincode. As [Instruções de instalação do Go](https://golang.org/doc/install) irão guiá-lo através da configuração da variável de ambiente GOPATH.  

<br>
## Hyperledger Fabric

Duas versões do Hyperledger Fabric são suportadas para o Blockchain on Bluemix: v0.5 e v0.6.  Conforme descrito abaixo, sua versão do chaincode deve se alinhar à versão do Hyperledger na rede do Bluemix.

Atenção:
1. Para ativar as funções de leitura e gravação no livro razão, o chaincode deve importar o shim do chaincode a partir do Hyperledger Fabric.
2. Para compilar seu chaincode localmente, deve-se ter o local do código do Hyperledger Fabric especificado na variável de ambiente `GOPATH`.

Para determinar qual versão do Hyperledger Fabric a instância do Bluemix está executando, clique na guia **Service Status** no Monitor do Painel.  Role para baixo para a seção **Notas sobre a Liberação**; o painel `Your network is using this version` exibirá o **Hyperledger Commit Level** que você está executando:

![Versão de backend do Bluemix](images/fabricversion.png "Bluemix backend version")
Figura 1. Versão do Hyperledger Fabric

A versão do seu chaincode deve se alinhar à versão do Hyperledger Fabric à qual você implementará seu chaincode. Por exemplo, a rede apresentada na Figura 1 requer a clonagem do código base do Hyperledger Fabric v0.6-preview. O código base da malha, para qualquer versão, deve ser armazenado no caminho `$GOPATH/hyperledger/fabric`:

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Para instalar o código base do Hyperledger Fabric v0.5, use o seguinte comando git clone:

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into
$GOPATH/src/github.com/hyperledger/fabric # Note that the v0.5
release is a branch of the repository.  It is defined below after the
-b argument git clone -b v0.5-developer-preview
https://github.com/hyperledger-archives/fabric.git
```

Para instalar o código base do Hyperledger Fabric v0.6, use o seguinte comando git clone:

```
# The v0.6 release exists as a branch inside the Gerrit fabric
repository git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

Se a malha não estiver corretamente instalada no `GOPATH`, construir seu chaincode retornará um erro semelhante ao exemplo a seguir:
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### Configure seu pipeline de desenvolvimento

Use as etapas a seguir para configurar um pipeline para escrever, construir e testar seu chaincode. Você escreverá o chaincode em sua máquina local, verificará se ele é compilado e fará upload dele para o GitHub. Você irá, então, implementar e testar seu chaincode em sua rede do Bluemix usando a API REST da malha:

1. Bifurque a versão apropriada do repositório [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) para sua versão de rede para sua conta do GitHub. Bifurque v1.0 para uma rede de malhas v0.5 ou bifurque v2.0 para uma rede de malhas v0.6. Uma opção é usar o botão **Fork**, localizado na parte superior direita da página do repositório. A bifurcação copia o repositório inteiro para sua máquina local, incluindo todas as ramificações, que são mostradas clicando no botão **Branch:** na parte superior esquerda da página. Para bifurcar usando a CLI, insira os seguintes comandos em seu shell bash do Git:

2. Clone sua bifurcação para o seu $GOPATH:

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  Agora você tem uma cópia de sua bifurcação em sua máquina local. Você escreverá o chaincode mudando ou incluindo arquivos locais, enviando-os por push para sua bifurcação no GitHub e, em seguida, implementando seu chaincode em sua rede blockchain usando a API REST em um peer de rede.

3. Duas versões do chaincode usadas neste tutorial são fornecidas: **start** é o chaincode de estrutura básica a partir do qual você iniciará e **finished* é o chaincode concluído que está pronto para construir. Primeiro, certifique-se de que **start** seja construído em seu ambiente local:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

A versão **start** de learn-chaincode deve ser compilada sem erros nem mensagens. Em caso negativo, revise as instruções anteriores para instalar o Go corretamente.

5. Grave as mudanças em seus arquivos de chaincode locais e envie por push os arquivos atualizados para sua bifurcação de GitHub:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # See what files have changed locally.  You should see chaincode_start.go
  git status
  # Stage all changes in the local repository for commit
  git add --all
  # Commit all staged changes.  Insert a short description after the -m argument
  git commit -m "Compiled my code"
  # Push local commits back to https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### Implemente a interface de chaincode
A próxima etapa é implementar a interface do shim do chaincode no código de Go. As três funções principais são **Init**, **Invoke** e **Query**. Todas as três funções levam um nome de função e uma matriz de sequências como entrada, mas são chamadas em pontos diferentes. O caminho de desenvolvimento termina com o chaincode de trabalho que cria ativos genéricos para troca em uma rede de blockchain.

### Dependências.
A instrução `import` lista as dependências para construir seu chaincode:
1. `fmt` - contém `Println` para depuração/criação de log.
2. `errors` - formato de erro padrão de Go.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - código que faz interface com o seu código do Golang com um peer de rede.

#### Init()
A função `Init` é chamada quando você implementa pela primeira vez seu chaincode. Como o nome implica, use esta função para inicializar seu chaincode. Neste exemplo, `Init` configura o estado inicial de um único par de chave/valor no livro razão.

Em seu arquivo `chaincode_start.go`, mude a função `Init` para que ele armazene o primeiro elemento `args` na chave "hello_world":

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

Isso é feito usando a função stub `stub.PutState`. Essa função interpreta o primeiro argumento enviado na solicitação de implementação como o valor a ser armazenado na chave 'hello_world'. Se um erro ocorre porque o número errado de argumentos foi transmitido ou porque algo deu errado ao gravar no livro razão, esta função retorna um erro. Caso contrário, ela é encerrada corretamente, não retornando nenhuma mensagem.  

#### Invoke()
Use a função `Invoke` para chamar as funções de chaincode para fazerem o "trabalho real" na rede de blockchain. As funções de chamada são capturadas como transações, que são agrupadas em blocos para gravação no livro razão. A atualização do livro razão é alcançada chamando seu chaincode. A estrutura de `Invoke` é simples; ela recebe uma função e uma matriz de argumentos. Com base na função transmitida pelo parâmetro da função na solicitação de chamada, `Invoke` chamará uma função auxiliar ou retornará um erro.

No arquivo `chaincode_start.go`, mude a função `Invoke` para chamar uma função de gravação genérica:

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

O código, agora, está procurando `write`, portanto, inclua a função de gravação em seu arquivo `chaincode_start.go`:

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

Essa função `write` deve ser semelhante à sua mudança `Init` anterior. Agora é possível configurar a chave e o valor para `PutState`, que permite armazenar qualquer par chave/valor no livro razão de blockchain.

#### Query()
A função `Query` é chamada para consultar o seu estado de chaincode e não inclui blocos na cadeia (livro razão). Apenas implemente e chame funções incluir novos blocos. Use `Query` para ler o valor de seus pares chave/valor do estado de seu chaincode.

Em seu arquivo `chaincode_start.go`, mude a função `Query` para que ele chame uma função de leitura genérica:

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

O código, agora, está procurando `read`, portanto, inclua a função 'ler' em seu arquivo `chaincode_start.go`:

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

Essa função `read` usa `GetState`, que é o complemento para `PutState`. Esta função shim toma apenas um argumento de sequência: o nome da chave a ser recuperada. Em seguida, essa função retorna o valor, como uma matriz de bytes, para `Query`, que por sua vez o envia para o manipulador REST.

#### Main()
A função `main` é executada quando cada peer implementa a sua instância do chaincode. Ela inicia o chaincode e o registra com o peer. Nenhuma atualização de código é necessária para 'principal'; ambos, chaincode_start.go e chaincode_finished.go, incluem uma função `main` na parte superior de cada arquivo:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interagindo com o seu chaincode
A maneira mais rápida de testar o seu chaincode é usar a interface REST em seus peers.
A UI do Swagger em seu monitor de painel do Bluemix permite que você experimente a implementação de chaincode, sem gravar nenhum código adicional.  

#### API do Swagger
Conclua as etapas a seguir para usar a API do Swagger:

1. Efetue login no [Bluemix](https://console.ng.bluemix.net/login) e assegure-se de estar na guia **Painel**.
1. Verifique se você está no mesmo "espaço" do Bluemix que contém o seu serviço do IBM Blockchain. A navegação de espaço é à esquerda.
1. Há um painel **Serviços** perto da parte inferior; clique em seu serviço do IBM Blockchain.
1. Você deverá ver uma mensagem "Bem-vindo ao IBM Blockchain..." ; clique no botão **LAUNCH** à direita.
1. Na página do monitor, você deverá ver duas tabelas; a tabela da parte inferior poderá estar vazia.
	- **Guia Rede:**
		- **Logs de peer** estão na tabela da parte superior. Na linha para **peer 1**, clique no ícone de arquivo para visualizar o log. Além dessa visualização estática, existem **logs de peer de fluxo** em tempo real na guia **Visualizar logs** perto da parte superior da página.
		- **Logs de ChainCode** estão na tabela da parte inferior. Cada chaincode é rotulado com o hash de chaincode que foi retornado quando ele foi implementado. Selecione o peer em qualquer linha de chaincode e, em seguida, clique no ícone de arquivo para visualizar o log.
	- **Guia APIs**: exibe a página de documentação da API do Swagger.
1. Continue com as etapas a seguir para implementar a inscrição segura. Chamadas para o terminal `/chaincode` na interface REST requerem um ID de contexto seguro. Para a maioria das chamadas REST serem aceitas, deve-se passar um *enrollID* registrado a partir da lista de credenciais de serviço:
  - Clique em **+ IDs de inscrição de rede** para expandir a lista de valores *enrollID* e os seus segredos.
  - Copie o conjunto de credenciais em um arquivo de texto para uso posterior.
  - Expanda a seção de API **Escrivão**.
  - Expanda a seção `POST /registrar`.
  - Preencha o campo `Value` com JSON que especifique um `enrollID` e `enrollSecret' a partir de suas credenciais:

  ![Exemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Exemplo de registro")

  O *Corpo de resposta* deve ser semelhante ao exemplo a seguir:

  ![Exemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Corpo de resposta de exemplo de registro")

Agora que você tem uma configuração de `enrollID`, é possível usar esse ID ao implementar, chamar e consultar o chaincode nas etapas a seguir.
### Implementando o seu chaincode
Para implementar o seu chaincode através da interface REST, o seu chaincode deve ser armazenado em um repositório GitHub público. Ao enviar uma solicitação de implementação para um peer, você especifica a URL para o repositório de chaincode e os parâmetros para inicializar o chaincode.

**Antes de implementar** o seu chaincode, verifique se ele é construído localmente:
1. Abra um prompt de comandos e navegue para o diretório que contém `chaincode_start.go`. Insira o seguinte comando:
	```
	go build ./
	```
1. Expanda a seção de API **Chaincode**.
1. Expanda a seção `POST /chaincode`.
1. Configure o campo de texto `DeploySpec` (faça os outros campos ficarem em branco) com o código de exemplo abaixo, especificando o seu caminho do repositório de chaincode e o `enrollID` a partir da etapa `/registrar` anterior. O `"path":` deve ser semelhante a: `"https://github.com/johndoe/learn-chaincode/finished"`. Esse é o caminho para a sua bifurcação de repositório, mais o caminho para o seu arquivo chaincode_finished.go:

	```
	{
		"jsonrpc": "2.0",
		"method": "deploy",
		"params": {
			"type": 1,
			"chaincodeID": {
				"path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
			"ctorMsg": {
				"function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  O *Corpo de resposta* deve ser semelhante ao exemplo a seguir:

  ![Exemplo de implementação](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Corpo de resposta de exemplo de implementação")

  A resposta para a implementação conterá o ID para esse chaincode. O ID é um hash alfanumérico de 128 caracteres, que pode ser usado para futuras solicitações de chamada ou consulta. Copie esse ID para o seu editor de texto.

#### Consulta
Consulte o seu chaincode para o valor da chave `hello_world`, que você configura com a função `Init`:
1. Expanda a seção de API **Chaincode**.
1. Expanda a seção `POST /chaincode`.
1. Preencha o campo de texto `QuerySpec` (faça os outros campos ficarem em branco) com o exemplo a seguir, especificando o ID do chaincode a partir da etapa de implementação anterior e o `enrollID` a partir da etapa anterior `/registrar`:

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
  O *Corpo de resposta" deve ser semelhante ao exemplo a seguir:

  ![Exemplo de consulta](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Corpo de resposta de exemplo de consulta")

  O valor de `hello_world` é "hi there", que foi configurado pelo corpo de sua chamada de implementação anterior.

#### Chamar
Chame a sua função de gravação genérica com `invoke`. Mude o valor de `hello_world` para "go away":
1. Expanda a seção de API **Chaincode**.
1. Expanda a seção `POST /chaincode`.
1. Preencha o campo de texto `InvokeSpec` (faça os outros campos ficarem em branco) com o exemplo a seguir, especificando o ID do chaincode a partir da etapa de implementação anterior e o `enrollID` a partir da etapa anterior `/registrar`:

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
  O *Corpo de resposta" deve ser semelhante ao exemplo a seguir:

  ![Exemplo de chamada](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Corpo de resposta de exemplo de chamada")

  Execute novamente a consulta acima e a resposta a seguir deverá ser obtida:

  ![Exemplo de Query2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Resposta de exemplo de chamada")

Você acabou de gravar algum chaincode de configuração básica.  

<br>
## Requisitos de demo
{: #requirements}

Os pré-requisitos a seguir, que estão incluídos com o serviço do Bluemix, são necessários para executar os aplicativos de demo Marbles, Commercial Paper e Car Lease. O seu ambiente do Bluemix clona o Hyperledger Fabric para fornecer essas dependências:

- ID do Bluemix https://console.ng.bluemix.net/ (necessário para criar a sua rede do IBM Blockchain e fornecer credenciais de serviço para peers e a Autoridade de certificação)
- Node.js 0.12.0+ e npm v2+
- Golang Environment (necessário apenas para construir o seu próprio chaincode)

A demos também requer proficiência com Node.js e o módulo expresso. Deve-se também ter um entendimento conceitual de 'chaincode', 'livro razão' e 'peer' em um contexto de blockchain; consulte o [Glossário do Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md).  

<br>
## Demo do Marbles
{: #marbles}

O aplicativo Marbles demonstra uma transferência de ativo simples entre duas partes. O aplicativo foi projetado para testar o SDK de JavaScript, guiar o seu desenvolvimento e ajudar os desenvolvedores a se familiarizarem com o SDK e o chaincode.

Explore os [Tutoriais do Marbles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) para saber como o aplicativo da web, o SDK e o chaincode funcionam juntos. Se você já estiver familiarizado com o chaincode e o IBM Blockchain, poderá [implementar manualmente](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) a demo no Bluemix ou clicar no botão Implementar no Bluemix para usar o aplicativo da web:  
[![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Demo de papel comercial
{: #commercialpaper}

O aplicativo Commercial Paper demonstra como uma rede de negócios de papel comercial pode ser implementada usando o IBM Blockchain. A demo do Commercial Paper explora uma rede de blockchain com permissão, na qual os participantes têm funções e níveis de acesso correspondentes designados. Visite o [LEIA-ME do Commercial Paper](https://github.com/IBM-Blockchain/cp-web#readme) para saber mais sobre os componentes dessa demo ou implemente-a no Bluemix imediatamente para ver a rede de negócios em ação:  
[![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Demo de lease de carro
{: #carlease}

O aplicativo Car Lease demonstra o ciclo de vida de um veículo, a partir da manufatura, através de uma série de proprietários e concluindo com o veículo sendo descartado. A demo usa Node.js para programação do lado do servidor e o Golang para executar o chaincode na rede do IBM Blockchain. A demo inclui duas instâncias de chaincode: uma define as regras para transações de veículo e a outra registra todas as transações de veículo durante o seu tempo de vida. Ambos os programas de chaincode usam objetos de JSON para armazenar dados. Visite o [LEIA-ME Car Lease](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) para saber mais sobre a arquitetura do aplicativo e os atributos de veículo associados a esta demo ou implemente-a imediatamente no Bluemix:  
[![Implementar no Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
