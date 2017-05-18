---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizando painéis e relatórios
{: #DRA_toolchain_reports}

O {{site.data.keyword.DRA_short}} fornece a você uma riqueza de informações acionáveis sobre os seus projetos.
{:shortdesc}

## Painéis do {{site.data.keyword.DRA_short}}    
{: #DI_toolchain_dashboards}

O {{site.data.keyword.DRA_short}} fornece painéis que exibem informações sobre o desempenho ao longo de sua organização do Bluemix. Para vê-los,
após abrir o {{site.data.keyword.DRA_short}}, clique em **Construir verificação** ou em **Implementar
verificação**.

Os painéis são preenchidos automaticamente com as informações mais recentes a partir das tarefas de teste do {{site.data.keyword.DRA_short}} dos
seus pipelines. Clique nos elementos dentro dos painéis para obter mais informações sobre eles.

### Principais indicadores de desempenho em construções    
{: #DI_key_performance_indicators}

A página **Construir verificação** contém três gráficos que contêm informações sobre o funcionamento da filial de desenvolvimento
selecionada:

<table>
<thead>
<tr>
<th>Gráfico</th>
<th>Descrição</th>
</tr>
</thead>

<tbody>
<tr>
<td>Construções mais recentes</td>
<td>O número de construções recentes que foram concluídas comparado com o número total de construções recentes.</td>
</tr>
<tr>
<td>Testes</td>
<td>O número de testes que passaram comparado com o número total de testes.</td>
</tr>
<tr>
<td>Cobertura do Código</td>
<td>As porcentagens de instruções e funções do seu código que são chamadas por seus testes.</td>
</tr>
</tbody></table>

## Visualizando relatórios de decisão    
{: #DI_decision_reports}

Após um pipeline ser executado, o {{site.data.keyword.DRA_short}} começa a coletar e analisar os resultados de teste a partir dele, para estabelecer uma referência. Dados de cada execução subsequente são coletados e comparados com resultados anteriores. Portas de decisão usam esses dados para determinarem quando
parar uma implementação. 

Para visualizar o relatório de decisão para uma porta a partir do pipeline, conclua estas etapas:

   1. No estágio que contém a porta a ser verificada, clique em **Visualizar logs e histórico**.

   2. A partir da janela de tarefas no estágio, clique no nome da porta.

   3. Na visualização de log, localize a mensagem 'Verifique o relatório do {{site.data.keyword.DRA_short}} aqui' e clique no link fornecido para abrir
o relatório.
