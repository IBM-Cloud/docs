---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrando seus logs para um valor de campo específico
{:#k4_filter_logs_spec_field}

É possível procurar por entradas que incluam um valor de campo específico.{:shortdesc}

Conclua as etapas a seguir para procurar por entradas que incluem um valor de campo específico:

1. Consulte a página Descobrir do Kibana para ver qual subconjunto de seus dados é exibido. Para obter mais informações, consulte [Identificando os dados que são exibidos em sua página Descobrir do Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Na *Lista de campos*, identifique o campo para o qual deseja definir um filtro e clique nele.

    Um máximo de 5 valores é mostrado para o campo. Cada valor possui dois botões de lupa. 
    
    Se você não conseguir ver o valor, consulte [Incluindo um filtro para um valor que não estiver relacionado na lista Campos](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. Para incluir um filtro que procure por entradas com um valor de campo, escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_include_field_icon.jpg "Botão de lupa no modo inclusivo") para esse valor.

    ![Filtro que inclui o valor de campo](images/k4_add_filter_for_field.jpg "Filtro que inclui o valor de campo")

    Para incluir um filtro que procure por entradas que não incluam esse valor de campo, escolha o botão de lupa ![Botão de lupa no modo inclusivo](images/k4_exclude_field_icon.jpg "Botão de lupa no modo inclusivo") para o valor.

    ![Filtro que exclui o valor de campo](images/k4_add_filter_to_exclude_field.jpg "Filtro que exclui o valor de campo")

4. Escolha qualquer uma das seguintes opções para trabalhar com filtros no Kibana:

    <table>
      <tbody>
        <tr>
          <th align="center">Opção</th>
          <th align="center">Descrição</th>
          <th align="center">Outras informações</th>
        </tr>
        <tr>
          <td align="left">Ativar</td>
          <td align="left">Selecione essa opção para ativar um filtro.</td>
          <td align="left">Ao incluir um filtro, ele é ativado automaticamente.<br> Se um filtro estiver desativado, clique nele para ativá-lo.</td>
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

 

 
 

