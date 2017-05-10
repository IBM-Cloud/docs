---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# FAQ do Kibana
{: #logging_qa_kibana}

A seguir estão as respostas para perguntas comuns sobre como usar os recursos de criação de log
do {{site.data.keyword.Bluemix}}. {:shortdesc}

* [O que poderei fazer se eu não conseguir ver
os dados na página Descobrir no Kibana?](logging_qa_kibana.html#logging_qa_no_data_discover_kibana)

* [O que poderei fazer se eu receber uma
exceção de autenticação?](logging_qa_kibana.html#logging_qa_no_data_dashboard_kibana)


## O que poderei fazer se eu não conseguir ver os dados na página Descobrir no Kibana?
{: #logging_qa_no_data_discover_kibana}

Há diferentes cenários em que você talvez não consiga ver dados no Kibana:

1. Ao ativar o Kibana, talvez você não consiga ver nenhum dado na página Descobrir. Você recebe a
seguinte mensagem: **Nenhum resultado localizado.**. 
2. Talvez você esteja trabalhando na página Descobrir no Kibana. No entanto, após um curto período
de tempo, você receberá a mensagem **Nenhum resultado localizado.** ao tentar
executar uma tarefa no Kibana.

Para resolver este problema,
conclua as seguintes etapas:

1. Verifique o *Selecionador de Tempo* que está configurado na página Descobrir e
aumente o período de tempo. 

    **Nota**: por padrão, no {{site.data.keyword.Bluemix_notm}}, o
*Selecionador de Tempo* é configurado para mostrar dados dos últimos 15 minutos.

    Para obter mais informações sobre como configurar o *Selecionador de Tempo*, consulte
[Configurando um filtro de
tempo](../kibana4/k4_filter_logs.html#set_time_filter).
       
2. Clique na lupa que está localizada na barra de procura da página *Descobrir*. Os dados da página são atualizados com base na consulta de procura padrão.

    Como alternativa, é possível configurar um período de *Atualização automática*.

    **Nota**: por padrão, no {{site.data.keyword.Bluemix_notm}}, o
período de *Atualização automática* é configurado como **OFF**.
    
    Para obter mais informações sobre como ativá-lo, consulte
[Atualizando
os dados automaticamente](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval).



## O que poderei fazer se eu receber uma
exceção de autenticação?
{: #logging_qa_no_data_dashboard_kibana}

Quando não for possível ver dados exibidos em suas visualizações em uma página Painel e você receber a
mensagem de erro **Erro: Exceção de autorização.**, verifique suas permissões para ver os dados em
cada visualização.

Considere as seguintes informações: é possível configurar uma ou mais visualizações em uma página Painel. Quando a página Painel faz uma solicitação para reunir os dados que são exibidos por essas visualizações,
somente uma solicitação é emitida para todas as visualizações. Se você não tiver permissões para ver os dados
em uma das visualizações, a solicitação inteira falhará.

Para resolver este problema,
conclua as seguintes etapas:

1. Identifique as visualizações para as quais você não tem permissões.

    1. Clique no ícone de *lápis* de uma visualização na página *Painel*. A
visualização se abre na página *Visualizar*. Como alternativa, na página
*Visualizar*, carregue uma visualização. 
    2. Verifique se é possível ver os dados.
    
    Repita estas etapas para cada visualização.

2. Solicite acesso para ver dados nessas visualizações no seu administrador em nuvem.

3. Crie uma nova página Painel que exclua as visualizações para as quais você não tem permissões enquanto
recebe acesso para ver dados nas visualizações que estiverem causando o problema. 

    Se você compartilhar o Painel, não exclua as visualizações, já que isso afetará outros membros da
equipe que usam o mesmo painel.


