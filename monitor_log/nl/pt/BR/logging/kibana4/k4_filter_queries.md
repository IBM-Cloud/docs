---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando logs definindo consultas de procura customizadas
{:#k4_filter_queries}

Na barra de procura da página Descobrir, é possível definir e salvar consultas de procura usando a
linguagem de consulta Lucene. Para cada procura, é possível aplicar filtros para refinar as
entradas que estiverem disponíveis para análise. {:shortdesc}

Conclua as tarefas a seguir para filtrar seus logs usando uma procura customizada:

1. Acesse a guia **Logs** de seu app ou contêiner Cloud Foundry (CF). 

    1. Clique no nome ou no contêiner do app no painel do {{site.data.keyword.Bluemix}}.
    2. Para aplicativos CF, clique na guia **Logs**. Para contêineres, clique em
**Monitoramento e logs** e, em seguida, selecione a guia **Criação de
log**.
    
    Os logs são exibidos.

2. Acesse o Kibana. Clique em **Visualização avançada**
![Link de Visualização avançada](images/logging_advanced_view.jpg). O painel do Kibana é exibido.

    Ao acessar o Kibana, a procura padrão é aplicada. É possível ver os logs para a lista de instâncias
do recurso para o qual você ativou o Kibana. É possível filtrar os logs para quaisquer ou todos os
recursos do {{site.data.keyword.Bluemix_notm}} nesse espaço.

Em vez de "keyword", o termo correto é "term" para Lucene.

3. Consulte a página Descobrir para ver qual subconjunto de seus dados é exibido. Para obter mais
informações, consulte
[Identificando os dados que são
exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).Em seguida, modifique a consulta padrão para
filtrar entradas.

    **Nota:** use a linguagem de consulta Lucene para definir sua consulta
customizada. Para obter mais informações, consulte o
[Apache Lucene - Sintaxe do
analisador sintático de consulta![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    Quando o Kibana é ativado por meio do {{site.data.keyword.Bluemix_notm}}, para modificar a
consulta e definir múltiplos critérios de procura, é possível usar os termos lógicos **AND**
e **OR**. Esses operadores devem estar em maiúsculas.    
    
    * Para procurar por uma palavra-chave ou parte de uma palavra-chave, insira uma palavra, seguida por um símbolo curinga \*; por exemplo, `Java*`. 
    * Para procurar por uma frase específica, insira essa frase entre aspas duplas; por exemplo, `"Java/1.8.0"`.
    * Para criar procuras mais complexas, é possível usar os termos lógicos AND e OR; por exemplo, `"Java/1.8.0" OR "Java/1.7.0"`.
    * Para procurar por um valor em um campo específico, insira sua procura no formato a seguir:
*log_field_name:search_term*; por exemplo, `instance_id:"1"`.
    * Para procurar por um intervalo de valores para um campo de log específico, insira sua procura no
formato a seguir: *log_field_name:[start_of_range TO end_of_range]*; por exemplo,
`instance_id:["1" TO "2"]`.

     Por exemplo, para um app CF, é possível criar uma consulta
`application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` que
liste somente as entradas para as instâncias *0* e *1*. 

4. Salve a consulta para poder reutilizá-la posteriormente. Para obter mais informações, consulte
[Salvando uma procura](logging_kibana_filtering_logs.html#k4_save_search). 

**Nota:** se precisar excluir uma consulta, consulte
[Excluindo uma procura](logging_kibana_filtering_logs.html#k4_delete_search).



