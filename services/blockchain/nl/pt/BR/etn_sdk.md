---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}


O Hyperledger Fabric Client (HFC) SDK permite que desenvolvedores de aplicativos construam aplicativos Node.js que interagem com uma rede de blockchain. Aplicativos Node.js que alavancam o SDK do HFC podem ser usados para executar as tarefas de rede a seguir:
{:shortdesc}

* Registre e inscreva usuários com segurança. Um administrador do aplicativo da web com autoridade `registrar` pode registrar e inscrever dinamicamente usuários que se autenticaram no aplicativo da web.
* Envie transações para a rede de blockchain (implementar, chamar e consultar). Todas as transações são anônimas, confidenciais e não vinculáveis sem a autoridade de 'auditor'.
* Armazene chaves privadas sensíveis e certificados em qualquer local, como um banco de dados fora do blockchain. Isso requer a implementação de uma interface de armazenamento de valor da chave simples.

O SDK do HFC fornece APIs, através das quais os aplicativos interagem com uma rede de blockchain do Hyperledger Fabric. Essas APIs são projetadas para suportar dois componentes conectáveis:

1. Armazenamento de valor da chave conectável, que é usado para recuperar e armazenar chaves associadas com um membro. O método `chain.setKeyValStore()` substitui a implementação de armazenamento de valor da chave baseado em arquivo padrão. O armazenamento de valor da chave de cadeia é usado para armazenar chaves privadas sensíveis; portanto, o acesso deverá ser apropriadamente protegido.
2. Serviço de membro conectável, que é usado para registrar e inscrever membros. O método `chain.setMemberServices()` substitui a implementação padrão no `MemberServices`. Os Serviços de membro implementam a malha do Hyperledger como uma rede de blockchain com permissão, que fornece anonimato, incapacidade de ter links de transações e confidencialidade.

É possível incluir o SDK do HFC em seu aplicativo Node.js usando o método off-line ou o método npm:
*  método off-line: primeiramente, copie os arquivos da árvore de origem do Hyperledger Fabric (https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/lib) para o diretório `/lib` do seu aplicativo Node.js. Em seguida, inclua o SDK do HFC em seu aplicativo incluindo o fragmento de código a seguir:

```js
var hfc = require("./lib/hfc");
```

* método npm: a partir da linha de comandos, primeiramente, instale o SDK do HFC a partir do npm com o fragmento a seguir:

```
npm install hfc@0.6.5
```

Em seguida, inclua o SDK do HFC em seu aplicativo com o fragmento de código a seguir:

