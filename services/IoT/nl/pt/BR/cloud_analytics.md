---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Analytics
{: #cloud_analytics}

Usando análise de dados de nuvem do {{site.data.keyword.iot_short}}, você especifica as condições das regras que são baseadas em dados do dispositivo de tempo real e que acionam alertas e ações opcionais quando atendidas.    
{: shortdesc}

Por exemplo, você pode criar uma regra para assegurar que quando o dispositivo for descartado ou quando a temperatura do dispositivo aumentar, um alerta será enviado ao painel do dispositivo de um usuário e um e-mail será enviado ao administrador.

## Antes de iniciar
{: #byb}
Certifique-se de que as propriedades do dispositivo que você deseja usar como condições em suas regras tenham sido mapeadas para esquemas. Consulte [Conectando dispositivos](iotplatform_task.html) e [Criando esquemas](im_schemas.html) para obter mais informações.

Além disso, revise a orientação [Usando regras e ações com o {{site.data.keyword.iot_short}} Cloud
Analytics ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} para entender as regras e ações que são usadas no Cloud Analytics.

## Gerenciando regras e ações  
{: #managing_rules}

Use o painel **Regras** para criar e gerenciar regras e ações para sua organização.

Para obter uma visão geral de regras e alertas que foram acionados para seus dispositivos, use os painéis a seguir:

 |Nome do Painel | Descrição |  
 |:---|:---|  
  |Análise de dados central da regra | Mostra as regras para sua organização. Cartões adicionais listam alertas acionados, dispositivos associados, propriedades dos dispositivos e informações de alerta. |  
 |Análise de dados central do dispositivo | Mostra os dispositivos que estão conectados à sua organização. Cartões adicionais mostram alertas para um dispositivo selecionado, informações para um dispositivo selecionado, propriedades do dispositivo e informações de alerta. |

 Para obter mais informações sobre as placas de análise de dados padrão, consulte [Visualizando dados em tempo real usando placas e cartões](data_visualization.html#default_boards).


## Criando regras
{: #rules}

Regras são pontos de decisão baseados em condições que correspondem a dados do dispositivo de tempo real com valores de limites predefinidos ou outros dados de propriedade para acionar um alerta se uma condição for atendida. Além do alerta que é exibido no painel do {{site.data.keyword.iot_short}}, é possível incluir uma ou mais ações para executar a lógica de negócios quando uma regra for acionada.

**Importante:** antes que seja possível criar regras para um tipo de dispositivo, deve-se criar um esquema para o tipo de dispositivo. Para obter informações, consulte [Criar esquemas para o tipo de dispositivo](im_schemas.html).

Para criar uma regra:
1. No painel do {{site.data.keyword.iot_short}}, acesse **Regras**.
2. Clique em **Criar uma regra**, dê à regra um nome, forneça uma descrição, selecione um tipo de dispositivo ao qual a regra se aplica e, em seguida, clique em **Avançar**.  
3. Para configurar a lógica de regra, inclua uma ou mais condições IF para usar como acionadores da regra.  
É possível incluir condições em linhas paralelas para aplicá-las como condições OR ou incluir condições em colunas sequenciais para aplicá-las como condições AND.  
**Importante:** para acionar uma condição que compara duas propriedades ou para acionar duas ou mais condições de propriedade combinadas em sequência usando AND, os pontos de dados de acionamento devem ser incluídos na mesma mensagem do dispositivo. Se os dados forem recebidos em mais de uma mensagem, a condição ou condições sequenciais não serão acionadas.  
**Exemplos:**   
Uma regra simples poderá acionar um alerta se um valor de parâmetro for maior que um valor especificado:
Condição = `temp_cpu>80`  
Uma regra mais complexa pode ser acionada quando uma combinação de limites é atendida:
Condição = `temp_cpu>60 AND cpu_load>90`   

4. Configure os requisitos de acionador condicional para a sua regra.  
Para controlar o número de alertas que são acionadas para uma regra durante um período de tempo, é possível configurar os requisitos de acionador condicional para a sua regra.  
**Importante:** o acionamento condicional age em qualquer condição na regra. Por exemplo, se uma regra tiver cinco condições paralelas diferentes configuradas usando OR, cada condição verdadeira será incluída na contagem do acionador condicional.
Para configurar o acionamento condicional para uma regra:
 1. No editor de regras, clique no link **Acionar cada vez que as condições forem atendidas** padrão para abrir a caixa de diálogo para configurar requisitos de frequência.
 2. Selecione e configure o acionador condicional que você deseja usar na regra.
 <ul>
 <li>Acionar cada vez que as condições forem atendidas.</li>
 <li>Acionar se a condições forem atendidas N vezes em *Unidade de tempo* M</li>
 </ul>  
 Para obter uma descrição mais detalhada dos acionadores condicionais, consulte [Acionamento de regra condicional](#conditional "Visão geral de acionamento condicional").
5. Crie ou selecione uma ou mais ações que ocorrem se as condições da regra forem atendidas.  
Para obter mais informações sobre ações, consulte [Usando ações com suas regras](#shared "Criar ações").   
 Por exemplo: uma ação pode ser enviar um e-mail ou postar uma webhook.
3. **Opcional:** Selecione uma prioridade de alerta para a regra.  
 A prioridade é usada para classificar os alertas exibidos na placa **Análise de dados baseada em regra**. A prioridade padrão é Baixa.
6. Quando estiver satisfeito com sua regra, clique em **Salvar** para salvar sem ativar ou clique em **Ativar** para salvar e ativar a regra.

Sua regra está criada. Se você ativar a regra, quando as condições da regra forem atendidas, um alerta será incluído na placa **Placas > Análise de dados baseada em regra** e qualquer ação de regra será executada.

## Acionamento de regra condicional
{: #conditional}

Para controlar o número de alertas que são acionadas para uma regra durante um período de tempo, é possível configurar os requisitos de acionador condicional para a sua regra.

Dependendo da frequência da mensagem e das condições da regra, uma regra pode ser acionada um grande número de vezes após uma condição acionadora ser atendida. Por exemplo, se a condição for `temp >= 90` e a temperatura aumentar e se estabilizar em 91, a regra será acionada com cada mensagem recebida. Dependendo da frequência das mensagens do dispositivo e das ações que a regra está configurada para executar, esse volume de alertas pode encher rapidamente sua caixa de entrada de e-mail ou sobrecarregar um feed do Twitter com mensagens que não fornecem nenhum valor adicional.

**Importante:** o acionamento condicional age em qualquer condição na regra. Por exemplo, se uma regra tiver cinco condições paralelas diferentes configuradas usando OR, cada condição atendida será incluída na contagem do acionador condicional.

Condição | Descrição
------------- | -------------
Acionar cada vez que as condições forem atendidas. | A regra é acionada cada vez que as condições da regra são atendidas.
Acionar se condições forem atendidas *N* vezes em *M* *dias/horas/minutos/customizado* | A regra será acionada quando as condições forem atendidas *N* vezes no intervalo de tempo selecionado e não será acionada novamente até que o período configurado tenha passado. </br>Exemplo: requisito de acionador condicional =`Acionar somente uma vez se as condições forem atendidas 4 vezes em 30 minutos`. O dispositivo envia uma nova mensagem a cada cinco minutos. Ao meio-dia, a temperatura excede inicialmente 90 graus, que atende à condição. O contador do acionador condicional é iniciado, mas a regra ainda não foi acionada.  Após 15 minutos e mais três mensagens que indicam `temp > 90` serem recebidas, a regra será acionada. A regra não será então acionada por mais 15 minutos, independentemente da temperatura.
Acionar apenas na primeira vez que as condições forem atendidas e reconfigurar quando as condições não estiverem mais atendidas. | A regra será acionada quando as condições forem atendidas, mas não será então acionada para mensagens consecutivas que também atendem as condições. Os critérios de acionamento serão reconfigurados pela primeira mensagem que não atender as condições da regra.
Acionar se persistirem condições para *M* *days/hours/minutes/custom*. | A regra é acionada após o intervalo de tempo selecionado, se todos os pontos de dados que são recebidos durante o intervalo de tempo atenderem às condições ou se nenhum ponto de dados adicional é recebido. O intervalo de tempo inicia quando as condições são atendidas inicialmente.



## Usando ações em suas regras
{: #shared}

Além de exibir alertas no painel de alertas, o {{site.data.keyword.iot_short}} suporta vários tipos de ações de acionadas por regras, como enviar e-mails e postar webhooks.

É possível criar ações diretamente no editor de regras ou na guia Ações e, em seguida, selecioná-las ao criar suas regras.

Para criar uma ação na guia Ações:
1. No painel do {{site.data.keyword.iot_short}}, acesse **Regras**.
2. No painel Regras, selecione a guia **Ações**.
2. Clique em **Criar uma ação**, forneça à ação um nome e uma descrição e selecione um tipo de ação, em seguida, clique em **Avançar**.
3. Forneça os parâmetros necessários para o tipo de ação que você está criando.  
Tipos de ação:  
 - [Enviar e-mail](#email "Enviar e-mail")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Clique em **OK** para criar a nova ação.

A ação agora está disponível no editor de regras.

**Nota:** todos os exemplos a seguir representam uma ação que notifica um engenheiro de serviço quando a temperatura, que é representada pela propriedade `temp_cpu` de um dispositivo, excede 80 graus, usando a condição da regra a seguir: `temp_cpu >= 80`

### Enviar E-mail  
{: #email}
Use a ação enviar e-mail para enviar um e-mail para um ou mais destinatários quando uma regra for acionada.

Exemplo: [enviar e-mail](#emailex).

Os parâmetros a seguir são usados para configurar a ação enviar e-mail:

Parâmetro | Descrição
---|---
Name | O nome da ação, que é usado no Painel de alertas.
Descrição | Uma breve descrição da ação.
Assunto | A linha de assunto do e-mail. A linha de assunto padrão é "Alerta do IBM Watson IoT: ação de e-mail".
Para | Selecione enviar o alerta apenas para você mesmo ou para uma lista separada por vírgula de endereços de e-mail. Se selecionar enviar para si mesmo, o e-mail será enviado para o endereço de e-mail do {{site.data.keyword.iot_short}} com o qual você efetuou login.
Cc | Nenhum ou uma lista separada por vírgula de endereços de e-mail.
O corpo do e-mail é criado automaticamente a partir da mensagem do dispositivo no momento em que a regra foi acionada.  
**Importante:** por padrão, e-mails não incluem dados do dispositivo que possam incluir informações confidenciais. Mude a configuração **Incluir dados** para incluir dados do dispositivo.

#### Exemplo: usar enviar e-mail
{: #emailex}

Neste exemplo, a ação está configurada para usar o recurso de envio de e-mail para enviar um e-mail ao engenheiro de serviço principal e também enviar um e-mail de backup para seu gerente.

Para criar uma ação de e-mail:
1. No painel do {{site.data.keyword.iot_short}}, acesse **Regras**.
2. Clique em **Criar uma ação**.
4. Insira o nome da ação `Enviar e-mail de solicitação de serviço`.
5. Insira a descrição `Enviar um e-mail para o engenheiro de serviço e seu gerente`.
3. Selecione o tipo **E-mail**.
6. No campo Para, selecione **Pessoas específicas** e insira `service.engineer@company.com`.
7. No campo CC (cópia carbono), selecione **Pessoas específicas** e insira `service.manager@company.com`.
8. Na linha de assunto, insira: `Serviço necessário`.
10. Selecione **Incluir dados** para incluir os dados do dispositivo no e-mail.
11. Clique em **Concluir** para salvar a ação.  


### IFTTT  
{: #ifttt}

Use a ação IFTTT para acionar uma receita do IFTTT quando uma regra for acionada. Para obter mais informações sobre o acionamento de ações como orientações de IFTTT, consulte [Canal do criador ![Ícone de link
externo](../../icons/launch-glyph.svg)](https://ifttt.com/maker){: new_window} no site do IFTTT.

Exemplo: [usar o IFTTT para postar um cartão do Trello](#iftttex).

Os parâmetros a seguir são usados para configurar uma ação do IFTTT:

Parâmetro | Descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
Descrição | Uma breve descrição da ação.
Chave | A chave do Canal Maker a ser usada para acionar o evento.
Event | O nome do evento que você configurou como um acionador para o Evento Maker. É possível criar várias receitas com diferentes acionadores, cada uma com um nome de evento diferente.
Valor de 1 a 3 | É possível passar qualquer conteúdo nesses parâmetros que são passados para a ação em sua receita do IFTTT. **Dica:** é possível usar a [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente no cabeçalho.

#### Exemplo: usar o IFTTT para postar um cartão do Trello {: #iftttex}

Neste exemplo, a ação está configurada para usar o IFTTT para postar um cartão em uma lista de solicitações de serviço no Trello.

Para criar a ação postar um cartão no Trello:
1.	Em IFTTT, conecte-se ao canal Trello.
2.	Em IFTTT, conecte-se ao canal Maker. Anota sua chave do IFTTT. Você precisa dessa chave para se conectar ao IFTTT a partir do {{site.data.keyword.iot_short_notm}}.
5.	Em IFTTT, crie uma receita:
 1. Clique em **ESTE**.
 2. Selecione o canal **Maker**.  
 2. Clique em **Receber uma solicitação da web**.
 3. Insira o nome do evento `post-Trello-card`.
 4. Clique em **ESSE**.
 5. Selecione o canal **Trello**.
 6. Selecione a placa do Trello na qual criar o cartão.
 7. Insira um nome da lista no qual incluir os cartões.
 8. Edite o título e a descrição.
 9. Designe os membros @service.engineer e @service.manager.
 8. Clique em **Criar ação**.   
3. No painel do {{site.data.keyword.iot_short}}, acesse **Regras > Ações** e crie uma nova ação que tenha os parâmetros a seguir:
<ul>
<li>Tipo - **IFTTT**</li>
<li>Nome - `Postar cartão de solicitação de serviço`</li>
<li>Descrição - `Use o IFTTT para postar um cartão na lista de solicitações de serviço no Trello.`</li>
<li>Chave - Sua chave do IFTTT</li>
<li>Evento - `post-Trello-card`</li>
<li>Opcionalmente, inclua valores para Valor 1 a 3. **Dica:** é possível usar [substituição de variável](#variable_substitution) para incluir dinamicamente dados do dispositivo.</li>
</ul>
4. Clique em **OK** para salvar a ação.


### Node-RED
{: #nodered}

Use a ação do Node-RED para se conectar a um aplicativo Node-RED quando uma regra for acionada. Para obter mais informações sobre como usar o Node-RED, veja [Criando apps com o aplicativo Internet of Things Starter](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Exemplo: [usar o Node-RED para enviar uma mensagem de texto](#noderedex).

Os parâmetros a seguir são usados para configurar uma ação do Node-RED:

Parâmetro | Descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
Descrição | Uma breve descrição da ação.
URL | A URL do nó de entrada HTTP Node-RED de destino.
User name | Inclua se requerido pelo serviço Node-RED.
Password | Inclua se requerido pelo serviço Node-RED. **Importante:** a senha é enviada em texto não criptografado.
Corpo | Por padrão, o campo de corpo é preenchido previamente com todas as variáveis listadas em [substituição de variável](#variable_substitution).

#### Exemplo: usar o Node-RED para enviar uma mensagem de texto
{: #noderedex}

Neste exemplo, a ação é configurada para usar o Node-RED com um nó Twilio para enviar uma mensagem de texto ao engenheiro de serviço.

Para criar a ação enviar mensagem de texto:
1. No Twilio, localize ou crie um novo Serviço de sistema de mensagens a ser usado para enviar mensagens de texto a partir de sua conta do Twilio. Para obter informações, consulte a [documentação do Twilio ![Ícone de link externo](../../icons/launch-glyph.svg)](https://www.twilio.com/help){: new_window}.
2. No Bluemix, configure e acesse sua conta do Node-RED com a URL do Node-RED `http://mynodered.mybluemix.net/red/`. Para obter mais informações, veja o tópico [Criando apps com o Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) na documentação do Bluemix.
3. No Node-RED, crie um fluxo simples com dois nós, como [RTI-alert]->[SMS].  
Em que o primeiro nó é um nó http e o segundo é um nó twilio.
 1. Inclua o nó de entrada "http" e configure-o com os atributos a seguir:
  <ul>
  <li>Método - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Nome - Ação de RTI</li>
  </ul>
  2. Inclua um nó de saída "http response" e conecte ele e os nós de entrada "http" juntos arrastando-os entre a porta de saída de um até a porta de entrada do outro.
  3. Inclua um nó de saída "twilio" e configure-o com os atributos a seguir:
  <ul>
  <li>Serviço - **Serviço externo**</li>
  <li>Twilio - Incluir novo twilio-api</li>
  <li>SMS para - `Número do telefone para o engenheiro de serviço`</li>
  <li>Nome - **SMS**</li>
  </ul>
  4. Conecte os nós juntos  
  Conecte os nós http e twilio juntos arrastando entre a porta de saída de um para a porta de entrada do outro.
  5. Clique no botão **Implementar** para implementar o fluxo no servidor
4. No painel do {{site.data.keyword.iot_short}}, acesse **Regras > Ações** e crie uma nova ação que tenha os parâmetros a seguir:
 - Tipo - **Node-RED**
 - Nome - `Enviar texto usando Node-RED e Twilio`
 - Descrição - `Enviar um alerta de mensagem de texto para o engenheiro de serviço.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. Clique em **Concluir** para salvar a ação.



### Webhook
{: #webhook}

Use a ação do webhook para fazer uma solicitação de HTTP para um serviço da web ativado para o webhook quando um alerta for acionado. Por exemplo, um webhook poderá ser usado para abrir uma solicitação de serviço para um ativo se um sensor no dispositivo relatar uma leitura anormal.

Exemplo: [usar um webhook para postar no Slack](#webhookex).

Os parâmetros a seguir são usados para configurar uma ação do webhook:

Parâmetro | Descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
Descrição | Uma breve descrição da ação.
URL | A URL do servidor de destino ativado para o webhook. **Dica:** é possível usar a [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente na URL.
Método | O tipo de chamada do webhook a executar. Selecione um dos tipos a seguir: GET, HEAD, OPTIONS, PATCH, PUT, POST ou DELETE.
User name | Inclua se necessário pelo serviço da web.
Password | Inclua se necessário pelo serviço da web. **Importante:** a senha é enviada em texto não criptografado.
Header | Os cabeçalhos são compostos de pares de chave e valor. **Dica:** é possível usar a [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente no cabeçalho.
Tipo de Conteúdo | O tipo de conteúdo do corpo: JSON, XML, URL codificada de formulário WWW ou texto simples.  Disponível para os métodos OPTIONS, PATCH, PUT, POST e DELETE.
Corpo | O corpo da chamada do webhook.  Disponível para os métodos OPTIONS, PATCH, PUT, POST e DELETE. Por padrão, o campo de corpo é preenchido previamente com todas as variáveis listadas em [substituição de variável](#variable_substitution). **Importante:** O servidor webhook pode requerer que determinados campos específico sejam incluídos no corpo. Por exemplo, um webhook do Slack deve conter o campo "text".   

#### Exemplo: usar um webhook para postar no Slack
{: #webhookex}

Neste exemplo, a ação está configurada para usar um webhook para postar uma mensagem no canal #service-requests do Slack.

Para criar a ação postar no Slack:
1. No Slack, configure a integração do Incoming Webhooks para o canal #service-requests. Anote a URL dos webhooks. Para obter informações, consulte a [documentação do Slack![Ícone de link externo](../../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window}.
2. No painel do {{site.data.keyword.iot_short}}, acesse **Regras > Ações** e crie uma nova ação que tenha os parâmetros a seguir:
 - Nome - `Postar solicitação de serviço no Slack`
 - Tipo - **Webhook**
 - URL - `Sua URL dos webhooks do Slack`
 - Método - **POST**
 - Tipo de conteúdo - `application/json`
 - Corpo   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **Importante:** O webhook do Slack deve conter, no mínimo, o campo "text". Para obter informações, consulte os [Webhooks de entrada ![Ícone de link externo](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window} na documentação do Slack.
11. Clique em **Concluir** para salvar a ação.


### Substituição de variáveis  
{: #variable_substitution}

Inclua as substituições de variáveis a seguir para incluir dados do dispositivo dinamicamente. A variável deve ser cercada por chaves duplas.

Variável | Descrição
---|---
**URL, cabeçalho e corpo** |
`{{timestamp}}` | O registro de data e hora da mensagem.
`{{orgId}}` | O ID da organização do serviço do {{site.data.keyword.iot_short_notm}}.
`{{tenantId}}` | Descontinuado: o ID do serviço do {{site.data.keyword.iotrtinsights_full}}.
`{{deviceId}}` | O ID do dispositivo.
`{{ruleName}}` | O nome da regra que inclui a ação.
`{{ruleID}}` | O ID da regra que inclui a ação.
**Somente o corpo** |
`{{ruleDescription}}`| A descrição da regra que inclui a ação.
`{{ruleCondition}}` | A condição da regra que acionou a ação.
`{{message}}` | A mensagem do dispositivo bruto que incluiu o valor de ponto de dados que acionou a regra.

## Orientações sobre o Cloud Analytics

As orientações a seguir descrevem como usar os recursos do Cloud Analytics para casos de uso diferentes:

- [Análise de dados em tempo real usando o IBM Watson™ IoT Platform Analytics ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Análise preditiva nos dados de amostra da IoT ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [O cartão de lista de dispositivos SIMPLIFICA o monitoramento do dispositivo em tempo real no painel WIoTP
![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Executar ações no IBM Watson IoT Platform Cloud Analytics ![Ícone de link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use o IBM Data Science Experience para detectar anomalias de séries temporais ![Ícone de
link externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
