---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao iniciador do {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Introdução ao {{site.data.keyword.iot_full}} usando o projeto do {{site.data.keyword.iot_short_notm}} Starter GitHub. Usando o Starter, é
possível simular rapidamente um dispositivo, criar cartões, gerar dados e iniciar a análise e exibir dados no painel do
{{site.data.keyword.iot_short_notm}}.  
{:shortdesc}

## Visão geral
{: #overview}  

O iniciador é implementado automaticamente e conecta esses serviços:
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>Um serviço da web do IoT que inclui gerenciamento de gateway, gerenciamento de dispositivo e acesso ao aplicativo. Usando o
{{site.data.keyword.iot_short_notm}}, é possível coletar dados do dispositivo conectados e executar analítica em dados em tempo real por meio de sua
organização.</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>O ambiente de tempo de execução no qual o Node-RED é executado. </br>Para obter mais informações, veja a
documentação do iniciador do [{{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html).</dd>
<dd>O Node-RED é uma ferramenta para conexão de dispositivos de hardware, APIs e serviços on-line em conjunto, de maneiras novas e interessantes.  É possível usar o Node-RED para criar um termostato simulado que
envia dados simulados para o seu serviço do {{site.data.keyword.iot_short_notm}}. É possível criar cartões para exibir dados em tempo real no painel do {{site.data.keyword.iot_short_notm}}. </br>Para obter mais informações, consulte a [documentação do Node-RED](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>O banco de dados no qual o Node-RED armazena metadados.</dd>
</dl>

## Antes de iniciar
{: #byb}  

- Contas necessárias  
Antes de iniciar, será necessária uma [conta do IBM Bluemix](https://bluemix.net/registration).

- Circulando  
Para facilitar a movimentação entre tarefas no processo a seguir, abra o painel do {{site.data.keyword.Bluemix_notm}}, o
painel do {{site.data.keyword.iot_short_notm}} e o aplicativo Node-RED em guias diferentes em seu navegador.
<dl>
<dt>Painel do *{{site.data.keyword.Bluemix_notm}}*</dt>
<dd>Veja o estado de sua implementação, leia a documentação e ative os painéis.</dd>
<dt>Painel do *{{site.data.keyword.iot_short_notm}}*</dt>
<dd>Defina tipos de dispositivo, registre dispositivos, monitore dados do sensor recebidos, crie cartões de visualização de dados e veja visualizações de dados em
tempo real.</dd>
<dt>*Node-RED*</dt>
<dd>Configure e execute o fluxo de simulador de dispositivo e trabalhe com outros fluxos para processar dados do
{{site.data.keyword.iot_short_notm}}.</dd>
</dl>

## Etapa 1: Implemente o {{site.data.keyword.iot_short_notm}} Starter
{: #deployStarter}

Execute as etapas a seguir para implementar o aplicativo de amostra Starter:

1. Implemente o aplicativo iniciador.
 1. Clique em <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> para criar uma nova Cadeia de ferramentas de entrega contínua no Bluemix:  (via Continuous Delivery)  
 **Dica:** se você preferir implementar por meio da linha de comandos, será possível [localizar o iniciador do {{site.data.keyword.iot_short_notm}}](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) na organização do IBM Watson IoT no GitHub.
 2. Quando solicitado, efetue login no IBM Bluemix.
 3. Se necessário, selecione o Bluemix Organization no qual você deseja implementar o aplicativo iniciador.
 4. Mantenha o nome da Cadeia de ferramentas ou o atualize conforme necessário. Ele é usado como o nome do app padrão e a raiz de URL do seu app:
`<app-name>.mybluemix.net`
 5. Clique em **Criar**.  
**Dica:** clique no azulejo **Delivery Pipeline** para monitorar o progresso para a sua primeira implementação.
 6. Quando a implementação estiver concluída, clique em **Visualizar app** para abrir o novo aplicativo Node-RED em uma nova guia.
2. Localize os serviços do aplicativo Starter.
 1. No menu Bluemix, selecione **Painel**.
 2. Localize os serviços a seguir sob *Todos os serviços*:
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Localize a cadeia de ferramentas sob *Todos os apps*:
    - default-toolchain-{id}}


## Etapa 2: defina um dispositivo simulado em {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}

Conclua as etapas a seguir para simular um cenário que use um termostato para monitorar temperatura, umidade e local de uma sala de estar.

1.	Ative o painel do {{site.data.keyword.iot_short_notm}}.
  1. No painel do Bluemix, sob *Todos os serviços*, clique no nome de sua instância do {{site.data.keyword.iot_short_notm}}.
**Dica:** o nome da instância geralmente inclui `iotp-starter`.
  2. Clique em **Ativar** para abrir o painel do {{site.data.keyword.iot_short_notm}} em uma nova guia do navegador.   
A página `Todas as placas` é exibida por padrão.
2. Crie um tipo de dispositivo.
  1.	No menu principal, selecione **Dispositivos** e, em seguida, clique em **Incluir dispositivo**.
  2.	Na página Incluir dispositivo, clique em **Criar tipo de dispositivo**.
  3.	Na página Criar tipo de dispositivo, clique em **Criar tipo de dispositivo**.
  4. Insira um nome exclusivo (por exemplo `Termostato`) para o seu tipo de dispositivo e clique em **Avançar**.
  5. Opcional: definir um modelo e metadados nas próximas duas páginas é opcional e pode ser ignorado com segurança clicando em
**Avançar** em cada página.
  6.	Clique em **Criar** para incluir o tipo de dispositivo.
3.	Inclua um dispositivo que use o tipo de dispositivo recém-criado.
  1. Na página Incluir dispositivo, o tipo de dispositivo que você acabou de criar é exibido na lista de tipos de dispositivo. Clique em
**Avançar** para incluir um dispositivo que use esse tipo de dispositivo.
  2. Insira um ID do dispositivo exclusivo (por exemplo `LivingRoomThermo1`).
  3. Opcional: fornecer dados descritivos na página Incluir dispositivo ou inserir metadados de dispositivo na próxima página é opcional e é possível ignorar
com segurança essas páginas, clicando em **Avançar** em cada página.
  4. Na página Segurança, clique em **Avançar** para gerar um token de autenticação para o seu dispositivo.
  5. Na página Resumo, verifique se as informações estão corretas e clique em **Incluir** para incluir o dispositivo. Clique em **Voltar** para retornar a uma página anterior.
4.	Tome nota das informações que são exibidas na página Credenciais de seu dispositivo.   
São necessárias as informações a seguir para configurar o simulador e exibir os dados:
 - ID de Organização
 - Tipo do Dispositivo
 - ID do dispositivo
 - Método de Autenticação
 - Token de Autenticação

## Etapa 3: configure e execute o simulador de dispositivo do Node-RED.  
{: #confignodered}  
Configure o simulador de dispositivo do Node-RED para enviar mensagens do dispositivo do MQTT com informações de temperatura e umidade para
o {{site.data.keyword.iot_short_notm}}.

1. Ative o editor de fluxo do Node-RED.
  1. No painel do Bluemix, sob *Todos os apps*, clique no nome de sua cadeia de ferramentas.  
**Dica:** o nome da cadeia de ferramentas geralmente inclui `default-toolchain...`.
  2. No painel de cadeia de ferramentas, abra a sua instância do Node-RED clicando em **Rotas** e selecionando o link rota.  
  2. Clique em **Acessar o seu editor de fluxo do Node-RED** para abrir o editor.
2. Implemente o seu dispositivo.
  1. No fluxo do Simulador de dispositivo, dê um clique duplo no nó **Enviar para o IBM IoT Platform** azul.
  2. Verifique se a Autenticação está configurada como **Bluemix Service**.
  3. Insira o **Tipo de dispositivo** e o **ID do dispositivo** de seu dispositivo e clique em
**Pronto**.
  4. Implemente o dispositivo clicando em **Implementar**.
3. Configure o fluxo do Monitor de temperatura do Node-RED.
  1. No fluxo do Simulador de dispositivo, dê um clique duplo no nó **IBM IoT App In**.
  2. Em Autenticação, selecione **Bluemix Service**.
  3.	Selecione **Todos** para Tipo de dispositivo, ID do dispositivo, Evento e Formato.
  4.	Clique em **Pronto**.
  5.  Implemente o seu monitor clicando em **Implementar**.
4. Valide a conexão de dispositivo.
  1.	Abra o painel {{site.data.keyword.iot_short_notm}}.  
**Dica:** se o painel do {{site.data.keyword.iot_short_notm}} ainda não estiver aberto em outra guia, retorne para o seu painel do
{{site.data.keyword.Bluemix_notm}}, clique no nome de sua instância do {{site.data.keyword.iot_short_notm}} e, em seguida, clique em
**Ativar painel**.
  2. No menu principal, selecione **Dispositivos**.
  3. Clique no nome do dispositivo que você incluiu.   
As informações sobre o dispositivo exibem o status da conexão de seu dispositivo.
  4.	Em seu editor de fluxo do Node-RED, dê um clique duplo no nó **Enviar dados**, configure o valor de Repetição como
**Interval** e configure a frequência a cada `3` segundos.
  5. Clique em **Pronto**.
  6. Implemente as suas mudanças clicando em **Implementar**.  
A carga útil contém pontos de dados, como aqueles mostrados no exemplo a seguir:
```
{"d":{"temp":15,"umidade":50,"local":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Opcional: abra a guia Depurar para verificar se as mensagens estão sendo criadas.
    1. No menu que está localizado na seção de título, selecione **Visualizar**.
    2. Selecione **Mostrar barra lateral**.
    3. Clique na guia Depurar para ver as mensagens.
  8. Na página de Informações sobre o dispositivo do {{site.data.keyword.iot_short_notm}}, verifique se você vê pontos de dados do dispositivo na seção
Informações do sensor.


## Etapa 4: Criar cartões em {{site.data.keyword.iot_short_notm}} para mostrar dados ativos  
{: #createcards}  
Crie uma placa e cartões para exibir dados do dispositivo no painel do {{site.data.keyword.iot_short_notm}}. Para obter mais informações sobre as placas e
os cartões, veja [Visualizando dados em tempo real usando placas e cartões](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

1. Crie uma placa
  1. Abra o painel {{site.data.keyword.iot_short_notm}}.  
  **Dica:** se o painel do {{site.data.keyword.iot_short_notm}} ainda não estiver aberto em outra guia, retorne para o seu painel do
{{site.data.keyword.Bluemix_notm}}, clique no nome de sua instância do {{site.data.keyword.iot_short_notm}} e, em seguida, clique em **Ativar
painel**.  
  2. Crie uma placa para conter os cartões para os seus dispositivos simulados.
    1. Se a página Todas as placas ainda não estiver exibida, selecione **Placas** no menu
principal de painel do {{site.data.keyword.iot_short_notm}} e, em seguida, clique em
**Criar nova placa**.
    2. Insira um nome para a placa (por exemplo, `Home Environment`) e clique em **Avançar**.
    3. Na próxima página, clique em **Enviar**.  
  3. Clique na placa que você acabou de criar para abri-la.
2. Crie uma placa para exibir a temperatura
  1. Clique em **Incluir nova placa** e, em seguida, selecione o tipo de cartão **Gráfico de linha** por
meio da seção Dispositivos.
  2. Selecione o seu dispositivo na lista de dispositivos e, em seguida, clique em **Avançar**.
  3. Clique em **Conectar novo conjunto de dados**.
  4. Na página Criar cartão de valor, selecione ou insira os valores a seguir e clique em **Avançar**.
    - Evento: atualização
    - Propriedade: temp
    - Nome: Temperatura
    - Tipo: Valor flutuante
    - Unidade: °C
    - Precisão: 2
    - Mín: 0
    - Máx: 50
  5. Na página Visualização de cartão, selecione **L** para o tamanho de gráfico de linha e clique em **Avançar**.
  6. Na página Informações do cartão, mude o nome do cartão para **Temperatura** e clique em **Enviar**.   
O cartão de temperatura aparece no painel e inclui um gráfico de linha dos dados de temperatura em tempo real.
3. Crie um cartão para exibir a umidade
  1. Clique em **Incluir novo cartão** e, em seguida, selecione o tipo de cartão **Calibrador** por
meio da seção Dispositivos.
  2. Selecione o seu dispositivo na lista e, em seguida, clique em **Avançar**.
  3. Clique em **Conectar novo conjunto de dados**.
  4. Na página Criar cartão de valor, selecione ou insira os valores a seguir e clique em **Avançar**.Evento: atualização
     - Propriedade: umidade
     - Nome: Umidade
     - Tipo: Valor flutuante
     - Unidade: %
     - Precisão: 1
     - Mín: 10
     - Máx: 95
  5. Na página Visualização de cartão, selecione **M** para o tamanho de calibrador e clique em **Avançar**.
  6. Na página Informações do cartão, mude o nome do cartão para **Umidade** e clique em **Enviar**.   
O cartão de umidade aparece no painel e inclui um gráfico que mostra os dados de umidade em tempo real.  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## O que vem a seguir  
{: #whats-next}  
Agora que o seu dispositivo simulado está enviando dados para o {{site.data.keyword.iot_short_notm}}, é possível continuar a interagir em seu projeto de IoT.
 - Veja os seus cartões exibirem os dados que são gerados por seu fluxo do Node-RED.  
O Node-Red continua a enviar dados até você pará-lo. Para parar os dados simulados, execute as etapas a seguir:
    1.	Em seu editor de fluxo do Node-RED, dê um clique duplo no nó cinza **Enviar dados**, configure o valor de Repetição como
**Interval** e configure a frequência a cada **3** segundos.
    2. Clique em **Pronto**.
    3. Implemente as suas mudanças clicando em **Implementar**.

 - Conecte um dispositivo físico.  
[Procure o IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) para conectar um dispositivo físico como um Raspberry Pi
e envie os dados para o {{site.data.keyword.iot_short_notm}}.

 - Explore as opções de visualização.  
[Implemente um aplicativo node.js de amostra para visualizar os dados do
dispositivo.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html).

 -	Proteja por senha o editor de fluxo do Node-RED.   
Por padrão, o editor é aberto para que qualquer pessoa acesse e modifique os fluxos. Para proteger por senha o editor, execute as tarefas a seguir:
    1.	No painel do {{site.data.keyword.Bluemix_notm}}, clique no nome de seu aplicativo Starter para abrir as páginas do aplicativo.
    2. Clique em **Tempo de execução** para exibir a página Tempo de execução.
    3. Clique em **Variável de ambiente** para exibir a página Variáveis de ambiente.
    4. Na seção **Definido pelo usuário**, clique em **Incluir** e, em seguida, insira as variáveis definidas pelo
usuário a seguir:
         -	NODE_RED_USERNAME - o nome do usuário para proteger o editor
         -	NODE_RED_PASSWORD - a senha para proteger o editor
    3.	Clique em **Salvar**.
