---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoramento para o IBM Bluemix Container Service
{: #monitoring_bmx_containers_ov}

No {{site.data.keyword.Bluemix}}, as métricas do contêiner são coletadas automaticamente de fora
do contêiner, sem precisar instalar e manter agentes dentro do contêiner.{:shortdesc}

Agentes no contêiner podem ter gastos adicionais e tempos de instalação
significativos para instâncias da nuvem e grupos de escala automática leves de curta duração, onde os contêineres
podem ser rapidamente criados e destruídos. Essa abordagem de coleção de dados fora da banda elimina esses
desafios e remove a carga de monitoramento dos usuários.

Um processo que está em execução no host executa o monitoramento sem agente para as métricas. Esse
processo, que também é chamado de crawler, coleta constantemente as seguintes métricas de todos os contêineres
por padrão:

* CPU
* Memória
* Informações de rede

Dados de métrica são coletados no Graphite e exibidos na IU do
{{site.data.keyword.Bluemix_notm}} e no Grafana. 

É possível ativar o Grafana na IU do {{site.data.keyword.Bluemix_notm}} ou diretamente de um
navegador. Para obter mais informações, consulte
[Analisando métricas
no Grafana](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

As informações de
convenções do Docker e de contabilidade de grupos são usadas como o mecanismo básico para a coleção de dados
de monitoramento.

**Retenção de métricas**

Até um ponto de dados por minuto é coletado. As métricas do contêiner que não foram gravadas em sete dias são excluídas.
    
**Classificação de métricas**

Os dados são exibidos e ordenados pelo ID do contêiner. 

Na linha de comandos, é possível executar o comando `cf ic ps` para visualizar
uma lista dos IDs de contêiner para os contêineres no registro de
imagens privadas do {{site.data.keyword.Bluemix_notm}}.

