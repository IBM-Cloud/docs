---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Apps e tutoriais de amostra
{: #1stanchor}
Última atualização: 5 de outubro de 2016
{: .last-updated}

As amostras a seguir demonstram como os aplicativos e o chaincode funcionam em uma rede do IBM Blockchain. Para saber mais sobre o código do Hyperledger Fabric
v0.5, que suporta a sua rede de blockchain, visite a seção
[Docs do Fabric](https://github.com/hyperledger/fabric/tree/master/docs) do Hyperledger Project do Linux Foundation.  
{:shortdesc}

Para experimentar os aplicativos chaincode em ação, é possível implementar imediatamente a demo do Marbles, Commercial Paper ou Car Lease abaixo (clique em um botão Implementar no Bluemix). Ou continue lendo para explorar o tutorial Hello Chaincode.

- [![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  **Marbles**
- [![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  **Commercial Paper**
- [![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)] **Car Lease**  

<br>
## Usando o tutorial Hello Chaincode
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
Chaincode é código Go (GoLang) ou Java que permite aos usuários interagirem com uma rede de blockchain. Sempre que você 'chamar' uma transação na rede, estará chamando uma função em chaincode que lê e grava valores no livro razão.

### Implementando o seu primeiro chaincode
Conclua os tópicos a seguir para implementar chaincode em uma rede do IBM Blockchain on Bluemix:
#### Configurando o ambiente
1. Faça download e instale o Golang para o seu sistema operacional a partir de: [GoLang](https://golang.org/dl/).
2. Configure o seu GOPATH:
	- $GOPATH é um caminho de **Variável de ambiente** para o seu código e projetos do Go. O seu $GOPATH deve ser configurado para obter, construir e instalar pacotes fora da árvore de Go padrão. Portanto, $GOPATH deve ser exclusivo a partir do caminho $GOROOT no qual a árvore de Go original reside. Simplesmente crie um diretório e, em seguida, aponte para o seu $GOPATH lá.
	- Configure o seu $GOPATH no Windows:
		- Crie um diretório da área de trabalho para o seu projeto, como C:\Users\ADMIN\Documents\GoProjects.
		- Clique em seu menu **Iniciar** do Windows e procure "variáveis de ambiente do sistema."
		- Clique em **Editar as variáveis de ambiente do sistema**.
		- A partir da guia **Avançada**, clique em **Variáveis de ambiente**.
		- Localize as suas variáveis de ambiente do sistema GOPATH e GOROOT. Se você precisar criar GOPATH, clique em **Novo**.  
		- Os seus valores GOROOT e GOPATH devem ser exclusivos. GOROOT é gerado automaticamente quando você instala Go e deve ser C:\Go\.
		- Configure o seu GOPATH para o diretório da área de trabalho que você criou. Nesse exemplo, **GOPATH** é **C:\Users\ADMIN\Documents\GoProjects**.  
		- Para obter mais detalhes, execute o comando `go help gopath` ou visite a [Documentação do Go](https://golang.org/doc/install).
3. Inclua o código shim do Hyperledger Fabric v0.5 em seu caminho Go executando o comando a seguir:

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **Nota**: certifique-se de seguir o link acima para importar o código shim de archives do hyperledger v0.5. O backend do Bluemix é
construído com essa mesma versão; como resultado, é importante para a versão shim e versão do Bluemix se alinharem.

#### Configurando o GitHub
Os planos do Blockchain on Bluemix requerem que o seu chaincode esteja localizado em um repositório [GitHub](https://Github.com/). Crie uma conta do GitHub e configure Git conforme descrito em [Configurar Git](https://help.github.com/articles/set-up-git/). Após configurar GitHub, conclua as etapas a seguir:
1. Acesse [aprender chaincode](https://github.com/IBM-Blockchain/learn-chaincode) e bifurque o repositório.  
2. Clone a bifurcação para o diretório especificado em seu $GOPATH.  
3. O repositório inclui dois diretórios de chaincode: [Início](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) é o chaincode a partir do qual você começará a construir. [Concluído](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) é o chaincode que você irá, enfim, construir.
4. Assegure-se de que o chaincode seja construído em seu ambiente local. Abra um prompt de comandos e navegue para a pasta que contém `chaincode_start.go`. Insira o seguinte comando:

	```
	go build ./
	```
O comando deve retornar sem erros ou mensagens.

#### Implementando a interface de chaincode
A próxima etapa é implementar a interface shim de chaincode em seu código de Golang. As três funções principais são **Init**, **Chamar** e **Consultar**. Todas as três funções tomam um nome da função e uma matriz de sequências como entrada, mas variam quanto ao momento em que elas são chamadas. Você estará construindo para um chaincode de trabalho que criará recursos genéricos para troca em uma rede de blockchain.

### Dependências.
A instrução `import` lista dependências que são necessárias para construir o seu chaincode:
1. `fmt` - contém `Println` para depuração/criação de log.
2. `errors` - formato de erro padrão de Go.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - código que faz interface com o seu código do Golang com um peer de rede.

### Passando Valores

Os valores a seguir são passados:
#### Init()
Init é chamado para inicializar o seu chaincode quando você, primeiramente, o implementa na rede. Neste exemplo, você usa `Init` para configurar o estado inicial de uma variável no livro razão.

Em seu arquivo `chaincode_start.go`, mude a função `Init` para que ele armazene o primeiro elemento `args` na chave "hello_world":

```go
func (t *SimpleChaincode) Init(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
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

Isso é feito usando o execute a função shim `stub.PutState`. O primeiro argumento é a chave como uma sequência e o segundo argumento é o valor como uma matriz de bytes. 
Essa função pode retornar um erro, que o seu código inspeciona e retorna, se presente.

#### Invoke()
`Invoke` é chamado para incluir uma solicitação de transação para a cadeia. A estrutura de `Invoke` é simples;
ela recebe um argumento `function` e, com base nesse argumento, chama funções Go no chaincode.

Em seu arquivo `chaincode_start.go`, mude a função `Invoke` para que ele chame uma função de gravação genérica.

```go
func (t *SimpleChaincode) Invoke(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
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

O código está agora procurando `write`, portanto, inclua essa função em seu arquivo `chaincode_start.go`:

```go
func (t *SimpleChaincode) write(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
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
`Query` é chamado para consultar o seu estado de chaincode e não inclui blocos na cadeia. Apenas implemente e chame funções incluir novos blocos. Use `Query` para ler o valor de seus pares chave/valor do estado de seu chaincode.

Em seu arquivo `chaincode_start.go`, mude a função `Query` para que ele chame uma função de leitura genérica:

```go
func (t *SimpleChaincode) Query(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

O código está agora procurando `read`, portanto, inclua essa função em seu arquivo `chaincode_start.go`:

```go
func (t *SimpleChaincode) read(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
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

Essa função `read` usa `GetState`, que é o complemento para `PutState`. Essa função shim toma apenas um argumento de sequência, que é o nome da chave a ser recuperado. Em seguida, essa função retorna o valor, como uma matriz de bytes, para `Query`, que por sua vez o envia para o manipulador REST.

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

<br>
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
  - Preencha o campo ``Value`` com JSON que especifique um ``enrollID` e `enrollSecret' a partir de suas credenciais:

  ![Exemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Exemplo de registro")

  O *Corpo de resposta* deve ser semelhante ao exemplo a seguir:

  ![Exemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Corpo de resposta de exemplo deregistro")


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

  ![Exemplo de implementação](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Corpo de resposta de exemplo deimplementação")


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

  ![Exemplo de consulta](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Corpo de resposta de exemplo deconsulta")


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
  ![Exemplo de chamada](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Corpo de resposta de exemplo dechamada")


  Execute novamente a consulta acima e a resposta a seguir deverá ser obtida:

  ![Exemplo de Query2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Resposta de exemplo dechamada")


Você acabou de gravar algum chaincode de configuração básica.  

<br>
## Requisitos para demos do Marbles, Commercial Paper e Car Lease
{: #requirements}

Os pré-requisitos a seguir são incluídos com o seu serviço do Bluemix para executar os aplicativos Marbles, Commercial Paper e Car Lease localmente. O seu ambiente do Bluemix clona o Hyperledger Fabric para fornecer essas dependências:

- ID do Bluemix https://console.ng.bluemix.net/ (necessário para criar a sua rede do IBM Blockchain e fornecer credenciais de serviço para peers e a Autoridade de certificação)
- Node.js 0.12.0+ e npm v2+
- Golang Environment (necessário apenas para construir o seu próprio chaincode)

As demos requerem proficiência com Node.js e o módulo express. Deve-se também ter um entendimento conceitual de 'chaincode', 'livro razão' e 'peer' em um contexto de blockchain; consulte o [Glossário do Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md).  

<br>
## Usando a demo do Marbles
{: #marbles}

O aplicativo Marbles demonstra uma transferência de ativo simples entre duas partes. O aplicativo foi projetado para testar o SDK de JavaScript, guiar o seu desenvolvimento e ajudar os desenvolvedores a se familiarizarem com o SDK e o chaincode.

Explore os [Tutoriais do Marbles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) para saber como o aplicativo da web, o SDK e o chaincode funcionam juntos. Se você já estiver familiarizado com o chaincode e o IBM Blockchain, será possível [implementar manualmente](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) a demo para o Bluemix ou clicar no botão Implementar no Bluemix para usar o aplicativo da web:
  
[![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Usando a demo do Commercial Paper
{: #commercialpaper}

O aplicativo Commercial Paper demonstra como uma rede de negócios de papel comercial pode ser implementada usando o IBM Blockchain. A demo do Commercial Paper explora uma rede de blockchain com permissão, na qual os participantes têm funções e níveis de acesso correspondentes designados. Visite o [LEIA-ME do Commercial Paper](https://github.com/IBM-Blockchain/cp-web#readme) para saber mais sobre os componentes dessa demo ou implementá-los no Bluemix imediatamente para ver a rede de negócios em ação:
  
[![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Usando a demo do Car Lease
{: #carlease}

O aplicativo Car Lease demonstra o ciclo de vida de um veículo, a partir da manufatura, através de uma série de proprietários e concluindo com o veículo sendo descartado. A demo usa Node.js para programação do lado do servidor e o Golang para executar o chaincode na rede do IBM Blockchain. A demo inclui duas instâncias de chaincode: uma define as regras para transações de veículo e a outra registra todas as transações de veículo durante o seu tempo de vida. Ambos os programas de chaincode usam objetos de JSON para armazenar dados. Visite o [LEIA-ME do Car Lease](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) para saber mais sobre a arquitetura do aplicativo e atributos de veículo com essa demo ou implementar a demo no Bluemix imediatamente:
  
[![Implementar no Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Chaincode não determinístico
{: #ndcc}

As redes do IBM Blockchain suportam chaincode determinístico apenas. O uso de chaincode não determinístico não é suportado e causará erros graves, em qualquer rede de blockchain.

**Chaincode não determinístico** é qualquer chaincode que **não** resulte no mesmo valor anexado, ao longo do tempo e entre nós, no livro razão de blockchain. Em contraste, o **chaincode determinístico** sempre produz o mesmo valor anexado, ao longo do tempo e entre nós, no livro razão de blockchain.

### Exemplo de chaincode determinístico
Uma transação **chamar** que sempre incrementa o valor de uma variável por um é determinística, porque o resultado é sempre o mesmo, em cada nó, sem variação. Sempre que essa transação for executada com relação a um valor fixo, por exemplo, o valor anexado será sempre seis, em cada nó, toda vez. O resultado de rede para chaincode determinístico é nenhuma divergência no blockchain; a cópia do livro razão em cada nó sempre indica (após a sincronização) que o valor é um maior que a chamada anterior.

### Exemplo de chaincode não determinístico
Uma transação **chamar** que incrementa o valor de uma variável de blockchain com o número de segundos decorridos desde o início do dia (00h) é não determinística, porque ao longo do tempo o valor irá variar entre nós. Cada vez que esta transação for executada com relação a um valor fixo, por exemplo, o valor anexado divergirá entre nós (com raras exceções), porque o número de segundos decorridos desde às 00h irá variar inevitavelmente. O resultado da rede para esse chaincode não determinístico são blockchains divergentes; todos os nós não concordarão com o valor de cinco + o número de segundos decorridos desde as 00h.

### Aleatoriedade
O chaincode deve apresentar nenhuma aleatoriedade nos valores anexados, ao longo do tempo e entre nós. Qualquer aleatoriedade produz blockchains divergentes entre nós, que devem, então, ser resolvidos pela rede. Para evitar aleatoriedade, deve-se assegurar que nenhum chaincode paralelo pode afetar o valor de entrada a partir do chaincode de chamada. Por exemplo, não execute nenhuma transação **consultar** em paralelo com transações **chamar**, porque consultas paralelas poderiam produzir variação nos valores de chamada entre nós.

### Usando uma variável global
Usar uma variável global ou de instância para armazenar um valor que foi recuperado do livro razão ou para configurar um valor no livro razão pode levar a não
determinismo. O chaincode não deve depender de variáveis globais ou de instância que não reterão seu
estado ao longo de reinicializações de um contêiner de chaincode. A seguir está um exemplo que usa uma variável global; o valor de `key`, que é gravado no livro razão por meio da função
`stub.PutState`, é derivado de uma variável global:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iteração sobre um tipo de mapa
A iteração sobre um tipo de mapa pode levar a não determinismo, porque a ordem não é determinística na linguagem de programação Go. A seguir está um exemplo de
iteração sobre o mapa chamado `columnTypes`:

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

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
