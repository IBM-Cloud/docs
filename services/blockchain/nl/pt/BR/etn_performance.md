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


# Desempenho verificado
{: #etn_performance}


Os comportamentos a seguir foram testados e verificados pela IBM. Os resultados foram alcançados em uma rede de Alta segurança, a menos que indicado de outra
forma:
{:shortdesc}

### Desempenho/Estresse

Esse teste foi feito para obter TPS (transações por segundo) de chamadas e consultas sob intervalos de teste de curta duração - 10 minutos e intervalos de teste de longa duração - 60 minutos, com
PBFT / Segurança e Privacidade ativados.  O desempenho pode variar com base no ambiente, tipo de aplicativo, definições de configuração/segurança, tamanho do lote de transação e outros fatores.  (**Nota:** essas métricas foram
alcançadas em uma rede distribuída de múltiplos locatários.)

- example02 de chaincode
- nível de criação de log: erro
- número de encadeamentos: 100
- tamanho do lote: 1000
- duração: 10 min. e 60 min.
- tipos de transação: chamar a->b, chamar b->a, em seguida, repetir & consulta a, consulta b, em seguida, repetir

| Tipo de transação | Número de peers | Número de Encadeamentos | Duração da execução (min) | Transações por segundo |
| ---------- |:-------:|:-----:|:------:|:------:|
| chamadas   |  4  | 100 | 10 | 72  |
| chamadas   |  4  | 100 | 60 | 66  |
| consultas   |  4  | 100 | 10 | 252 |
| consultas   |  4  | 100 | 60 | 248 |

### Resiliência/Consenso

Esse teste foi feito para assegurar a estabilidade e a resiliência de PBFT quando falhas bizantinas ocorrerem.  Os testes incluíram:

- Parar 1 nó e continuar enviando transações de implementação, chamada e consulta.  A rede continua a operar. Executado em cada nó na rede.
- Parar 2 nós; a rede para devido a uma falta de consenso.
- Reiniciar um dos nós interrompidos no teste anterior.  A rede continua e o nó que reiniciou é sincronizado com os outros peers de validação. Para obter etapas detalhadas sobre o teste de PBFT,
consulte o tópico [Testando consenso e disponibilidade](etn_pbft.html).

Continue com o tópico [Teste adicional](etn_next.html) para obter testes adicionais e funcionalidade verificada.  
