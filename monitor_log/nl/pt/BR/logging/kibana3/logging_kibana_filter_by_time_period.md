---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrando seus logs do app Cloud Foundry por horário no Kibana
{: #logging_kibana_time_filter}


Visualize e filtre os logs do aplicativo {{site.data.keyword.Bluemix_notm}} por horário no painel do Kibana. É possível acessar o painel do Kibana na guia **Logs** para seu app Cloud Foundry. 
{:shortdesc}

Conclua as tarefas a seguir para visualizar e filtrar seus logs do app Cloud Foundry por horário no painel do Kibana:

1. Acesse a guia **Logs** de seu app Cloud Foundry. 

    1. Clique no nome do app no painel **Apps** do {{site.data.keyword.Bluemix_notm}}.
    2. Clique na guia **Logs**. 
    
    Os logs para seu app são exibidos.

2. Acesse o painel do Kibana para seu app. Clique em **Visualização avançada** ![Link da visualização avançada](images/logging_advanced_view.jpg "Link da visualização avançada"). O painel do Kibana é exibido.


3. No painel do Kibana, clique no **Filtro de tempo**; ![Filtro de tempo do Kibana](images/logging_kibana_time_filter.jpg "Filtro de tempo do Kibana"), em seguida, selecione **Customizado** no menu suspenso. A janela a seguir é exibida:

    ![Filtro de tempo customizado no painel do Kibana](images/logging_custom_time_filter.jpg "Filtro de tempo customizado no painel do Kibana")

4. Clique nos campos **De** e **Até** para editar o horário de início e encerramento de seu filtro. 
    
    Para incluir logs no presente momento, clique no link **agora**. 
    Quando estiver satisfeito com seu intervalo de horário, clique em **Aplicar**. 

O painel do Kibana agora exibe eventos registrados para seu filtro de tempo customizado.
