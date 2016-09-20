---

copyright:
  years: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Conectando e visualizando seus dispositivos
{: #iotrtinsights_task}
*Última atualização: 11 de fevereiro de 2016*

O {{site.data.keyword.iotrtinsights_short}} usa o {{site.data.keyword.iot_short}} para acesso ao dispositivo e recuperação de dados. Os dispositivos que você conecta ao {{site.data.keyword.iot_short}} são conectados automaticamente ao {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Se você estiver conectando um novo tipo de dispositivo, também deve-se configurar o esquema de mensagem para mapear os pontos de dados do dispositivo, configurar as unidades e nomear o tipo de dispositivo. Se os seus dispositivos forem de um tipo de dispositivo já configurado, os dados aparecerão automaticamente no painel. 

## Incluindo um novo dispositivo
{: #iotrtinsights_subtask}

Para incluir um novo dispositivo:   
A inclusão de um novo dispositivo é um processo de duas etapas. Primeiro, você inclui o dispositivo no {{site.data.keyword.iot_short}} e, em seguida, configura como o {{site.data.keyword.iotrtinsights_short}} consome e exibe os dados do dispositivo. 
1. Inclua dispositivos no {{site.data.keyword.iot_short}}. 
> **Dica:** se você implementou o aplicativo de telefone Internet of Things, um dispositivo iotphone já estará incluído no *iot-phone-iotf-service* {{site.data.keyword.iot_short}} e será possível ignorar esta etapa.   

  Para incluir novos dispositivos no {{site.data.keyword.iot_short}}, veja a [documentação do {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html) e as [receitas de conexão de dispositivo do {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configure seu dispositivo no {{site.data.keyword.iotrtinsights_short}}.  
  1. Efetue login no console do {{site.data.keyword.iotrtinsights_short}} como um usuário administrador.
  9. Acesse **Dispositivos > Procurar dispositivos** e verifique se o dispositivo recém-incluído está listado. 
  > **Dica:** a lista de dispositivos é atualizada a partir da origem de dados uma vez por minuto. Clique em **Atualizar** para atualizar a lista de dispositivos agora mesmo.
  3. Acesse **Dispositivos > Gerenciar esquemas** e clique em **Incluir novo esquema de mensagem**.   
  4. Insira um nome para o esquema de mensagem, por exemplo:
  `Novo esquema de mensagem`.
  5. Clique em **Vincular a nova origem de dados** e selecione a origem de dados e o tipo de dispositivo que corresponde à sua instância do {{site.data.keyword.iot_short}} e ao dispositivo. Opcionalmente, insira um nome de evento para coletar dados somente para esse evento ou deixe o curinga `+` para coletar todos os eventos. Mais informações sobre como identificar tipos de eventos para o dispositivo estão [aqui](#identify-datapoints "Identificar pontos de dados.").   
  >**Importante:** cada esquema de mensagem deve ter uma combinação exclusiva de origem de dados, tipo de dispositivo e nome do evento. Para criar mais de um esquema para uma origem de dados específica e uma combinação de tipo de dispositivo, especifique um nome de evento exclusivo para cada esquema de mensagem em vez de usar o curinga padrão `+`.    
  6. Inclua um ou mais pontos de dados que você deseja incluir nos painéis de dispositivo.
    É possível selecionar pontos de dados de um dispositivo conectado ou incluir pontos de dados manualmente. Os pontos de dados disponíveis são definidos na carga útil das mensagens que são enviadas por um dispositivo. Para obter informações sobre o formato de carga útil do {{site.data.keyword.iot_short}}, veja o tópico [Carga útil da mensagem](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Carga útil da mensagem.") na documentação do {{site.data.keyword.iot_short}}.   
    > **Dica:** é possível criar manualmente pontos de dados virtuais que modificam ou combinam pontos de dados existentes que são do tipo número inteiro ou valor flutuante. Por exemplo, se o ponto de dados do dispositivo temp retornar um valor de temperatura em Fahrenheit e você desejar usar Celsius em seu lugar, será possível criar um ponto de dados virtual *temp_c* com a função a seguir *temp_c=(temp-32)/1.8*. É possível, então, usar o ponto de dados virtual *temp_c* em vez do ponto de dados em tempo real *temp* em suas condições da regra. Nos painéis, os pontos de dados virtuais são identificados por um sublinhado tracejado.     

  <dl>
  <dt>Selecionar a partir do dispositivo conectado </dt>
  <dd>
  <ol>
    <li>Clique em **Selecionar a partir do dispositivo conectado**. </li>  
    <li>No diálogo Incluir pontos de dados, selecione um ou mais pontos de dados para incluir e, em seguida, clique em **OK**. </li>   
    <li>Os pontos de dados selecionados são incluídos com a descrição configurada para o nome do ponto de dados. Clique no ponto de dados na lista para editá-lo e inclua atributos adicionais, como tipo de sensor, tipo de dados e número de casas decimais. </li>
  </ol>
  </dd>
  <dt>Incluir manualmente </dt>
  <p><b>Dica:</b> para criar uma [estrutura de pontos de dados aninhados](schemas.html), primeiro inclua um ponto de dados que tenha o tipo de dados Pai. Na tabela de pontos de dados, é possível clicar em ![ícone Incluir filho.](images/add_child.png "Incluir filho") para incluir um ou mais pontos de dados filhos.</p>
  <dd>
  <ol>
    <li>Clique em **Incluir manualmente**. </li>
    <li>Selecione **Ponto de dados em tempo real** ou **Ponto de dados virtual** </br></li>
    <li>Defina as informações de ponto de dados a seguir:
    <ul>  
     <li> Ponto de dados - O identificador de ponto de dados que você [localizou no painel do {{site.data.keyword.iot_short}}](#identify-datapoints "Identificar pontos de dados."). Por
Exemplo:  
   `id`, `ts`, `lat`  </li>
     <li>Descrição - Uma descrição simples do ponto de dados. Essa descrição é usada ao exibir os pontos de dados em painéis. </li>
     <li>Função de ponto de dados virtual - Inclua um ou mais componentes para definir uma função válida. É possível usar pontos de dados, valores numéricos e operadores matemáticos como +, -, \*, /, (, e ) para construir sua função. </li>
     <li>Tipo de dados - O tipo de dados do ponto de dados:  
   `Sequência`, `Número inteiro`, `Valor flutuante` ou `Pai`.</li>
     <li>Tipo de sensor - Opcionalmente, selecione como interpretar o ponto de dados nos painéis. Dependendo da combinação de tipo e de tipo de sensor, opções adicionais de visualização podem estar disponíveis para seus widgets do painel. Para obter mais informações sobre tipos de sensor e opções de visualização, veja [Widgets do painel](dashboards.html#dashboard-widget "Widgets do painel"). </li>
     <li>Ícone de ponto de dados - Opcionalmente, selecione um ícone para representar o ponto de dados nos widgets do painel.</li>
     <li>Valor mín./Valor máx. - Opcional, somente número inteiro e valor flutuante: se um valor máx. e um mín. forem inseridos, os dados do dispositivo poderão ser exibidos como um calibrador nos painéis.</li>
     <li>Unidade de dados - Opcional: a unidade de dados do ponto de dados. Por
Exemplo:  
     `C`, `Mph`  </li>
     <li> Casas decimais - Opcional, somente valor flutuante: o número de decimais para incluir nos dados do dispositivo.</li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. Clique em **OK** para criar o esquema de mensagem. 
   9. Acesse **Dispositivos > Procurar dispositivos** e clique em seu dispositivo recém-incluído para verificar se os dados do dispositivo em tempo real são exibidos e se os pontos de dados estão mapeados corretamente. 

## Identificando pontos de dados e eventos no painel do {{site.data.keyword.iot_short}}. 
{: #identify-datapoints}
   Os pontos de dados e tipos de eventos para um dispositivo podem ser localizados no painel do {{site.data.keyword.iot_short}}.
   >**Dica:** se você estiver usando o aplicativo de telefone Internet of Things como seu dispositivo IoT, será possível usar o evento sensorData e os pontos de dados a seguir para configurar o esquema de mensagem:
   >- d.id - ID do dispositivo
   >- d.ts - Registro de data e hora
   >- d.lat - Latitude
   >- d.lng - Longitude
   >- d.ax - Aceleração X
   >- d.ay - Aceleração Y
   >- d.az - Aceleração Z
   >- d.oa - Movimento alpha
   >- d.ob - Movimento beta
   >- d.og - Movimento gama
   >Em que d.*datapoint* indica que o ponto de dados é aninhado sob um ponto de dados do tipo-pai d na carga útil da mensagem.

   1. No painel do Bluemix, clique no tile Internet of Things.   
   >**Nota:** se você estiver usando o aplicativo de telefone Internet of Things, clique no tile *iot-phone-iotf-service*.  
   2. Clique em **Ativar painel** para abrir o painel do {{site.data.keyword.iot_short}}.
   3. Acesse a página **Dispositivos**. 
   4. Clique em seu dispositivo para abrir a página de detalhes do dispositivo.
     Role para baixo até a seção **Informações do sensor** para ver uma lista de eventos e pontos de dados disponíveis para o dispositivo. Essas informações são necessárias ao configurar o dispositivo no {{site.data.keyword.iotrtinsights_short}}. 
