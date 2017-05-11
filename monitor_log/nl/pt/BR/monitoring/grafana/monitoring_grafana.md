---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Criando um painel do Grafana
{:#monitoring_grafana}

Crie um painel do Grafana customizado para exibir métricas para todos os contêineres que forem executados
em um espaço de sua organização do {{site.data.keyword.Bluemix}}.
{:shortdesc}

Conclua as etapas a seguir para criar um painel do Grafana:

1. Ative o Grafana em um navegador da web. Para obter mais informações, veja [Navegando para o painel do Grafana por meio de um navegador da web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).

2. Salve o painel padrão.

    1. Na barra de ferramentas, clique no ícone Salvar.
    2. Insira um nome para o painel.
    3. Ao lado do campo de nome, clique no ícone Salvar.
   
3. Desative a atualização de página automática enquanto trabalha no painel. 

    1. Clique no selecionador de horário no cabeçalho.
    2. Selecione **Atualização automática**.
    3. Clique em **Desativar**.
 
 5. Exclua as linhas de exemplo.
 
     1. Ao lado do cabeçalho *Bem-vindo ao Grafana*, passe o cursor sobre a
régua de controle do menu Linha e, em seguida, clique no ícone do menu Linha que desliza para fora.
     2. Clique em **Excluir linha** e, em seguida, clique em
**Sim**.
     
     Repita estas etapas para remover os Links de Documentação e as linhas do Primeiro Parágrafo. 
     
     No cabeçalho da página, ajuste o selecionador de tempo para assegurar-se de que possa ver dados. O valor padrão é de 6 horas até alguns segundos atrás. Selecione **Últimos 30 dias**.
     
6. Inclua uma visualização.

    * Para incluir uma visualização de CPU inativa, consulte
[Incluindo uma visualização de CPU inativa](monitoring_grafana.html#grafana_add_cpu).
    * Para incluir uma visualização de memória usada, consulte
[Incluindo uma visualização de memória usada](monitoring_grafana.html#grafana_add_mem).
        
7. Salve o painel customizado.

    1. Na barra de ferramentas, clique no ícone Salvar.
    2. Insira um nome para o painel.
    3. Ao lado do campo de nome, clique no ícone Salvar.
    

## Incluindo uma visualização de CPU inativa
{:#grafana_add_cpu}

Para incluir um gráfico de CPU inativa que inclua dados de todos os contêineres em seu espaço, conclua
as etapas a seguir:

1. Clique no botão **Incluir uma linha**. Uma régua de controle de menu Linha é
exibida no lado da linha.
    
2. Passe o cursor sobre a régua de controle do menu de linha e, em seguida, clique no ícone do menu
Linha que desliza para fora.

3. Clique em **Incluir painel**. Em seguida, clique em
**gráfico**.

4. Clique no título do gráfico para abrir o menu do painel e clique em **Editar**. 

    O restante do painel fica oculto; apenas o editor desse gráfico e uma visualização do gráfico
são exibidos.
    
5. Na guia Métricas, construa uma consulta para coletar dados para o gráfico. 

    Por exemplo, quando você trabalha com contêineres, o formato da consulta inclui o ID do espaço,
um ID do grupo de contêiner e um ID da instância de contêiner única no formato a seguir:
`space_ID.group_ID.instance_ID.metric`
        
    1. Na linha A, clique em **Selecionar métrica**. Em seguida, selecione seu ID de
espaço.
    2. Clique em **Selecionar métrica** e selecione o asterisco (\*).
    
    Ao selecionar (\*), os dados incluem métricas de cada grupo de contêiner no espaço. Opcionalmente, é possível
manipular esse formato com uma expressão regular para incluir métricas apenas de certos contêineres. Por
exemplo, se desejar ver métricas apenas de contêineres únicos e excluir grupos de contêineres, clique em
**Selecionar métrica** e selecione **0000**.
        
    3. Clique em **Selecionar métrica** e selecione o asterisco (\*) novamente. Esse formato inclui métricas de cada contêiner único no espaço.
        
    4. Clique em **Selecionar métrica** e **cpu-0**.
        
    5. Clique em **Selecionar métrica** e em **cpu-idle**. A visualização do gráfico é atualizada para exibir as métricas que correspondem a esta consulta.
    
6. Opcional: customize a exibição do gráfico.
    
    * Para fornecer um nome ao gráfico, clique na guia Geral e, no campo Título, insira um nome para o
gráfico, por exemplo: CPU inativa
    * Para fornecer um rótulo ao eixo vertical, clique na guia Eixos e grade e, na seção Eixo Y à
esquerda, no campo Rótulo, insira CPU.
    * Para mudar a cor do plano de fundo do gráfico, na seção Limites da grade, para o Nível 2, clique
no ícone selecionador de cor do Plano de Fundo e mude a cor do plano de fundo para branco ou cinza claro.
    
    No cabeçalho, clique em **Voltar para o painel**.
    
7. Para salvar as mudanças feitas nesse painel, no cabeçalho, clique no ícone Salvar e, em seguida,
clique no ícone Salvar no menu.


## Incluindo uma visualização de memória usada
{:#grafana_add_mem}

Conclua as etapas a seguir para carregar uma visualização de memória usada:

1. Clique no botão Incluir uma linha. Uma régua de controle do menu Linha é exibida no lado da linha.
   
2. Passe o cursor sobre a régua de controle do menu de linha e, em seguida, clique no ícone do menu
Linha que desliza para fora.

    1. Clique em Incluir Painel > gráfico.
    2. Clique em Editar. O restante do painel fica oculto; apenas o editor desse gráfico e uma visualização do gráfico
são exibidos.
    
3. Na guia Métricas, construa uma consulta para coletar dados para o gráfico. 

    Por exemplo, quando você trabalha com contêineres, o formato da consulta inclui o ID do espaço, um
ID do grupo de contêiner e um ID da instância de contêiner única no formato a seguir:
space_ID.group_ID.instance_ID.metric
        
    1. Na linha A, clique em **Selecionar métrica**. Em seguida, selecione seu ID de
espaço.
    2. Clique em **Selecionar métrica** e selecione o asterisco (\*).
    
    Ao selecionar (\*), os dados incluem métricas de cada grupo de contêiner no espaço. Opcionalmente, é possível
manipular esse formato com uma expressão regular para incluir métricas apenas de certos contêineres. Por
exemplo, se desejar ver métricas apenas de contêineres únicos e excluir grupos de contêineres, clique em
**Selecionar métrica** e selecione **0000**.
    
    3. Clique em **Selecionar métrica** e selecione o asterisco (\*) novamente. Esse formato inclui métricas de cada contêiner único no espaço.
        
    4. Clique em **Selecionar métrica** e em **memória**.
        
    5. Clique em **Selecionar métrica** e em **memory-used**. A visualização do gráfico é atualizada para exibir as métricas que correspondem a esta consulta.
    
6. Opcional: customize a exibição do gráfico.
    
    * Para fornecer um nome ao gráfico, clique na guia Geral e, no campo Título, insira um nome para o
gráfico, por exemplo: Memória usada
    *  Para mudar o formato dos valores do eixo vertical, clique na guia Eixos e
grade e, na seção Eixo Y à esquerda, para o Formato,
selecione bytes.
    * Para fornecer um rótulo ao eixo vertical, no campo Rótulo, insira
Memória.
    * Para mudar a cor do plano de fundo do gráfico, na seção Limites da grade, para o Nível 2, clique
no ícone selecionador de cor do Plano de Fundo e mude a cor do plano de fundo para branco ou cinza claro.
    
    No cabeçalho, clique em **Voltar para o painel**.

7. Para salvar as mudanças feitas nesse painel, no cabeçalho, clique no ícone Salvar e, em seguida,
clique no ícone Salvar no menu.

