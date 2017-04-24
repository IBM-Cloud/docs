---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Criação de log para o IBM Bluemix Container Service
{: #logging_containers_ov}

No {{site.data.keyword.Bluemix}}, é possível visualizar, filtrar e analisar logs do contêiner por
meio do painel do {{site.data.keyword.Bluemix_notm}}, do Kibana e da interface da linha de comandos. {:shortdesc}

Os logs do contêiner são monitorados e encaminhados de fora do contêiner usando crawlers. Os dados são
enviados pelos crawlers para um Elasticsearch de diversos locatários no
{{site.data.keyword.Bluemix_notm}}.

A figura a seguir mostra uma visualização de alto nível de criação de log para o
{{site.data.keyword.containershort}}:

![Visão geral do componente de alto nível para contêineres](images/logging_containers_ov.jpg "Visão geral do componente de alto nível paracontêineres")


A criação de log de contêineres é ativada automaticamente quando você implementa esse contêiner
no {{site.data.keyword.Bluemix_notm}}.

## Logs coletados para contêineres
{: #logging_containers_ov_logs_collected}

Por padrão, os logs a seguir são coletados:

<table>
  <tbody>
    <tr>
      <th align="center">Registro</th>
      <th align="center">Descrição</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> Por padrão, as mensagens do Docker são armazenadas na pasta
/var/log/messages do contêiner. Esse log inclui mensagens do sistema.</td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Este é o log do Docker.<br> O arquivo de log do Docker não é armazenado como um arquivo dentro do contêiner, mas é coletado de qualquer maneira. 
Esse arquivo de log é coletado por padrão, pois ele é a convenção do Docker padrão para expor as informações
de stdout (saída padrão) e stderr (erro padrão) para o contêiner. Se algum processo do contêiner for impresso
como stdout ou stderr, estas informações serão coletadas.</td>
     </tr>
  </tbody>
</table>

Para coletar logs adicionais, inclua a variável de ambiente **LOG_LOCATIONS**
com um caminho para o arquivo de log ao criar o contêiner. É possível incluir múltiplos arquivos de log
separando-os com vírgulas. Para obter mais informações, consulte
[Coletando dados de log não
padrão de um contêiner](logging_containers_other_logs.html#logging_containers_collect_data).


## Métodos para analisar os logs do contêiner
{: #logging_containers_ov_methods}
 
É possível escolher qualquer um dos métodos a seguir para analisar os logs de seu contêiner:

* Analise o log no {{site.data.keyword.Bluemix_notm}} para visualizar a atividade mais recente
do contêiner.
    
    É possível visualizar, filtrar e analisar logs por
meio da guia **Monitoramento e logs** que está disponível para cada contêiner.
Para obter mais informações, consulte [Analisando
logs no painel do Bluemix](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analise os logs no Kibana para executar tarefas analíticas avançadas.
    
    É possível usar o Kibana, uma plataforma de software livre para análise de dados e
visualização, para monitorar, procurar, analisar e visualizar seus dados em uma variedade de
gráficos, por exemplo, diagramas e tabelas. Para obter mais informações, veja [Analisando logs no Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analise os logs por meio da CLI para usar comandos para gerenciar logs programaticamente.
    
    É possível visualizar, filtrar e analisar logs por meio da interface da linha de comandos usando o
comando **cf ic logs**. Para obter mais informações, consulte
[Analisando logs na interface da
linha de comandos](../logging_view_cli.html#analyzing_logs_cli).


## Retenção de log
{: #logging_containers_ov_log_retention}

Considere as informações a seguir sobre retenção de log. 

* No máximo 1 GB por espaço de dados é armazenado por dia. Qualquer log além
desse valor máximo de 1 GB é descartado. As dotações de limite são reconfiguradas diariamente às 0h30 UTC. 

    É possível aumentar o limite entrando em contato com o suporte. No chamado de suporte, inclua seu
ID de espaço para a solicitação de aumento de limite, o novo tamanho de limite e o motivo para a solicitação.

* É
possível procurar até 7 GB de dados por um máximo de 7 dias. Os dados do log são substituídos (Primeiro a entrar, primeiro a sair) após 7 GB de dados serem alcançados ou 7 dias.

