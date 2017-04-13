---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Teste adicional
{: #etn_next}


Os testes a seguir foram executados no ambiente do High Security Business Network (a menos que indicado de outra forma) para testar a função de chaincode, livro razão, execuções longas, simultaneidade e transações complexas.  Os nós validadores e de serviços de associação foram executados como guests de VM (máquina virtual) dentro do contêiner de serviços seguros no LinuxONE OS.  Os valores usados abaixo foram escolhidos com base na entrada do cliente e não devem ser confundidos com os valores máximos. (Nota: alguns desses testes são repetidos nas seções [Node.js SDK](etn_txn.html) e [Testando consenso e disponibilidade](etn_pbft.html).)

{:shortdesc}

1. Função de chaincode - interfaces de chaincode foram exercitadas para assegurar que as transações `Implementar`, `Chamar` e `Consultar`
funcionam adequadamente usando a API REST e a CLI. A API REST e a CLI foram utilizadas para testar todas as funções de terminal, incluindo Bloco, Blockchain, Chaincode, Rede, Escrivão e
Transações, conforme descrito na Especificação de Protocolo do Hyperledger.
2. Livro Razão - a criação de 20.000 registros de 1 K de cargas úteis no livro razão baseada em diferentes ambientes de direcionamento. Os testes incluíram um
cliente criando 20 mil registros de uma maneira serializada.
3. Execuções longas - esse teste foi feito enviando chamadas, altura de cadeia e consultas ao longo de múltiplos nós por 72 horas usando o chaincode de demo example02.
4. Node.js SDK - o Node.js SDK aprimorado foi usado para registrar e inscrever usuários e executar implementação, chamadas e consulta em um peer no modo de desenvolvimento (peer de início com:
`peer node start –peer -chaincodedev`) e no modo de rede (peer inicial com: `peer node start`).
5. Simultaneidade básica - esse teste foi feito enviando chamadas simultâneas para cada um dos quatro peers por uma duração de 10 minutos, com 1 KB de cargas úteis, medindo a altura de cadeia e
consultando o estado do livro razão.
6. Transações complexas - esse teste foi feito enviando aleatoriamente uma combinação de consultas e chamadas de vários tamanhos de carga útil, variando de 10
mil a 500 mil, para peers por uma duração de 10 minutos. A altura de cadeia e a consulta de estado do mundo foram medidas para assegurar a sincronização do livro
razão compartilhado ao longo de peers de rede.
