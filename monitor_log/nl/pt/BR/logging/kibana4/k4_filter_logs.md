---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando logs no Kibana
{:#k4_filter_logs}

Na página Descobrir, é possível criar consultas de procura e aplicar filtros para restringir as
informações que são exibidas para análise.
{:shortdesc}

* É possível definir uma ou mais consultas de procura na barra de procura da página Descobrir. Uma
consulta de procura define um subconjunto de entradas de log. Use a linguagem de consulta Lucene para definir
uma consulta de procura. 

* É possível incluir filtros da *Lista de campos* ou de entradas de tabela. Um filtro define a seleção de dados incluindo ou excluindo informações. É possível ativar ou desativar um filtro, inverter a ação do filtro, ativar ou desativar o filtro ou
removê-lo completamente. 

Depois de definir uma nova procura, salve-a para que ela possa ser reutilizada para análise futura na
página Descobrir ou para criar visualizações que possam ser usadas em painéis customizados. Para obter mais informações, consulte
[Salvando uma procura](logging_kibana_filtering_logs.html#k4_save_search).

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
 
* É possível filtrar seus logs para mostrar entradas em um período de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](logging_kibana_set_time_filter.html#set_time_filter).
     

## Incluindo um filtro para um valor que não esteja relacionado na *Lista de campos*
{:#k4_add_filter_out_value}

Para incluir um filtro para um valor que não é mostrado na *Lista de campos*, procure
por registros que incluam esse valor por meio de uma consulta. Em seguida, inclua o filtro na entrada de
tabela que está disponível na página Descobrir. 

Conclua as etapas a seguir para incluir um filtro para um valor que não está disponível na lista mostrada
na seção *Lista de campos*:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

    Por exemplo, a figura a seguir mostra os valores de instâncias para um app CF na *Lista
de campos*. 
    
    ![Mostrar valores
na lista de Campos](images/k4_add_filter_f1.jpg "Mostrar valores na lista de Campos")
    
    Você está interessado na instância de número *3*, mas ela não está disponível na
lista que pode ser vista.

2. Na página Descobrir, modifique a consulta para procurar por um valor de campo específico.

    Por exemplo, para procurar pela instância *3*, a consulta que você insere é a seguinte:
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Modificar consulta](images/k4_add_filter_f2.jpg "Modificar consulta")
    
    Na tabela, é possível ver quaisquer registros que corresponderem à sua consulta. 
    
 3. Expanda um registro e selecione o botão de lupa
![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupano modo inclusivo") para incluir um filtro.

 
     Por exemplo, para incluir um filtro no ID da instância com o valor *3*, clique
no botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupano modo inclusivo") no campo *instance_id*.

     
     ![Mostrar tabela](images/k4_add_filter_f3.jpg "Mostrar tabela")
     
4. Verifique se o filtro foi incluído.

    Por exemplo, a figura a seguir mostra o filtro ativado após ele ser incluído por meio da tabela.
    
    ![Mostrar filtro](images/k4_add_filter_f4.jpg "Mostrar filtro")
    
    


## Filtrando seus logs para um valor de campo específico
{:#k4_filter_logs_spec_field}

É possível procurar por entradas que incluam um valor de campo específico. 

Conclua as etapas a seguir para procurar por entradas que incluem um valor de campo específico:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, identifique o campo para o qual deseja definir um filtro e clique nele.

    Um máximo de 5 valores é mostrado para o campo. Cada valor possui dois botões de lupa. 
    
    Se você não conseguir ver o valor, consulte [Incluindo um filtro para um valor que não estiver relacionado na lista Campos](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. Para incluir um filtro que procure por entradas com um valor de campo, escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modo inclusivo") para esse valor.

    ![Filtro que inclui o valor de campo](images/k4_add_filter_for_field.jpg "Filtro que inclui o valor de campo")

    Para incluir um filtro que procure por entradas que não incluam esse valor de campo, escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modo inclusivo") para o valor.

    ![Filtro que exclui o valor de campo](images/k4_add_filter_to_exclude_field.jpg "Filtro que exclui o valor de campo")

4. Escolha qualquer uma das seguintes opções para trabalhar com filtros no Kibana:

    <table>
      <caption>Tabela 1. Métodos para trabalhar com filtros</caption>
      <tbody>
        <tr>
          <th align="center">Opção</th>
          <th align="center">Descrição</th>
          <th align="center">Outras informações</th>
        </tr>
        <tr>
          <td align="left">Ativar</td>
          <td align="left">Selecione essa opção para ativar um filtro.</td>
          <td align="left">Ao incluir um filtro, ele é ativado automaticamente. <br> Se um filtro estiver desativado, clique nele para ativá-lo.</td>
        </tr>
        <tr>
          <td align="left">Disable</td>
          <td align="left">Selecione essa opção para desativar um filtro.</td>
          <td align="left">Depois de incluir um filtro, se desejar ocultar entradas para um valor de campo, clique em **desativar**.</td>
        </tr>
        <tr>
          <td align="left">Alfinete</td>
          <td align="left">Selecione essa opção para persistir o filtro nas páginas do Kibana.</td>
          <td align="left">É possível fixar um filtro na página *Descobrir*, na página *Visualizar* ou na página *Painel*.</td>
        </tr>
        <tr>
          <td align="left">Comutar</td>
          <td align="left">Selecione essa opção para alternar um filtro.</td>
          <td align="left">Por padrão, as entradas que correspondem a um filtro são exibidas. Para exibir entradas que não correspondem, alterne o filtro.</td>
        </tr>
        <tr>
          <td align="left">Remover</td>
          <td align="left">Selecione essa opção para remover um filtro.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

## Filtrando seus logs do app CF por origem
{:#k4_filter_logs_by_source}

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


## Filtrando seus logs por tipo de log
{:#k4_filter_logs_by_log_type}

Conclua as etapas a seguir para procurar por entradas que incluam um tipo de log específico:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, selecione o campo **tipo**.

    Por exemplo, na figura a seguir, somente um tipo de log está disponível: *syslog*
    
    ![Lista de filtro que mostra o tipo de log de campo](images/k4_filter_log_type_F1.jpg "Lista de filtro que mostra o tipo de log decampo")

   
3. Para incluir um filtro que procura por um tipo de log específico, escolha o botão de lupa
![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa nomodo inclusivo") para o tipo de log que deseja analisar.


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



## Filtrando seus logs por ID da instância
{:#k4_filter_logs_by_instance_id}

Conclua as etapas a seguir para visualizar e filtrar seus logs por ID da instância no painel do Kibana:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, selecione um dos campos a seguir para procurar por um ID da instância específico:

    * **instance_ID**: esse campo lista os IDs de instância diferentes que estão
disponíveis no log para um aplicativo Cloud Foundry. 
    * **instance**: esse campo lista os GUIDs diferentes de todas as instâncias
para um grupo de contêiner. 

    Por exemplo, a figura a seguir mostra valores diferentes de instâncias para um app CF:
    
    ![Lista de filtro que mostra o campo instance_id](images/k4_filter_instanceid_f1.jpg "Lista de filtro que mostra ocampo instance_id")

   
3. Para incluir um filtro que procura por um tipo de log específico, escolha o botão de lupa
![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa nomodo inclusivo") para o tipo de log que deseja analisar.


   Por exemplo, para incluir um filtro que inclua entradas para a instância do app CF *2*,
selecione o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa nomodo inclusivo") que está disponível para o valor *2* na

seção Lista de campos. A figura a seguir mostra o filtro que inclui entradas para a instância *2*.
    
    ![Filtro que inclui entradas de instance_id para a instância 2](images/k4_filter_instanceid_f2.jpg "Filtro que inclui entradas de instance_idpara a instância 2")


    Para incluir um filtro que procure por entradas que não incluam um ID da instância específico,
escolha o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modoexclusivo") para o valor.


     Por exemplo, para incluir um filtro que exclua entradas para a instância do app CF
*2*, selecione o botão de lupa ![Botão de lupa no modo exclusivo](images/k4_exclude_field_icon.jpg "Botão de lupano modo exclusivo") que está disponível para o valor *2*

na seção Lista de campos. A figura a seguir mostra o filtro que exclua entradas para a instância
*2*.
     
      ![Filtro que exclui entradas de instance_id para a instância 2](images/k4_filter_instanceid_f3.jpg "Filtro que exclui entradas de instance_idpara a instância 2")



## Filtrando seus logs do app CF por tipo de mensagem
{:#k4_filter_cf_logs_by_msg_type}

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


## Filtrando seus logs para um texto específico em um valor de campo
{:#k4_filter_logs_spec_text}

Visualize e procure por entradas que incluam um texto específico no valor de um campo. 

**Aviso:** é possível fazer uma procura de texto livre somente de campos de sequência
que forem analisados pelo analisador Elasticsearch. 
    
Quando o Elasticsearch analisa o valor de um campo de sequência, ele divide o texto em limites de
palavras, conforme definido pelo Consórcio de Unicode, remove a pontuação e coloca todas as
palavras em letras minúsculas.
    
Conclua as etapas a seguir para procurar por entradas que incluam texto específico em um valor de campo:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para
obter mais informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Identifique os campos que são analisados no ElasticSearch por padrão.

    Para exibir a lista completa de campos analisados que estão disponíveis para procura e filtragem
de dados de log,
[recarregue a
lista de campos](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields). Em seguida, na Lista de campos que está disponível na página Descobrir,
conclua as etapas a seguir:
    
    1. Clique no ícone de configuração ![ícone Configurar](images/k4_configure_icon.jpg "ícone deconfiguração"). A seção **Campos selecionados**, na qual é possível

filtrar campos, é exibida.

        ![Seção de configuração para mostrar campos com atributos específicos](images/k4_reset_filters.jpg "Seção de configuração para mostrar campos comatributos específicos")

    
    2. Para identificar os campos que estiverem analisados, selecione **Sim** para o
campo de procura **Analisados**.

        ![Atributo
analisado](images/k4_reset_filters_analyze_options.jpg "Atributo analisado")
    
        A lista de campos analisados é mostrada.
    
        ![Lista de
campos analisados](images/k4_list_analyzed_fields.jpg "Lista de campos analisados")
        
         
    3. Verifique se o campo no qual deseja procurar por texto livre é um campo que é analisado pelo
ElasticSearch por padrão.
    
3. Se o campo for analisado, modifique a consulta para procurar por entradas nos logs que incluam esse
texto livre como parte do valor de um campo.

    
**Exemplo**

Se você ativar o Kibana para um aplicativo Cloud Foundry (CF) na IU do
{{site.data.keyword.Bluemix}} e desejar procurar por uma mensagem específica que inclua o ID de
mensagem *CWWKT0016I:*, modifique a procura para incluir o texto livre.
    
1. Verifique a consulta de procura que é carregada e os dados que são exibidos na página Descobrir.
       
    ![Consulta
de procura padrão](images/k4_filter_by_text_default_query.jpg "Consulta de procura padrão")
        
2. Para procurar pelo ID de mensagem *CWWKT0016I*, modifique a consulta de procura e
pressione **Enter**:
    
    <pre class="pre">application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" </pre>
        
    ![Modificar a
consulta](images/k4_filter_by_text_modify_query.jpg "Modificar a consulta")
      
A tabela mostra as entradas para seu app CF no qual o texto *CWWKT0016I* faz parte do valor
no campo *mensagem*.
    
![Nova
visualização de procura](images/k4_filter_by_text_result_query.jpg "nova visualização de procura") 	
        

## Configurando um filtro de tempo
{: #set_time_filter}

Visualize e filtre logs do {{site.data.keyword.Bluemix_notm}} dentro de um período de tempo
configurando o *Selecionador de tempo*.

É possível configurar o *Selecionador de tempo* na página Descobrir. Por padrão, ele é
configurado para os últimos 15 minutos. 

Conclua as etapas a seguir para procurar por entradas que incluam um tempo específico:

1. Na barra de menus da página Descobrir, clique no Selecionador de tempo
![Selecionador de tempo](images/k4_time_picker_icon.jpg "Selecionador de tempo").

2. Configure o intervalo de tempo. 

    É possível definir qualquer um dos seguintes tipos de intervalos de tempo:
    
    * Rápido: estes são os intervalos de tempo predefinidos que incluem os usos mais comuns de
intervalos de tempo Relativo e Absoluto, por exemplo, *Hoje* e *Este mês*. 
    
        ![Opções rápidas de Selecionador de Tempo](images/k4_time_picker_quick.jpg "Opções rápidas de Selecionador deTempo")

    
    * Relativo: estes são os intervalos de tempo em que é possível especificar a data e hora de início
e a data e hora de encerramento. É possível arredondar por hora.
    
        ![Opções relativas de Selecionador de Tempo](images/k4_time_picker_relative.jpg "Opções relativas de Selecionador deTempo")

    
    * Absoluto: estes são os intervalos de tempo entre uma data de início e uma data de encerramento.
    
        ![Opções absolutas de Selecionador de Tempo](images/k4_time_picker_absolute.jpg "Opções absolutas de Selecionador deTempo")

      

Depois de configurar um intervalo de tempo, os dados mostrados no Kibana corresponderão às entradas dentro
desse intervalo de tempo.








