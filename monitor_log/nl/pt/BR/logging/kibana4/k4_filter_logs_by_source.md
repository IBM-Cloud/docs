---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando seus logs do app CF por origem
{:#k4_filter_logs_by_source}

Visualize e filtre por logs de aplicativo Cloud Foundry de tipo de origem por meio do painel do
Kibana.{:shortdesc}

Conclua as etapas a seguir para procurar por entradas que incluam uma origem de log específica:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, selecione o campo **source_id**.

    ![Lista de filtro que mostra o campo source_id](images/k4_filter_sourceid_F1.jpg "Lista de filtro que mostra o camposource_id")     


3. Para incluir um filtro que procure por entradas que incluam um source_id específico,
escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modoinclusivo") para esse valor.


    Para obter uma lista de origens de log que estão disponíveis para apps CF, consulte
[Origens de log para apps CF](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources).

    Por exemplo, para incluir um filtro que inclua entradas de log sobre o início, parada ou
travamento de um aplicativo CF, selecione o botão de lupa
![Botão de lupa no
modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modo inclusivo") que está disponível para o valor CELL na seção Lista de
campos*. A figura a seguir mostra o filtro para o valor *CELL* de source_id ativado.
    
    ![Filtro que
inclui o valor de campo](images/k4_filter_sourceid_F2.jpg "Filtro que inclui o valor de campo")

    Para incluir um filtro que procure por entradas que não incluam um source_id
específico, escolha o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modoexclusivo") para o valor.

    
    Por exemplo, para incluir um filtro que exclua entradas de log sobre o início, parada ou
travamento de um aplicativo CF, selecione o botão de lupa
![Botão de lupa no modo
inclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modo inclusivo") que está disponível para o valor CELL na seção Lista de
campos*. A figura a seguir mostra o filtro que exclui entradas para o valor *CELL* de
source_id.

    ![Filtro que
exclui o valor de campo](images/k4_filter_sourceid_F3.jpg "Filtro que exclui o valor de campo")




