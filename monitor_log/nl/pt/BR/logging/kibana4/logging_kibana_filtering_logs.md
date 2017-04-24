---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando logs no Kibana
{:#kibana_filtering_logs}

Na página Descobrir, é possível criar consultas de procura e aplicar filtros para restringir as
informações que são exibidas para análise.{:shortdesc}

* É possível definir uma ou mais consultas de procura na barra de procura da página Descobrir. Uma
consulta de procura define um subconjunto de entradas de log.  Use a linguagem de consulta Lucene para definir
uma consulta de procura. 

* É possível incluir filtros da *Lista de campos* ou de entradas de tabela. Um filtro define a seleção de dados incluindo ou excluindo informações. 
É possível ativar ou desativar um filtro, inverter a ação do filtro, ativar ou desativar o filtro ou
removê-lo completamente. 

Depois de definir uma nova procura, salve-a para que ela possa ser reutilizada para análise futura na
página Descobrir ou para criar visualizações que possam ser usadas em painéis customizados. Para obter mais
informações, consulte [Salvando uma procura](logging_kibana_filtering_logs.html#k4_save_search).

Ao executar uma nova procura, o histograma, a tabela e a lista de Campos são atualizados automaticamente
para mostrar os resultados da procura. Para descobrir quais dados são mostrados, consulte
[Identificando os dados que são exibidos na página Descobrir](k4_identify_data.html#k4_identify_data).

A lista a seguir descreve cenários de como filtrar dados em seus logs:

* É possível criar procuras customizadas para filtrar seus logs. Para obter mais informações, consulte
[Filtrando logs definindo consultas customizadas](k4_filter_queries.html#k4_filter_queries). 

* É possível procurar no log por entradas que incluem um texto específico no valor de um campo. Para
obter mais informações, consulte
[Filtrando seus logs para um texto
específico em um valor de campo](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* É possível procurar no log por um valor de campo específico ou excluir entradas do log para um valor
de campo específico. Para obter mais informações, consulte
[Filtrando seus logs para um
valor de campo específico](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * É possível filtrar seus logs por tipo de log. Para obter mais informações, consulte
[Filtrando seus logs por tipo de log ](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type). 
    * É possível filtrar seus logs do app CF por origem. Para obter mais informações, consulte
[Filtrando seus logs de app CF por origem](k4_filter_logs_by_source.html#k4_filter_logs_by_source). 
    * É possível filtrar seus logs por ID da instância. Para obter mais informações, consulte
[Filtrando seus logs por ID da instância](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).    
    * É possível filtrar seus logs por tipo de mensagem. Para obter mais informações, consulte
[Filtrando seus logs por ID de
tipo de mensagem](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type). 
 
* É possível filtrar seus logs para mostrar entradas em um período de tempo. Para obter mais
informações, consulte [Configurando um filtro
de tempo](logging_kibana_set_time_filter.html#set_time_filter).
     

## Iniciando uma nova procura
{: #k4_new_search}

Para iniciar uma nova procura, clique no botão **Nova procura**
![Nova Procura](images/k4_new_search_icon.jpg "Nova procura") na barra de
ferramentas da página Descobrir.

## Salvando uma Procura 
{: #k4_save_search}

Ao salvar uma procura, a sequência de consultas de procura e o padrão de
índice selecionado atualmente são salvos.

Conclua as etapas a seguir para salvar uma procura atual na página Descobrir:

1. Na barra de ferramentas da página Descobrir, clique no botão **Salvar procura**
![Salvar procura](images/k4_save_search_icon.jpg "Salvar procura").

2. Digite um nome para a pesquisa.

3. Clique em salvar. 

## Excluindo uma Procura
{: #k4_delete_search}

Para excluir uma procura, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Procuras**, selecione a procura que deseja excluir.

3. Clique em **Excluir**.


## Exportando uma procura
{: #k4_export_search}

Para exportar uma procura, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Procuras**, selecione a procura que deseja exportar.

3. Clique em **Exportar**. 

4. Salve o arquivo.

## Importando uma procura
{: #k4_import_search}

Para importar uma procura, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Procuras**, selecione **Importar**.

3. Selecione um arquivo e clique em **Abrir**.

A procura é incluída na lista de procuras.


## Recarregando uma procura
{: #k4_reload_search}

Conclua as etapas a seguir para carregar uma procura salva:

1. Na barra de ferramentas da página Descobrir, clique no botão **Carregar procura**
![Carregar procura](images/k4_load_icon.jpg "Carregar procura").

2. Selecione a procura que deseja carregar. 


## Atualizando o conteúdo de uma procura
{: #k4_refresh_search}

Para atualizar manualmente o conteúdo de uma procura, é possível clicar na lupa que está disponível na
barra de procura. 

Para atualizar automaticamente os dados que são mostrados na página Descobrir, é possível configurar um
intervalo de atualização. O valor atual do intervalo de atualização é exibido na barra de menus da página
Descobrir. Por padrão, a atualização automática é configurada como **OFF**.

Conclua as etapas a seguir para configurar um intervalo de atualização:

1. Na página Descobrir, clique no **Filtro de tempo** que está disponível na barra
de menus.

2. Clique em **Atualização automática**
![Atualização
automática](images/k4_auto_refresh_icon.jpg "Atualização automática").

3. Escolha um intervalo de atualização na lista. 

    ![Opções do intervalo de atualização](images/k4_change_autorefresh.jpg "Opções do intervalo deatualização")



**Nota**: depois de ativar um intervalo de atualização automática, é possível
pausá-lo clicando no botão de pausa ![Pausa](images/k4_auto_refresh_pause_icon.jpg "Pausa").




