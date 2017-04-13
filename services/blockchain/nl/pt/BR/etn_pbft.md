---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Testando consenso e disponibilidade
{: #etn_pbft}

Ambos, o plano do Starter Developer e o plano do High Security Business Network, permitem que você teste o protocolo de consenso do Practical Byzantine Fault Tolerance (PBFT) em uma rede de blockchain
de quatro nós. Os tópicos a seguir fornecem detalhes sobre o consenso em geral e o PBFT em particular. Logo que você estiver pronto para iniciar o teste, casos de teste do PBFT serão fornecidos.  
{:shortdesc}  

## O que é consenso?

O consenso é um método para validar a ordem das solicitações ou transações (implementar e chamar) em uma rede de blockchain. A ordenação correta de transações é crítica, porque muitas transações têm uma
dependência em uma ou mais transações anteriores (débitos em conta muitas vezes têm uma dependência em créditos anteriores, por exemplo).

Em uma rede de blockchain, não há autoridade centralizada que determine a ordem de transação; em vez disso, muitos nós de validação (ou peers) implementam o protocolo de consenso de rede. O consenso
assegura que um quorum de nós concorda com a ordem na qual as transações são anexadas ao livro razão compartilhado. Resolvendo qualquer discrepância na ordem de transação proposta, o consenso assegura que
todos os nós de rede de blockchain estão operando em um livro razão idêntico. Em outras palavras, o consenso garante* a integridade e a consistência de todas as transações de rede de blockchain.

* Essa garantia depende de variáveis como o protocolo de consenso específico implementado e o número de nós na rede de blockchain. Ambos os planos do Blockchain no Bluemix implementam o protocolo de
consenso do PBFT.  

<br>
## O que é PBFT?

Practical Byzantine Fault Tolerance (PBFT) é um tipo de protocolo de consenso. A função de um protocolo de consenso é manter a ordem de transações em uma rede de blockchain, apesar das ameaças para essa
ordem. Uma tal ameaça é a falha simultânea arbitrária (um tipo de falha bizantina) de múltiplos nós de rede. Usando o PBFT, uma rede de blockchain de (N) nós pode suportar (f) número de nós bizantinos,
em que f = (N-1)/3. Em outras palavras, o PBFT assegura que um mínimo de 2\*f + 1 nós atinge o consenso sobre a ordem de transações antes de anexá-las ao livro razão compartilhado. Derivar qualquer fórmula
revela a regra de que uma rede do PBFT garante a consistência e a integridade de dados apesar das falhas bizantinas em menos de um terço de todos os nós de rede.  

<br>
## PBFT e a sua rede de blockchain

A regra do PBFT 2\*f + 1 tem as implicações a seguir para ambos, o plano do Starter Developer e o plano do High Security Business Network:

1. A rede pode tolerar não mais do que um nó bizantino. Cada rede contém N= 4 nós; portanto, aplicar a fórmula para o número máximo de nós bizantinos tolerados resulta em:
f=(4-1)/3=1. Se dois ou mais nós bizantinos (f>1) existirem, uma rede do PBFT de 4 nós não pode garantir consistência ou integridade do livro razão ao longo de todos os nós. (Para comparação, tolerar dois
nós bizantinos iria requerer f=(7-1)/3=2 ou um mínimo de rede de blockchain do PBFT de 7 nós.)
2. Se menos de 2\*f + 1 nós estiverem on-line, a rede para de anexar ao livro razão, porque o PBFT não pode garantir consistência ou integridade de dados ao longo de nós. A rede vai continuar a anexar
ao livro razão quando pelo menos 2\*f + 1 nós estiverem on-line (três ou quatro nós, neste caso).
3. Como apenas um mínimo de 2\*f + 1 nós devem chegar a um consenso antes de prosseguir para o próximo bloco de transações, o livro razão sobre quaisquer nós adicionais (além de 2\*f + 1) ficará
temporariamente atrasado. Esse atraso na sincronização no livro razão compartilhado ao longo de todos os nós é uma limitação inevitável em qualquer rede do PFBT.
<br>

## Casos de teste de consenso
Os casos de teste de consenso foram vetados pela IBM como cumpridores das normas de disponibilidade de rede para o PBFT:

1. [Testando o PBFT sem nós bizantinos](pbft_test1.html). O processo de consenso executa transações e anexa ao livro razão.
2. [Simulando um nó bizantino](pbft_test2.html) parando um nó e continuando a enviar transações de implementação, chamada e consulta. O processo de consenso do PBFT executa transações e anexa ao livro razão. Esse teste
foi repetido para cada nó em um ambiente de quatro nós.
3. [Simulando dois nós bizantinos](pbft_test3.html) parando dois nós e continuando a enviar transações de implementação, chamada e consulta. Devido à falha em chegar a um consenso do PBFT, as transações não são
executadas ou anexadas ao livro razão.
4. [Reiniciando um nó que foi interrompido](pbft_test4.html) no caso de teste anterior (Teste 3). O processo de consenso do PBFT continua a executar transações e a anexar ao livro razão. O nó que foi reiniciado sincroniza o seu
livro razão com o livro razão compartilhado.  

Atenção: revise as notas a seguir antes de iniciar o seu teste de consenso:

- Todos os casos de teste de consenso usam a API REST para interagir com os peers de rede.
- HTTP/2 é o protocolo de comunicação; os casos de teste usam as URLs de peer. Por exemplo: 'VP0–api.dev.blockchain.ibm.com:80'. Os valores simbólicos ***VP0, VP1, VP2 e VP3*** são
usados como marcadores para as URLs de peer literais.
-  Para efetuar login para um peer, use as credenciais que foram fornecidas quando você implementou o seu serviço do Bluemix. Para os casos de teste, **test\_user1** e
**test\_user1\_enrollSecret** são usados como os valores para *enrollID* e *enrollSecret*, respectivamente.
-  Simule travamentos de nó parando e reiniciando manualmente peers com os botões **Ações** no console de rede. A Figura 1 abaixo mostra as **Ações** na guia
**Rede**:

![](images/stopstartpeer.png "Parar e iniciar peers")
*Figura 1. Parar e iniciar peers*

- Os casos de teste usam **chaincode_example02**, por padrão, de: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go/chaincode_example02. No entanto, é possível usar seu próprio chaincode ou qualquer um dos exemplos de chaincode em: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go.
- As solicitações são colocadas em lote em uma transação para processamento. No entanto, é possível assegurar o processamento imediato contando com o valor de tempo limite de lote; esperar pelo menos
dois segundos antes de enviar a próxima solicitação processará a transação imediatamente.
