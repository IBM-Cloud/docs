---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Filtrando seus logs do app Cloud Foundry por tipo de log no Kibana
{: #logging_kibana_component_filter}

Visualize e filtre os logs do aplicativo {{site.data.keyword.Bluemix_notm}} por componente (tipo de log) no painel do Kibana. É possível acessar o painel do Kibana na guia **Logs** para seu app Cloud Foundry. 
{:shortdesc}

Conclua as tarefas a seguir para visualizar e filtrar seus logs do app Cloud Foundry por tipo de log no painel do Kibana:

1. Acesse a guia **Logs** de seu app Cloud Foundry. 

    1. Clique no nome do app no painel **Apps** do {{site.data.keyword.Bluemix_notm}}.
    2. Clique na guia **Logs**. 
    
    Os logs para seu app são exibidos.

2. Acesse o painel do Kibana para seu app. Clique em **Visualização avançada** ![Link da visualização avançada](images/logging_advanced_view.jpg "Link da visualização avançada"). O painel do Kibana é exibido.

3. Na janela **TODOS OS EVENTOS**, clique no ícone de seta à direita para mostrar todos os campos. 

    ![Janela Todos os eventos com ícone de seta à direita](images/logging_all_events_no_fields.jpg "Janela Todos os eventos com ícone de seta à direita")

4. Na área de janela **Campos**, selecione **source_id** para exibir o componente que gerou cada entrada de log na janela **TODOS OS EVENTOS**.

    ![Janela Todos os eventos com o campo source_id selecionado](images/logging_component.png "Janela Todos os eventos com o campo source_id selecionado")

5. Na janela **TODOS OS EVENTOS**, clique em uma linha de evento de log para exibir os detalhes para esse evento. Escolha um evento que exiba o source_id que você deseja filtrar.

    ![Janela Todos os eventos exibindo detalhes para um evento de log selecionado](images/logging_component_add_filter.png "Janela Todos os eventos exibindo detalhes para um evento de log selecionado")

6. Inclua um filtro para incluir ou excluir informações para um componente (tipo de log). 

    * Para incluir um filtro que inclua um valor de componente, clique no ícone de **Lupa** ![Ícone de lupa](images/logging_magnifying_glass.jpg "Ícone de lupa") na linha source_id da tabela. 

        ![Condição do filtro para o campo source_id](images/logging_component_filter.png "Condição do filtro para o campo source_id") 

    * Para incluir um filtro que exclua um valor de componente, clique no ícone de **Exclusão** ![Ícone de exclusão](images/logging_exclusion_icon.png "Ícone de exclusão") na linha source_id da tabela. 
    
         ![Condição do filtro para excluir o campo source_id](images/logging_component_add_exclusion_filter.png "Condição do filtro para excluir o campo source_id") 
     
     Uma nova condição do filtro é incluída no painel do Kibana.

7. Opcionalmente, é possível repetir a etapa anterior e incluir filtros para cada componente. Para ver a lista integral de componentes, veja [Formato de log](../logging_view_kibana3.html#kibana_log_format_cf).

    A imagem a seguir mostra o painel com múltiplos filtros para componentes diferentes:
    
    ![Múltiplas condições do filtro para o campo source_id](images/logging_component_multiple_filters.png "Múltiplas condições do filtro para o campo source_id")

8. Salve o painel. 

    Quando concluir a inclusão de filtros e a customização do painel, clique no ícone **Salvar** ![Ícone Salvar](images/logging_save.jpg "Ícone Salvar") e insira um nome para seu painel. 
      
    **Nota:** se você tentar salvar um painel com um nome contendo espaços em branco, ele não será salvo. Insira um nome sem espaços e clique no ícone **Salvar**.
    
    ![Salvar nome do painel](images/logging_save_dashboard.jpg "Salvar nome do painel")

Você criou um painel que filtra suas entradas de log por componente (tipo de log). É possível carregar seu painel salvo a qualquer momento clicando no ícone **Pasta** ![Ícone Pasta](images/logging_folder.jpg "Ícone Pasta") e selecionando seu painel por nome.


