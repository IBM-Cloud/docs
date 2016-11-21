---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain on z
{: #zblockchain}
Última atualização: 8 de julho de 2016
{: .last-updated}



É possível usar o serviço de blockchain na oferta dedicada do Bluemix com z/OS para criar ativos digitais privados e seguros, que podem, então, ser negociados com rapidez e segurança sobre redes com
permissão.  *(Informações adicionais como parte de descrições simples)*
{:shortdesc}


* A quantia de conteúdo merece que isto tenha a sua própria seção?  Ou desejamos deixá-lo como um tópico integrado sob "Sobre?"
* Espere informações relativas a PBFT, Segurança, Desempenho, Suporte.


## PBFT
{: #PBFT}

O Practical Byzantine Fault Tolerance (PBFT) é um protocolo de consenso seminal que pode ser conectado e configurado por implementação. O pacote `obcpbft` é uma implementação do
protocolo de consenso seminal do [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT"), que fornece um consenso entre validadores, apesar de um limite de validadores agindo como
*bizantinos*, ou seja, sendo maliciosos ou falhando de uma maneira imprevisível. Na configuração padrão, ambos PBFT e Sieva são projetados para execução em pelo menos *3t+1*
validadores (réplicas), tolerando até *t* potencialmente com falha (incluindo réplicas maliciosas ou *bizantinas*). Para saber mais sobre funções principais do PBFT, consulte a
seção [especificação de protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) do Hyperledger Project do Linux Foundation. 

Assista a uma [![visualização](http://www.youtube.com/watch?v=EKa5Gh9whgU)(http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)]

*(É necessário indicar uma razão prática pela qual os usuários precisam conhecer o PBFT. Que função o PBFT executa em suporte do blockchain on z e a sua relação com esse suporte.)*


### Casos de falha suportados
{: #failure}

*Quais casos de falha suportamos e o que não suportamos aqui.*

*(Barry Mosakowski/Raleigh/IBM ou Tuan Dang/Raleigh/IBM podem fornecer mais detalhes.)*

### Disponibilidade da oferta dedicada com z/OS
{: #Availability}

*Disponibilidade e expectativas em torno de disponibilidade com base em teste do PBFT.*

*(São necessários mais detalhes.)*

### Verificando a funcionalidade básica de PBFT
{: #Test PBFT}

*(Informações do Gari. São necessários mais detalhes do Jason sobre como executar as etapas de teste, incluindo capturas instantâneas.)*

Para verificar a funcionalidade de configuração básica do PBFT, execute as etapas a seguir:

1. Envie transações com relação a um ou mais peers na rede.
2. Verifique se pelo menos *2f+1* (3 neste caso) peers têm o mesmo estado. *(Como verificar? São necessários detalhes de caso de teste.)*

  *Um exemplo usando a API REST*
3. No painel, clique no botão para parar o peer 4. *(Use a funcionalidade "parar peer" no painel para parar o peer 4. É necessário caso de teste para descrever a operação detalhada.)*
4. Verifique se a rede continua o processamento. *(Como verificar?)*
5. No painel, clique no botão para parar o peer 3.
6. Verifique se a rede para o processamento.
7. No painel, clique no botão para reiniciar o peer 3.

Se o peer 3 recuperar o atraso e a rede continuar o processamento, será possível usar funções de configuração básica do PBFT.

**Notas:**
* Após reiniciar o peer 3, será necessário esperar o tempo limite antes de enviar novas transações para o peer 3.

* Transações que são enviadas para peers ativos quando a rede para o processamento serão armazenadas em buffer e enviadas à rede após a rede continuar o processamento.

## Ambiente para o blockchain on z
{: #z environment}

Para usar o serviço de blockchain na oferta dedicada do Bluemix com z/OS, certifique-se de que o seu ambiente atenda aos requisitos a seguir:

* Quatro redes de peer que estão executando PBFT com serviços de associação. Para saber mais sobre serviços de associação, consulte a seção
[especificação de protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) do Hyperledger Project do Linux Foundation. 
* Uma rede isolada que não tem computadores ou memória compartilhados.
* Peers isolados dentro da rede.
* Um sistema que é protegido contra administradores de sistema em nuvem.

O monitor de blockchain fornece uma visão geral de seu ambiente de blockchain e recupera detalhes sobre a sua rede. Para saber mais sobre o seu ambiente de blockchain e como monitorá-lo,
consulte [Gerenciando chaincode com o monitor de blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) e
[Aplicativos de amostra e tutoriais para blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Segurança

*Não fornecer informações de segurança no documento?*

## Desempenho

*Não fornecer informações de desempenho no documento?*

## Obtendo suporte ao cliente

Se você tiver problemas com o serviço de blockchain na oferta dedicada do Bluemix com z/OS, siga o processo de resolução de problemas do IBM Bluemix. Consulte
[Resolução de Problemas](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html) para obter mais informações sobre como obter ajuda.