```js
var hfc = require('hfc');
```  
<br>
## Objetos do HFC
{: #objects}

Os objetos do HFC a seguir (classes e interfaces) são descritos em um alto nível para ajudar a guiar você através da hierarquia de objeto:

* A classe de nível superior é `Chain`, que é a representação do cliente de uma rede de blockchain. O HFC permite que você interaja com múltiplas redes e compartilhe um objeto único `KeyValStore` e `MemberServices` com múltiplos objetos `Chain`, conforme necessário. Para cada rede de blockchain, você incluirá um ou mais objetos `Peer`, que representam os terminais aos quais o HFC se conecta para enviar transações.
* A interface `KeyValStore` é usada por HFC para armazenar e recuperar todos os dados persistentes. Esses dados incluem chaves privadas, que devem ser mantidas seguras. A implementação padrão é uma versão baseada em arquivo localizada na classe `FileKeyValStore`.
* A interface `MemberServices` é implementada pela classe `MemberServicesImpl` e Fornece recursos de segurança e relacionados à identidade como privacidade, incapacidade de ter links e confidencialidade. Essa implementação emite *eCerts* (certificados de inscrição de membro) e *tCerts* (certificados de transação para cada membro).
* A classe `Member` representa usuários finais que transacionam na rede e outros tipos de membros como peers (nós). Use a classe `Member`, que interage com o objeto `MemberServices`, para *registrar* e *inscrever* membros e usuários. Também é possível implementar, consultar e chamar chaincode diretamente a partir da classe 'Membro' transacionando com objetos `Peer`; essa implementação simplesmente delega o trabalho para um objeto `TransactionContext` provisório.
* A classe `TransactionContext` implementa a maior parte da implementação, chamada e consulta lógica. Cada instância `TransactionContext` recebe um tCert exclusivo a partir de `MemberServices`, que ela sempre usa para enviar transações. Para emitir múltiplas transações com o mesmo tCert, recupere um objeto `TransactionContext` diretamente de um objeto Membro e emita múltiplas operações de implementação, chamada e consulta. No entanto, usar um tCert único para múltiplas transações vincula as transações de forma que elas sejam identificáveis como envolvendo o mesmo usuário anônimo. Para evitar a ligação de transação, chame implementação, chamada e consulta no objeto `User` ou `Member`.  

<br>

## Aplicativo de amostra Node.js
{: #nodesample}

O aplicativo de amostra Node.js alavanca as APIs de SDK do HFC para interagir com uma rede de blockchain do Bluemix. As funções do programa com os planos de rede de blockchain (iniciador e HSBN) e com qualquer sistema operacional de operação e do lado do cliente.

O objetivo é usar um aplicativo JavaScript -- [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) -- para implementar com êxito uma parte do chaincode -- [chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/src/chaincode/chaincode_example02.go) -- em sua rede do Bluemix, seguida por uma chamada e consulta.  

1. Esse programa requer ambos, o Node.js e o gerenciador de pacote do JavaScript npm.  Instalar a versão mais recente de [Node.js](https://nodejs.org/en/) incluirá npm automaticamente.  

1. Abra um terminal e crie um diretório (área de trabalho) no qual deseja colocar o código-fonte para esta demo.  Por exemplo:

    ```
    mkdir -p $HOME/workspace
    ```

1. Acesse o diretório recém-criado e clone o repositório [SDK-Demo](https://github.com/IBM-Blockchain/SDK-Demo).  Certifique-se de ter a versão correta do [Git](https://git-scm.com/downloads) para o sistema operacional instalado antes de executar o comando `git clone`:

     ```
     cd $HOME/workspace
     git clone https://github.com/IBM-Blockchain/SDK-Demo.git
     ```
 Se sua rede estiver executando o Hyperledger Fabric v0.5, verifique a ramificação v0.5 depois de ter clonado:

     ```
     cd $HOME/workspace/SDK-Demo
     git checkout v0.5
     ```

1. Agora, é necessário utilizar as Credenciais de Serviço de uma instância de blockchain.

1. Se você ainda não tiver feito isso, acesse o ladrilho [Blockchain](https://console.ng.bluemix.net/catalog/services/blockchain/) no Bluemix e crie uma instância do serviço. Selecione o plano **Starter Developer** ou o plano **High Security Business Network**. Clique no botão **CREATE** depois de ter curado sua rede.  Isso abrirá o Painel de Serviço.  Clique na guia **Credenciais de Serviço** na parte superior da página para acessar o peer e os dados de registro de usuário para sua rede.  **Nota**: para redes HSBN, as Credenciais de Serviço não podem ser geradas automaticamente.  Simplesmente, clique no botão **Nova Credencial**, que abrirá uma nova janela.  Em seguida, clique em **Incluir** na parte inferior da janela.  Isso preencherá uma carga útil JSON que contém as Credenciais de Serviço.

1. Atualize seu arquivo ServiceCredentials.json, que você recebeu ao clonar o repositório SDK-Demo, com suas novas credenciais.

1. Quando o programa é executado, o SDK do HFC cria o diretório `keyValStore-<network-id>` dentro de $HOME/workspace/SDK-Demo.  Esse diretório `keyValStore-<network-id>` contém as chaves criptográficas para cada usuário inscrito.  Não é necessário excluir o diretório `keyValStore` ao se conectar às novas redes do Bluemix; em vez disso, diretórios `keyValStore-<network-id>` exclusivos serão criados para cada instância do Bluemix.  **NÃO** exclua este material de criptografia até que sua rede seja excluída ou reconfigurada.  Sem esses dados, seu cliente não poderá se comunicar com o servidor de autoridade de certificação do Bluemix e a inscrição falhará.

1. De sua pasta SDK-Demo, execute o programa de nó:

	```
	node helloblockchain.js
	```
	Ative logs de depuração:
	```
	DEBUG=hfc node helloblockchain.js
	```

	Ative rastreios de gRPC:
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js
	```

Se as transações `deploy`, `invoke` e `query` forem bem-sucedidas, você verá as mensagens a seguir em seu terminal:

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

**Nota**: o código-fonte de chaincode é mantido na pasta **src/chaincode** em seu repositório SDK-Demo.  Esta pasta **TAMBÉM** contém uma pasta **/vendor**, que contém bibliotecas e dependências do código base do Hyperledger Fabric.  Se você substituir o arquivo de chaincode atual -- chaincode_example02.go -- por seu próprio chaincode, certifique-se de manter a pasta **/vendor**.  Essas dependências são necessárias para que o peer compile com êxito seu chaincode e crie o contêiner. Além disso, se você tiver alguma biblioteca dependente, certifique-se de incluí-la na pasta **/vendor**.

Esteja ciente de que ao executar em uma rede do Starter Developer, poderá, algumas vezes, demorar um tempo maior para que a implementação seja bem-sucedida e o contêiner de chaincode seja iniciado.  No entanto, uma
vez iniciado, implementações e chamadas subsequentes serão executadas imediatamente, porque os arquivos de pré-requisito foram armazenados na máquina host para a sua
instância de blockchain.  

Navegue para a guia **Blockchain** a partir de seu **Console de rede**. Essa visualização mostra blocos sendo anexados ao livro razão de blockchain conforme o programa helloblockchain.js emite transações de implementação e chamada. A captura de tela a seguir mostra os resultados da execução de helloblockchain.js duas vezes, com os argumentos padrão para "a" e "b":

   ![Workspace3 de nó](images/nodeworkspace3.PNG "Node workspace 3")  

<br>

## Detecção de problemas
Certifique-se de estar executando o **hfc@0.5.4** ou o **hfc@0.6.5** emitindo qualquer um dos comandos a seguir a partir do seu diretório **/workspace**:
  * npm list | grep hfc
  * npm list -g | grep hfc (Se instalado usando a sinalização global `-g`)

As redes que estão usando a ramificação v0.5 precisarão da versão hfc anterior - 0.5.4

Use o procedimento a seguir se você receber uma mensagem de consulta:

  ```
Failed to query chaincode, function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, error={"error":{"status":"FAILURE","msg":{"type":"Buffer","data":[69,114,114,111,114,58,70,97,105,108,101,100,32,116,111,32,108,97,117,110,99,104,32,99,104,97,105,110,99,111,100,101,32,115,112,101,99,40,112,114,101,109,97,116,117,114,101,32,101,120,101,99,117,116,105,111,110,32,45,32,99,104,97,105,110,99,111,100,101,32,40,57,98,101,48,97,48,101,100,51,102,49,55,56,56,101,56,55,50,56,99,56,57,49,49,99,55,52,55,100,50,102,54,100,48,101,50,48,53,102,97,54,51,52,50,50,100,99,53,57,56,100,52,57,56,102,101,55,48,57,98,57,98,56,100,41,32,105,115,32,98,101,105,110,103,32,108,97,117,110,99,104,101,100,41]}},"msg":"Error:Failed
to launch chaincode spec(premature execution - chaincode (9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d) is
being launched)"}
  ```

Aumente o tempo de espera da implementação no aplicativo Node.js. O padrão é configurar para 60 segundos, mas pode levar mais tempo para o código ser corretamente implementado e compilado e para começar a ser executado no contêiner do Docker. Tente aumentar o tempo de espera da implementação para 120 segundos. Essa idiossincrasia é observada apenas nos planos Starter Developer como resultado dos recursos computacionais compartilhados na máquina que hospeda sua instância de cadeia de blocos:

  ```js
chain.setDeployWaitTime(120);
  ```

Logo que o seu chaincode é implementado com sucesso na rede, é possível reduzir o tempo de espera de implementação a uma quantia nominal, como alguns segundos.

Se você receber um erro de handshake, tente uma versão de `grpc` diferente. É possível acessar a sua versão do grpc com um dos comandos a seguir:
    - `npm list | grep grpc`
    - `npm list -g | grep grpc`  



<br>
## Chaves públicas e privadas
{: #keys}

O Hyperledger Fabric usa autoridades de certificação e suas chaves públicas e privadas subjacentes para atender aos requisitos de segurança de negócios operando em um blockchain compartilhado. O gerenciamento de identidade de membro, o gerenciamento de função e a privacidade transacional podem todos ser controlados por meio do SDK do HFC.

O usuário e a privacidade transacional em um blockchain compartilhado são gerenciados por meio da implementação de uma estrutura de PKI (Public Key Infrastructure). O PKI, através de autoridades de certificação, gerencia a geração, a distribuição e a revogação de chaves e certificados digitais. As especificações técnicas completas para PKI e Serviços de Associação são descritas na seção de segurança do Hyperledger Fabric v0.6 [especificação de protocolo](http://hyperledger-fabric.readthedocs.io/en/v0.6/protocol-spec/). Os princípios de configuração básica do PKI do Hyperledger Fabric são explicados abaixo:

1. A Autoridade de registro (RA) valida a identidade de um usuário que estiver solicitando acesso à rede de blockchain.  Isso pode ser feito dinamicamente por um usuário com autoridade de `registrar` ou manualmente, editando o arquivo membersrvc.yaml. O processo de registro ocorre fora da banda e é executado por meio da função `RegisterUser`. A RA designa credenciais de inscrição – `<enrollID>` e `<enrollPWD>` – para o usuário.

2. O usuário, então, envia uma solicitação de inscrição para a Autoridade de certificação de inscrição (ECA), usando a função `CreateCertificatePair`. Essa carga útil contém a `<enrollPWD>` única do usuário, Chave de verificação de assinatura pública e Chave de criptografia pública, e é assinada com a Chave de verificação de assinatura privada do usuário. <br><br>Após o recebimento da solicitação de inscrição, o ECA emite um desafio criptografado para o usuário que pode ser decriptografado apenas com a Chave de criptografia privada do usuário. Após decriptografar o desafio, o usuário reenviará a solicitação de certificado. O ECA, contingente de uma resposta decriptografada com precisão, retorna um par de certificados autenticados assinados com a sua assinatura digital. <br><br>A assinatura digital é produzida efetuando hash criptograficamente na solicitação de certificado (mensagem) usando o algoritmo SHA-2 para produzir uma "compilação." Esse "trecho da mensagem" é então criptografado com a chave de assinatura privada do ECA. Os membros da rede podem, então, autenticar a assinatura digital decriptografando-a com a chave de assinatura pública do ECA. O par de certificados de inscrição retornados (eCert) contém um certificado para assinatura de dados (privado) e um para criptografia de dados (público). Esse par de eCerts é estático e de longo prazo e pode ser visível ou invisível para transações.

3. Para transacionar em qualquer rede de blockchain, cada usuário também deve ter certificados de transação (tCerts). Após a inscrição bem-sucedida, um usuário envia uma solicitação para a Autoridade de certificação de transação (TCA) para um lote de tCerts. Um tCert é de curto prazo, específico para uma transação e pode ser modificado pelo cliente usando uma API. Depois de verificar o eCert do usuário, o TCA designa um lote de tCerts e uma KeyDF_Key (Chave de função de derivação de chave), que permite ao usuário decriptografar as suas chaves privadas. Enquanto a KeyDF_Key única é usada para cada tCert no lote, a chave privada resultante que é gerada é exclusiva para cada tCert. Para transacionar, um cliente deve ser capaz de assinar a carga útil de transação com a chave privada decriptografada. Só então uma transação será encaminhada para peers de validação de rede para consenso.
