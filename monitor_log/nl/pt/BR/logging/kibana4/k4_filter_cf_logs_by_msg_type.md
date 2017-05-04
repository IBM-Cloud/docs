---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando seus logs do app CF por tipo de mensagem 
{:#k4_filter_cf_logs_by_msg_type}

É possível visualizar e filtrar logs do Cloud Foundry por tipo de mensagem no Kibana{:shortdesc}


Conclua as etapas a seguir para procurar por entradas que incluam um tipo de mensagem específico:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, selecione o campo **message_type**.

    A figura a seguir mostra os valores localizados para o campo *message_type* nos logs
de um app CF:
    
    ![Lista de filtro que mostra o campo message_type](images/k4_filter_by_msg_type_f1.jpg "Lista de filtro que mostra omessage_type")     


3. Para incluir um filtro que procure por entradas que incluam um *message_type*
específico, escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupano modo inclusivo") para esse valor.


    Por exemplo, para incluir um filtro que inclua entradas de log que possuam um valor de
*OUT* de message_type, selecione o botão de lupa
![Botão de lupa no
modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modo inclusive") que está disponível para o valor de OUT na seção Lista de
campos*. A figura a seguir mostra o filtro para o valor de *OUT* de message_type ativado.
    
    ![Filtro
que inclui o valor de campo](images/k4_filter_by_msg_type_f2.jpg "Filtro que inclui o valor de campo")

    Para incluir um filtro que procure por entradas que não incluam um *message_type*
específico, escolha o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modoexclusivo") para o valor.

    
    Por exemplo, para incluir um filtro que exclua entradas de log para o *OUT* de message_type, selecione o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa nomodo inclusivo") que está disponível para o valor

*CELL* na seção *Lista de campos*. A figura a seguir mostra o filtro que exclui
entradas para o valor de *OUT* de message_type.

    ![Filtro
que exclui o valor de campo](images/k4_filter_by_msg_type_f3.jpg "Filtro que exclui o valor de campo")

