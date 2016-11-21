---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Sobre o blockchain
{: #ibmblockchain_overview}
Última atualização: 23 de setembro de 2016
{: .last-updated}

## O que é blockchain?
{: #what}

Blockchain é uma tecnologia para uma nova geração de aplicativos transacionais que estabelece confiança, prestação de contas e transparência, enquanto simplifica processos de negócios. A rede de
blockchain foi primeiramente apresentada por bitcoin, mas os seus usos práticos se estendem muito além de trocas de criptomoedas. Com o blockchain, a IBM está reimaginando as trocas de negócios mais
fundamentais e abrindo a porta para um mundo novo de interações digitais.

O Blockchain foi planejado para reduzir consideravelmente o custo e a complexidade de processos de negócios entre empresas. O seu livro razão distribuído torna mais fácil criar redes de negócios com
custo reduzido, no qual praticamente qualquer coisa de valor pode ser rastreada, sem um ponto de controle centralizado. O Blockchain já está mostrando uma grande promessa em uma ampla variedade de aplicativos de
negócios. Como apenas um exemplo, as redes de blockchain permitem que comércios de valores mobiliários sejam liquidados em minutos, em vez de dias. O Blockchain também está ajudando as empresas a simplificarem
o fluxo de mercadorias e pagamentos e permitindo que os fabricantes reduzam os recalls de produto compartilhando abertamente os logs de produção com OEMs e reguladores.  
<br>

## Termos-chave
{: #keyterms}
Os termos a seguir são instrumentais para obter um entendimento de conceitos de blockchain:

**Transacionador**: um participante de rede conectado à rede de blockchain por meio de um nó, que envia transações a partir de um cliente usando um SDK ou uma API.

**Transação**: uma solicitação de um transacionador para executar uma função na rede de blockchain. Os tipos de transação de implementação, chamada e consulta que são implementados
por meio de funções de chaincode definidas no contrato de API da malha.

**Livro razão**: uma sequência de blocos criptograficamente vinculados, contendo transações e o estado do mundo atual. Além dos dados de transações anteriores, o livro razão também
contém os dados para aplicativos chaincode atualmente em execução.

**Estado do mundo**: banco de dados de chave-valor usado por chaincodes para armazenar o seu estado quando executado por uma transação.

**Chaincode**: lógica integrada que codifica as regras para tipos específicos de transações de rede. Os desenvolvedores gravam aplicativos chaincode e os implementam na rede. Os
usuários finais, em seguida, chamam o chaincode por meio de um aplicativo do lado do cliente que faz interface com um peer ou nó de rede. O Chaincode executa transações de rede que, se validadas, serão anexadas
ao livro razão compartilhado e modificarão o estado do mundo.

**Peer de validação**: um nó de rede que executa o protocolo de consenso para a rede para validar transações e manter o livro razão. As transações validadas são anexadas ao livro
razão, em blocos. Se uma transação falhar no consenso, será eliminada do bloco e, portanto, não será gravada no livro razão. Um peer de validação (VP) tem autoridade para implementar, chamar e consultar chaincode.

**Peer de não validação**: um nó de rede que funciona como um proxy, conectando transacionadores para peers de validação. Um peer de não validação (NVP) encaminha solicitações de
chamada para o seu peer de validação (VP) conectado. Ele também hospeda o servidor de fluxo do evento e o serviço REST.

**Consenso**: um protocolo que mantém a ordem de transações de rede de blockchain (implementar e chamar). Validar nós funciona coletivamente para aprovar transações implementando o
protocolo de consenso. O consenso assegura que um quorum de nós concorda com a ordem de transações no livro razão compartilhado. Resolvendo qualquer discrepância nessa ordem, o consenso assegura que todos os
nós operem em um livro razão de blockchain idêntico. Consulte o tópico [consenso](etn_pbft.html) para obter mais informações e casos de teste.  

**Rede com permissão**: uma rede de blockchain em que cada nó é necessário para manter uma identidade de membro na rede e cada nó tem acesso apenas às transações que as suas permissões
permitirem.  

<br>
## Conceitos Principais
{: #keyconcepts}

**Visão geral**: o Blockchain é um tipo específico de rede, no qual os membros controlam e trocam ativos digitalizados. Um livro razão compartilhado contém o único registro de todas
as transações de rede e é replicado entre todos os membros de rede. Os aplicativos chaincode contêm contratos autoexecutáveis e aplicativos do lado do cliente que fazem interface com a rede através de um SDK ou
uma API.

Duas ou mais partes de transação, como membros de uma rede de blockchain, implicitamente concordam com os termos do contrato inteligente que governa a transação (por exemplo, após o recebimento do ativo
"a", ativo "b" ser devido). Uma vez implementadas no blockchain, funções no contrato podem ser chamadas (ou seja, uma transação pode ser acionada). Chamadas subsequentes são ordenadas por um nó de
início e transmitidas para peers de validação para consenso. Após a validação, as transações são executadas e registradas no livro razão em blocos. O livro razão será, então, distribuído para todos os nós de
rede por meio de replicação. Logo que anexadas ao livro razão, as transações não poderão ser mudadas ou excluídas; a única maneira de desfazer ou mudar os efeitos de uma transação aprovada será enviar uma
transação subsequente.

**Rede**: uma rede de blockchain é caracterizada como segue:

- Uma rede ponto a ponto distribuída, descentralizada, com nós que representam os participantes de rede, como bancos, agências do governo, fabricantes e firmas de segurança.
- Um grupo de peers que valida transações por meio de um protocolo de consenso antes de confirmá-los para um livro razão compartilhado.

**Livro razão compartilhado**: o livro razão compartilhado é a fonte isolada de verdade ou o histórico inteiro de transações validadas, em uma rede de blockchain. Qualquer
discrepância no livro razão compartilhado ao longo de nós é resolvida por meio de consenso. O livro razão tem os atributos a seguir:
- Ele registra todas as transações validadas na rede.
- Ele é compartilhado entre todos os participantes da rede.
- Ele é replicado, para que cada participante tenha a sua própria cópia.
- Ele é com permissão, para que os participantes possam visualizar apenas as suas próprias transações.

**Exemplo**: a Figura 1 representa uma rede de blockchain de patrimônios de exemplo e o livro razão compartilhado:
![Livro razão compartilhado](images/Architecture_shared_ledger.png "Rede de blockchain de patrimônios de exemplo")
*Figura 1. Um exemplo de livro razão compartilhado*

A Figura 1 mostra os participantes de rede típicos em um mercado de ações: Administrador de ativo (banco), Front Office, Operações, depósito de títulos (CSD) e uma parte de verificação
(Verificação/CCP):
1. Usando um aplicativo cliente, o administrador chama o chaincode para comprar e vender blocos de títulos.  
2. As transações podem ser acionadas a partir de qualquer nó de rede, mas são sempre encaminhadas para o nó de validação primário (líder), que ordena as transações. O nó primário transmite as
transações ordenadas para todos os peers de validação para consenso ou concordância, na ordem proposta.
3. Se houver concordância com a ordem de transações, as transações serão executadas e anexadas ao livro razão em cada nó de validação. O livro razão será então replicado para todos os nós de
rede.  

## Arquitetura de rede e do aplicativo
{: #architecture}

A Figura 2 representa uma rede de blockchain com permissão de exemplo, que apresenta uma arquitetura de ponto a ponto distribuída, descentralizada e uma
Autoridade de certificação gerenciando funções de usuário e permissões:
![Rede de blockchain](images/Architecture_network_and_application.png "Rede de blockchain permissão de exemplo")
*Figura 2. Uma rede de blockchain com permissão: o fluxo de dados e o acesso à rede são governados por funções de membro*

As descrições a seguir correspondem à arquitetura e ao fluxo mostrados na Figura 2, que não representam um processo sequencial:

**A:** Um usuário do Blockchain envia uma transação para a rede do Blockchain com permissão. A transação pode ser uma implementação, chamada ou consulta e é emitida por meio de um
aplicativo do lado do cliente que alavanca um SDK ou diretamente por meio de uma API REST.  

**B:** Redes de negócio confiáveis fornecem acesso a reguladores e auditores, como a SEC em um mercado de ações dos EUA.  

**C:** Um Operador de rede do Blockchain gerencia permissões de membro, como a inscrição do Regulador (B) como um "auditor" e do Usuário do Blockchain (A) como um
"cliente." Um auditor poderia ser restrito a transações de consulta, enquanto que um cliente poderia ser autorizado a implementar, chamar e consultar determinados tipos de chaincode.

**D:** Um Desenvolvedor do Blockchain grava chaincode (contratos inteligentes) e aplicativos do lado do cliente para chamar contratos inteligentes. O Desenvolvedor do Blockchain
poderia implementar o chaincode diretamente na rede, por meio de uma interface REST. Para incluir credenciais a partir de uma Origem de dados tradicional em chaincode, o desenvolvedor poderia usar uma conexão
fora da banda para acessar os dados (G).

**E:** Um usuário do Blockchain se conecta à rede através de um nó peer (A). Antes de continuar com quaisquer transações, o nó recupera a inscrição do usuário e certificados de
transação da Autoridade de certificação. Os usuários devem possuir esses certificados digitais para transacionar em uma rede com permissão.

**F:** Um usuário que tenta direcionar o chaincode poderia ser solicitado a verificar as suas credenciais em uma Origem de dados tradicional (G). Para confirmar a autorização do
usuário, o chaincode pode usar uma conexão fora da banda para esses dados, através de uma plataforma de Processamento tradicional.

A Figura 3 mostra os componentes principais do IBM Blockchain. Membership Services, Blockchain Services e Chaincode Services são estruturas lógicas, não um particionamento físico de componentes
em processos, espaços de endereço ou máquinas virtuais separados: ![Arquitetura de Referência](images/Architecture_core_com.png "Reference Architecture")
*Figura 3. Arquitetura de referência de malha do Hyperledger*

**Membership Services**: o Membership Services gerencia identidades de usuários em uma rede de blockchain com permissão por meio do peer de Autoridade de certificação. O Membership
Services fornece uma distinção de funções combinando elementos de Public Key Infrastructure (PKI) e descentralização (consenso). Em contrapartida, as redes sem permissão não fornecem autoridade
específica de membro ou uma distinção de funções.

Um blockchain com permissão requer entidades para registrar-se em credenciais de identidade de longo prazo (Certificados de inscrição), que podem ser distintas de acordo com o tipo de entidade. Para
usuários, um Certificado de inscrição autoriza a Autoridade de certificação de transação (TCA) a emitir credenciais pseudônimas; esses certificados autorizam transações enviadas pelo usuário. Certificados de
transação persistem no blockchain e permitem que os auditores autorizados associem transações que não podem ser vinculadas de outra maneira.

**Blockchain Services**: o Blockchain Services gerencia o livro razão compartilhado usando um protocolo de ponto a ponto, que é construído no HTTP/2. As estruturas de dados são
altamente otimizadas para fornecer o algoritmo hash mais eficiente para manter a replicação do livro razão compartilhado. O PBFT é implementado como o protocolo de consenso.    

**Chaincode Services**: o Chaincode Services fornece um método seguro e leve para execução de chaincode de ambiente de simulação nos nós de validação. O ambiente é um contêiner
“trancado” e seguro, juntamente com um conjunto de imagens de base sinalizado contendo linguagem de OS e de chaincode segura, camadas de tempo de execução e de SDK para Go, Java e Node.js. Linguagens
adicionais podem ser ativadas, se necessário.

Consulte a [especificação de protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) para o Hyperledger Fabric 0.5 para saber mais sobre a
implementação de blockchain da IBM.
