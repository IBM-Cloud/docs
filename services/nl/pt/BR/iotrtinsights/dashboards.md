---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Gerenciando painéis e modelos {: #managing-dashboards}

Os dados em tempo real de seus dispositivos IoT são exibidos nos painéis customizáveis. É possível criar manualmente os painéis que exibem métricas em tempo real, mostrar gráficos e exibir outras informações para um ou mais dispositivos. Os painéis também pode conter listas filtradas de dispositivos e links para outros painéis.
{: shortdesc}

Além dos painéis criados manualmente, o {{site.data.keyword.iotrtinsights_short}} é fornecido com um painel de alertas de dispositivo predefinidos em **Painéis > Visão geral** e cria painéis de dispositivo dinamicamente com base nos esquemas de mensagens criados.

## Painéis {: #dashboards}

Os administradores podem criar novos painéis e modificar os existentes para exibir os dados do dispositivo de interesse.   
Para criar um painel:
1.	Acesse **Painéis > Procurar painéis**. 
2.	Clique em **Incluir novo painel**. 
3.	Dê ao painel um nome e selecione atributos, como ícone e segundo plano. Além disso, selecione se deseja tornar esse painel editável para usuários operadores do {{site.data.keyword.iotrtinsights_short}}.
4.	Clique em ![ícone Criar](images/create.png "ícone Criar"). 
5.	Clique no novo tile do painel para abrir o painel vazio. 
6.	Para incluir widgets no painel:   
 1.	Clique em **Incluir novo componente** para incluir um widget do painel inicial. 
 2.	Selecione um componente para incluir, em seguida, selecione os atributos de componente e, se necessário, selecione as propriedades de exibição.
 Por exemplo, para exibir o valor numérico de um ponto de dados específico para um dispositivo, selecione `Dispositivo` e, em seguida, selecione o dispositivo a ser incluído. No editor do painel, sob Visualização, selecione um ponto de dados a ser exibido. Em seguida, posicione o widget recentemente incluído na grade do painel. 
 3.	Clique em ![ícone Criar](images/create.png "ícone Criar") para incluir o widget no painel.
7.	O painel é atualizado com os widgets recentemente incluídos e exibe os dados em tempo real que são definidos pelo ponto de dados selecionado. 

>**Dica:** para criar um painel que lista todos os seus dispositivos, faça o seguinte:   
1. Acesse **Painéis > Procurar painéis** e clique em **Incluir novo painel**. 
2. Dê ao painel um nome descritivo, como `Todos os dispositivos`, e clique em ![ícone Criar](images/create.png "ícone Criar"). 
3. Na área de painéis, clique no painel e, em seguida, clique em **Incluir novo componente**.
4. Selecione o componente **Contêiner** e selecione **Dispositivos filtrados** para criar uma lista de todos os seus dispositivos. 
5. Clique em ![ícone Criar](images/create.png "ícone Criar").   

>Seus dispositivos são listados no novo painel. Clique em um ícone de dispositivo para abrir o painel de dispositivo e ver os dados em tempo real para o dispositivo.

### Widgets de Painel {: #dashboard-widgets}
Os painéis são compostos de widgets que exibem dados em tempo real de um ou mais dispositivos. O comportamento do widget depende de seu tipo, do ponto de dados que é exibido e do modo como o ponto de dados é configurado no esquema.   
Por exemplo, se você incluir um widget de dispositivo para um ponto de dados 'brutos', o widget exibirá os dados brutos somente como uma sequência. 

Se, no entanto, você configurar o ponto de dados com um valor mín. e máx., terá a opção de exibir um widget como um calibrador. 

Também é possível designar um tipo de Sensor para o ponto de dados para ativar um tipo especial de widget de visualização para ilustrar melhor o tipo dos dados do sensor que são exibidos. Por exemplo, é possível selecionar o tipo de sensor `Aceso/Apagado` para ativar um widget de visualização `Indicador de luz simples (ligado/desligado)`.

Você também tem a opção de incluir vários widgets para o mesmo ponto de dados no mesmo painel para mostrar o valor numérico bruto e a umidade lado a lado. ![Vários widgets para o mesmo ponto de dados.](images/widgets.svg "Vários widgets para o mesmo ícone de ponto de dados")  
*Três opções de visualização para o mesmo ponto de dados.* 


Widget | Tipo e visualização
------------- | -------------
Dispositivo | Dados - Valor em tempo real de pontos de dados para o dispositivo. Se o ponto de dados estiver configurado para incluir um valor mínimo e um máximo, as opções de visualização incluirão mostrar o ponto de dados como um calibrador. Além disso, se o ponto de dados estiver configurado com um tipo de sensor, opções de visualização adicionais estarão disponíveis.
Diagrama | Gráfico - Criar gráfico de valores em tempo real de pontos de dados para um ou mais dispositivos.
Painel | Vincular a um painel ou modelo.
Mensagem | Caixa de texto - Texto formatado.
Container | Tipos de widgets de contêiner:<ul><li>Todos os painéis – Uma lista vinculada de todos os painéis.</li><li>Dispositivos filtrados – Uma lista de todos os dispositivos, ou filtrados por nome ou local.</li><li>Dispositivos filtrados com alertas – Uma lista de todos os dispositivos com alertas, filtrados por nome ou local.</li><li>Alertas para dispositivo – Uma lista de alertas para um dispositivo que é selecionado em um contêiner de Dispositivos filtrados com alertas.</li></ul>
Especial | Tipos de widgets especiais:<ul><li>Mapa – Um mapa que localiza o dispositivo selecionado.</li><li>Informações adicionais do dispositivo – Informações adicionais sobre o dispositivo selecionado.</li></ul>

A tabela a seguir resume as opções de visualização que estão disponíveis para os widgets de dispositivo se o ponto de dados selecionado estiver configurado com um atributo de tipo de sensor no esquema de mensagem.

Tipo de sensor de ponto de dados | Opções de visualização | Detalhes | Tipo de dados suportado
------------- | ------------- | -------------
Nenhuma seleção | Valor simples | - | Sequência/Número inteiro/Valor flutuante
Apagado/Aceso | Indicador de luz simples (ligado/desligado) | 0=desligado | Número inteiro
Ligado/Desligado | Indicador de comutador simples (ligado/desligado) | 0=desligado | Número inteiro
Sensor de temperatura | Calibrador genérico de temperatura | N/D | Número inteiro/Valor flutuante
Controle de temperatura | Calibrador genérico de temperatura | N/D | Número inteiro/Valor flutuante
Sensor de pressão | Calibrador de pressão simples | N/D | Número inteiro/Valor flutuante
Níveis de bateria | Widget de bateria simples (baixo/alto) | 0=bom | Número inteiro
Brilho | Indicador de brilho (escuro/claro) | 0=preto | Número inteiro
Abertura/fechamento de janela | Estado de janela simples (aberta/fechada) | 0=fechada | Número inteiro
Abertura/fechamento de porta | Estado de porta simples (aberta/fechada) | 0=fechada | Número inteiro
Sensor de umidade | Estado de umidade (seco/molhado) | 0=seco | Número inteiro
Consumo de energia | Calibrador de energia simples | N/D | Número inteiro/Valor flutuante
Medidor de energia | Valor simples | N/D | Número inteiro/Valor flutuante
Porcentagem | Porcentagem simples (0-100) | N/D | Número inteiro/Valor flutuante
Voltagem | Calibrador de voltagem simples | N/D | Número inteiro/Valor flutuante
Corrente | Calibrador de corrente simples | N/D | Número inteiro/Valor flutuante
Longitude | Local do dispositivo em Especial > widget Mapa (o widget Latitude também é necessário) | **Importante:** o ponto de dados usado para o valor de longitude deve ser designado ao tipo de sensor Longitude no esquema de mensagem. | Valor flutuante
Latitude | Local do dispositivo em Especial > widget Mapa (o widget Longitude também é necessário) | **Importante:** o ponto de dados usado para o valor de latitude deve ser designado ao tipo de sensor Latitude no esquema de mensagem. | Flutuação  


## Layouts do painel padrão
O {{site.data.keyword.iotrtinsights_short}} é fornecido com painéis predefinidos: um painel de alertas e painéis de dispositivo.

As tabelas a seguir descrevem os widgets e o layout dos painéis predefinidos.
### Painel Alertas (Painéis > Visão geral)
Esse painel é incluído com o produto e fornece uma lista de dispositivos que têm alertas abertos. É possível selecionar um dispositivo para ver detalhes sobre os alertas e é possível clicar no ícone de dispositivo para abrir um painel de dispositivo para exibir os dados em tempo real para o dispositivo. 

<table>
<thead>
<tr>
<th colspan="3">Painel de Alertas</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contêiner: dispositivos com alertas</td>
<td style="width:30%">Contêiner: alertas para o dispositivo</td>
<td style="width:30%">Especial: informações adicionais sobre o dispositivo</td>
</tr>
<tr>
<td style="width:30%"></td>
<td style="width:30%"></td>
<td style="width:30%">Especial: Mapa</td>
</tr>
</tbody>
</table>

*Layout do painel Alertas*

### Painéis de dispositivo
Clicar em um ícone de dispositivo em uma lista de dispositivos abre um painel de dispositivo para o dispositivo. Quando um ponto de dados é incluído no esquema de mensagem, ele também é incluído como um widget no modelo de dispositivo, que cria dinamicamente o painel de dispositivo. Os administradores podem incluir ou remover widgets manualmente. 

<table>
<thead>
<tr>
<th colspan="3">Painel de dispositivo </th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Dispositivo: ponto de dados 1</td>
<td style="width:30%">Dispositivo: ponto de dados 2</td>
<td style="width:30%">Dispositivo: ponto de dados 3</td>
</tr>
<tr>
<td style="width:30%">Dispositivo: ponto de dados N</td>
<td style="width:30%"></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Layout do painel de dispositivos predefinidos*

### Exemplo de painel: lista de todos os dispositivos
O painel a seguir inclui uma lista de todos os dispositivos e fornece informações sobre o dispositivo quando você seleciona um dispositivo da lista. 

<table>
<thead>
<tr>
<th colspan="3">Painel de lista de todos os dispositivos</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contêiner: dispositivos filtrados (nenhum parâmetro de filtro configurado) </td>
<td style="width:30%">Especial: informações adicionais sobre o dispositivo</td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Layout do painel de lista de todos os dispositivos*

## Modelos {: #templates}
Os modelos controlam o layout dos painéis predefinidos para um tipo de dispositivo específico. Os administradores podem modificar esses modelos predefinidos para adequar às suas necessidades. Por exemplo, um modelo predefinido inclui somente os pontos de dados genéricos. É possível incluir gráficos e outros componentes conforme necessário. 

Por exemplo, um usuário pode acessar o painel de dispositivos predefinidos para ver dados básicos de dispositivos e, em seguida, seguir um link para um modelo criado manualmente que pode conter um conjunto completo de gráficos em tempo real. Você cria um modelo de forma semelhante como cria um painel.   

Para modificar um modelo predefinido: 
1.	Acesse **Painéis > Gerenciar modelos**.
2.	No painel Gerenciar modelos, localize o arquivo de modelo e clique em ![ícone Configurar.](images/gear.png "ícone Configurar")** > Mudar layout** para abrir o modelo para edição.  
3.	Inclua widgets no modelo.
 1.	Clique em **Incluir novo componente modelo** para incluir um widget de modelo inicial. 
 2.	Selecione um componente para incluir, em seguida, selecione os atributos de componente e, se necessário, selecione as propriedades de exibição.  
 3.	Clique em ![ícone Criar](images/create.png "ícone Criar") para incluir o widget no modelo. 
4.	Edite os widgets existentes.
 1.	Passe o mouse sobre um widget de modelo e clique em ![ícone Configurar](images/gear.png "ícone Configurar").
 2.	Modifique o componente e seus atributos e reposicione o widget conforme necessário. 
 3.	Clique em ![ícone Criar](images/create.png "ícone Criar") para atualizar o widget.   

O modelo é atualizado com suas mudanças. 

<!-- Administrators can also manually add templates for specific device types. These templates can then be linked to from the predefined templates.  -->

<!-- To create a template:
1.	Go to **Dashboards > Manage templates**.
2.	Click **Add new template**.
3.	Give the template a name, select a device type and attributes such as icon and background.
4.	Click ![Create icon.](images/create.png "Create icon").
5.	The empty template opens.
6.	Add widgets to the template.  
For a list of widgets, see below.
 1.	Click **Add new component** to add an initial template widget.
 2.	Select a component to add, then select further component attributes and, if needed, select display properties.
 For example, ... Then position the newly added widget in the dashboard grid.
 3.	Click ![Create icon.](images/create.png "Create icon") to add the widget to the template.
7.	The template updates with the newly added widgets.

### Template widgets
Widget | Type and visualization
------------- | -------------
Device | Data - Real-time value of data points for the device. For a description of the available widget options, see [Dashboard widgets](#dashboard-widgets "Dashboard widgets") above.
Chart | Graph - Plot real-time values of data points for one or more devices.
Dashboard | Link to a dashboard or a template.
Text | Text box - Formatted text
Container | Types of containers:<ul><li>All dashboards – A linked list of all dashboards</li><li>Filtered devices – A list of all devices, or filtered by name or location</li><li>Filtered devices with alerts – A list of all devices with alerts, or filtered by name or location</li><li>Alerts for device – A list of alerts for a device that is selected in a Filtered devices with alerts container</li></ul>
Special | Types of special:<ul><li>Map – A map that locates the selected device</li><li>Additional device information – More information about the selected device</li></ul>

### Template example: Selected set of graphs
One way of using device templates is to expand on the predefined device template by creating specialized templates for a device type, and then linking these from the predefined template by using a Dashboard widget.

<table>
<thead>
<tr>
<th colspan="3">Descriptive graphs template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: ID</td>
<td style="width:30%">Graph: One data point</td>
<td style="width:30%">Graph: Another data point</td>
</tr>
<tr>
<td style="width:30%">Special: Additional device information</td>
<td style="width:30%">Text: Short description of how to <br>interpret the device data in the graphs.</td>
<td></td>
</tr>
</tbody>
</table>

*Descriptive graphs template*

Link to this template from a predefined device template:

<table>
<thead>
<tr>
<th colspan="3">Predefined device dashboard layout with link to template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: Datapoint 1</td>
<td style="width:30%">Device: Datapoint 2</td>
<td style="width:30%">Device: Datapoint 3</td>
</tr>
<tr>
<td style="width:30%">Device: Datapoint N</td>
<td style="width:30%"><b>Dashboard: Descriptive graphs template</b></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Predefined device dashboard layout with link to template* -->


## Reconfigurando modelos e painéis predefinidos {: #resetting-dashboards}
Se você modificar um modelo predefinido, o modelo não será mais atualizado dinamicamente a partir de atualizações do esquema de mensagem e será necessário reconfigurar o painel ou modelo para restaurar o layout e widgets originais. Para reconfigurar os painéis e modelos predefinidos: 
1.	Acesse **Painéis > Gerenciar modelos** ou **Painéis > Procurar painéis**.
2.	Localize o tile de modelo ou painel predefinido e clique em **![ícone Configurar](images/gear.png "ícone Configurar") > Reconfigurar layout** para excluir e, em seguida, recriar o modelo.  

O modelo ou painel é recriado com o widget padrão configurado. 
