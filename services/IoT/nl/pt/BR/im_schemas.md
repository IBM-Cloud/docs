---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Criar esquemas de tipo de dispositivo
{: #iotrtinsights_task}

Para usar recursos do {{site.data.keyword.iot_short}}, como regras e ações, deve-se criar um esquema para mapear propriedades do dispositivo para nomes de propriedades fáceis e simples, configurar as unidades de dados para as propriedades e especificar um tipo de mensagem para uso com o esquema.
{: shortdesc}

**Importante:** esquemas são necessários para o uso de regras e ações. Para obter informações, consulte [Cloud Analytics](cloud_analytics.html#rules).

**Importante:** os recursos de análise de dados são mesclados a partir do serviço do {{site.data.keyword.iotrtinsights_full}}. Se sua organização do {{site.data.keyword.iot_short_notm}} for usada como uma origem de dados para uma instância existente do {{site.data.keyword.iotrtinsights_short}}, Cloud e Edge Analytics não estarão ativados até após a migração das instâncias existentes do {{site.data.keyword.iotrtinsights_short}}. Continue a usar o painel do {{site.data.keyword.iotrtinsights_short}} para suas necessidades de análise de dados até que a migração seja concluída. Para obter mais informações, veja o [blog do IBM Watson IoT Platform ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} no IBM developerWorks e seus painéis de instância existentes do {{site.data.keyword.iotrtinsights_short}}.  

## Incluindo um esquema de dispositivo
{: #add_schema}

Para incluir um esquema:  
1. Acesse **Dispositivos > Gerenciar esquemas** e clique em **Incluir esquema**.  
2. Selecione um tipo de dispositivo para associar com esse esquema de mensagem. **Importante:** apenas um esquema pode ser definido para um tipo de dispositivo.

3. Inclua uma ou mais propriedades.  
    É possível selecionar propriedades de um dispositivo conectado, criar propriedades virtuais que modifiquem ou combinem propriedades existentes ou incluir propriedades manualmente.  

    **Dica:** as propriedades disponíveis são definidas na carga útil das mensagens que são enviadas por um dispositivo. Para obter informações sobre o formato da carga útil do {{site.data.keyword.iot_short}}, consulte o tópico [Carga útil da mensagem](reference/mqtt/index.html#message-payloadl "Carga útil da carga útil da mensagem.").   
  <dl>
  <dt>Incluir uma propriedade manualmente</dt>
  <p><b>Dica:</b> para criar uma estrutura de propriedade aninhada, primeiro inclua uma propriedade que tenha o tipo de dados Parent. Na tabela de propriedades, é possível clicar então no ícone ![Incluir filho.](images/add_child.png "Incluir filho") para incluir uma ou mais propriedades-filhas.</p>
  <dd>
  <ol>
    <li>Selecione a guia **Manual**.</li>
    <li>Defina os detalhes da propriedade a seguir:
    <ul>  
      <li>Nome - Um nome descritivo da propriedade usada em painéis, menus e assistentes do {{site.data.keyword.iot_short}}.</li>
      <li>Tipo de dados - O tipo de dados da propriedade:  
   `Sequência`, `Número inteiro`, `Valor flutuante` ou `Pai`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Propriedade - O identificador da propriedade, por exemplo:  
 `temp` ou `speed`  </br> Para obter informações sobre como identificar as propriedades das mensagens do dispositivo, consulte [Identificando propriedades para seus dispositivos](#identify-datapoints "Identificar propriedades.").</li>
  <li>Unidade de dados - Opcional: a unidade de dados da propriedade. Por
exemplo:  
     `C` ou `Mph`  </li>
     <li> Casas decimais - Opcional, somente valor flutuante: o número de decimais para incluir nos dados do dispositivo.</li>
    </ul>
    </li>
    <li>Clique em **Concluir** para criar a propriedade.</li>
  </ol>
  </dd>
  <dt>Criar uma propriedade virtual</dt>
  <dd> Por exemplo, se a propriedade do dispositivo temp retornar um valor de temperatura em Fahrenheit e você deseja usar Celsius, será possível criar uma propriedade virtual *temp_c* que tenha a função a seguir: *temp_c=(temp-32 )/1.8*. É possível então usar a propriedade virtual *temp_c* em vez da propriedade em tempo real *temp* nas condições da regra.  
  Para criar uma propriedade virtual:
  <ol>
    <li>Selecione a guia **Propriedade virtual**.</li>  
    <li>Defina os detalhes da propriedade a seguir:
    <ul>
    <li>Nome - Um nome descritivo da propriedade usada em painéis, menus e assistentes do {{site.data.keyword.iot_short}}.</li>
    <li>Tipo de dados - O tipo de dados da propriedade:  
 `Float` ou `Integer`.</li>
 <li>Propriedade - Um identificador de propriedade para a propriedade virtual. Por
exemplo:  
`temp_virt`</li>
    <li>Cálculo - Inclua um ou mais componentes para definir uma função válida. É possível usar propriedades, valores numéricos e operadores matemáticos, como +, -, \*, /, ( e ).  
    Clique em **Avançado** para obter um conjunto de fórmulas para usar com séries de pontos de dados em dispositivos de borda. Para obter mais informações sobre as fórmulas avançadas, veja [Cálculos avançados para propriedades virtuais de borda](im_vir_calculations.html).  
    **Importante:** condições de regra que comparam propriedades virtuais com base em fórmulas avançadas não são suportadas.</li>
    <li>Unidade de dados - Opcional: a unidade de dados da propriedade. Por exemplo: `C` ou `Mph`</li>
    <li> Casas decimais - Opcional, somente valor flutuante: o número de decimais para incluir nos dados do dispositivo.</li>
   </ul>
   </li>
   <li>Clique em **Concluir** para criar a propriedade.</li>
  </ol>
  </dd>
  <dt>Selecione as propriedades de um dispositivo conectado</dt>
  <dd>
  <ol>
    <li>Selecione a guia **Do conectado**.</li>  
    <li>Selecione uma ou mais propriedades para incluir no esquema. Essas propriedades podem ser editadas posteriormente para configurar atributos, como nome e unidade de dados.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Clique em **OK** para criar as propriedades.</li>
  </ol>
  </dd>
    <dd>As propriedades selecionadas são incluídas e a descrição é configurada como o nome da propriedade. Clique na propriedade na lista para editá-la e incluir atributos adicionais, como tipo de sensor, tipo de dados e número de casas decimais.</dd>
  </dl>
8. Clique em **Concluir** para criar o esquema de mensagem.

## Identificando propriedades para seus dispositivos.
{: #identify-datapoints}
   As propriedades de um dispositivo podem ser localizadas no painel do {{site.data.keyword.iot_short}}.

1. No painel do {{site.data.keyword.iot_short}}, acesse **Dispositivos**.
2. Clique em um dispositivo para abrir uma página que mostra detalhes do dispositivo.
3. Role para baixo até a seção **Informações do sensor** para ver uma lista das propriedades disponíveis para um dispositivo conectado.
