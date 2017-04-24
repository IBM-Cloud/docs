---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Incluindo um filtro para um valor que não esteja relacionado na *Lista de campos*
{:#k4_add_filter_out_value}

Para incluir um filtro para um valor que não é mostrado na *Lista de campos*, procure
por registros que incluam esse valor por meio de uma consulta. Em seguida, inclua o filtro na entrada de
tabela que está disponível na página Descobrir.{:shortdesc}

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
    
    
