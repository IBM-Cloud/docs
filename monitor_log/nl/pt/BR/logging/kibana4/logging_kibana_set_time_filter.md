---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Configurando um filtro de tempo
{: #set_time_filter}

Visualize e filtre logs do {{site.data.keyword.Bluemix}} dentro de um período de tempo
configurando o *Selecionador de tempo*.{:shortdesc}

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



