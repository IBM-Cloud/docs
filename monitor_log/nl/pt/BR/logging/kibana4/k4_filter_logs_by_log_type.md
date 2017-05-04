---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando seus logs por tipo de log
{:#k4_filter_logs_by_log_type}

Visualize e filtre logs do {{site.data.keyword.Bluemix}} por tipo de log.
{:shortdesc}

Conclua as etapas a seguir para procurar por entradas que incluam um tipo de log específico:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, selecione o campo **tipo**.

    Por exemplo, na figura a seguir, somente um tipo de log está disponível: *syslog*
    
    ![Lista de filtro que mostra o tipo de log de campo](images/k4_filter_log_type_F1.jpg "Lista de filtro que mostra o tipo de log decampo")

   
3. Para incluir um filtro que procura por um tipo de log específico, escolha o botão de lupa
![Botão de lupa no modo
inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modo inclusivo") para o tipo de log que deseja analisar.

    Por exemplo, para incluir um filtro que inclua entradas de log para o *syslog*,
selecione o botão de lupa ![Botão de lupa em modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa em modoinclusivo") que está disponível para o valor de *syslog* na

seção *Lista de campos*. A figura a seguir mostra o filtro que inclui entradas para o tipo de log
*syslog*.

    ![Filtro que inclui entradas de tipo de log para o syslog](images/k4_filter_log_type_F2.jpg "Filtro que inclui entradas de tipo de log para o syslog")

    Para incluir um filtro que procura por entradas que não incluam um tipo de log específico, escolha
o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modo exclusivo") para o valor.


     Por exemplo, para incluir um filtro que exclua entradas de log para o *syslog*,
selecione o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modoexclusivo") que está disponível para o valor de *syslog*

na seção *Lista de campos*. A figura a seguir mostra o filtro que exclui entradas para o tipo de log
*syslog*.
     
     ![Filtro que exclui entradas de tipo de log para o syslog](images/k4_filter_log_type_F3.jpg "Filtro que exclui entradas de tipo de logpara o syslog")




