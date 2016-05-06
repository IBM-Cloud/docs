---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Exemplos de ação

Os tipos de ação Enviar e-mail, IFTTT, Node-RED e webhooks abrem um amplo universo de opções para executar tarefas, que é limitado somente por sua imaginação e os conectores que são usados pelas outras ferramentas. Por
exemplo, ações para postar mensagens de status do dispositivo no
Slack, enviar mensagens de texto para a equipe de serviços, criar solicitações de serviço do dispositivo e muito mais.
{: shortdesc}

Os exemplos abaixo representam uma ação que notifica um engenheiro de serviço quando a temperatura, que é representada pelo ponto de dados temporários de um dispositivo, excede 100 graus usando a condição da regra a seguir:
`temp >= 100`

É possível acionar um ou mais dos tipos de ação a seguir quando a condição da regra ocorre:  
 - [Enviar e-mail](#emailex "Enviar e-mail")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Usar Enviar e-mail {: #emailex}
Neste exemplo, a ação é configurada para usar o recurso Enviar e-mail do Real-Time Insights para enviar um e-mail para o engenheiro de serviço principal e também enviar um e-mail de backup para seu gerente.

Para criar uma ação de e-mail:
1. No Real-Time Insights, acesse **Análise > Ações**.
2. Clique em **Incluir nova ação**.
3. Selecione o tipo **Enviar e-mail**.
4. Insira o nome da ação `Enviar e-mail de solicitação de serviço`.
5. Insira a descrição `Enviar um e-mail para o engenheiro de serviço e seu gerente`.
6. No campo Para, insira `service.engineer@company.com`.
7. No campo CC, insira: `service.manager@company.com`.
8. Na linha de assunto, insira: `Serviço necessário`.
9. Selecione para pré-anexar com "Alerta do {{site.data.keyword.iotrtinsights_short}}" para esclarecer de onde o e-mail é proveniente.
10. Para incluir os dados do dispositivo no e-mail, limpe a caixa de seleção **Não incluir dados do dispositivo na mensagem de e-mail**.
11. Clique em **OK** para salvar a ação.  




## Usar um webhook para postar no Slack {: #webhookex}

Neste exemplo, a ação é configurada para usar um webhook para postar uma mensagem em nosso canal do Slack #service-requests.

Para criar a ação postar no Slack:
1. No Slack, configure a integração do Incoming Webhooks para o canal #service-requests. Anote a URL dos webhooks. Para obter mais informações, veja a [documentação do Slack](https://api.slack.com/incoming-webhooks).
2. No Real-Time Insights, acesse **Análise > Ações** e crie uma nova ação que tenha os parâmetros a seguir:
 - Tipo - **Webhook**
 - Nome - `Postar solicitação de serviço no Slack`
 - URL - `Sua URL dos webhooks do Slack`
 - Método - **POST**
 - Tipo de conteúdo - application/json
 - Selecione **Usar corpo da mensagem customizado**
 - Corpo  
 ```{"text":"*Um dispositivo precisa de sua atenção*\n Horário: {{timestamp}}\n Instância do {{site.data.keyword.iotrtinsights_short}}: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regra: {{ruleName}}\n Descrição: {{ruleDescription}}\n Condição: {{ruleCondition}}\n Mensagem do dispositivo bruto: \n{{message}}"}```
 {: codeblock}  
 **Importante:** O webhook do Slack deve conter, no mínimo, o campo "text". Para obter informações, veja [Incoming Webhooks](https://api.slack.com/incoming-webhooks "Documentação do Slack") na documentação do Slack.
11. Clique em **OK** para salvar a ação.

## Usar o Node-RED para enviar uma mensagem de texto {: #noderedex}

Neste exemplo, a ação é configurada para usar o Node-RED com um nó Twilio para enviar uma mensagem de texto ao engenheiro de serviço.

Para criar a ação enviar mensagem de texto:
1. No Twilio, localize ou crie um novo Serviço de sistema de mensagens a ser usado para enviar mensagens de texto a partir de sua conta do Twilio. Para obter informações, veja a [documentação do Twilio](https://www.twilio.com/help).
1. No Bluemix, configure e acesse sua conta do Node-RED com a URL do Node-RED `http://mynodered.mybluemix.net/red/`. Para obter mais informações, veja o tópico [Criando apps com o Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) na documentação do Bluemix.
2. No Node-RED, crie um fluxo simples de dois nós, como [RTI-alert]->[SMS].
Em que o primeiro nó é um nó http e o segundo é um nó twilio.
 1. Inclua o nó de entrada "http" e configure-o com os atributos a seguir:
  <ul>
  <li>Método - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Nome - Ação de RTI</li>
  </ul>
  2. Inclua um nó de saída "resposta http" e conecte-o e os nós de entrada "http" juntos arrastando entre a porta de saída de um para a porta de entrada do outro.
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
3. No {{site.data.keyword.iotrtinsights_short}}, acesse **Análise > Ações** e crie uma ação que tenha os parâmetros a seguir:
 - Tipo - **Node-RED**
 - Nome - `Enviar texto usando Node-RED e Twilio`
 - Descrição - `Enviar um alerta de mensagem de texto para o engenheiro de serviço.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```{"text":"*Um dispositivo precisa de sua atenção*\n Horário: {{timestamp}}\n Instância do {{site.data.keyword.iotrtinsights_short}}: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regra: {{ruleName}}\n Descrição: {{ruleDescription}}\n Condição: {{ruleCondition}}\n Mensagem do dispositivo bruto: \n{{message}}"}```
 {: codeblock}
4. Clique em **OK** para salvar a ação.

## Usar o IFTTT para postar um cartão do Trello {: #iftttex}

Neste exemplo, configuramos a ação para usar o IFTTT para postar um cartão em uma lista de solicitações de serviço no Trello.

Para criar a ação postar um cartão no Trello:
1.	Em IFTTT, conecte-se ao canal Trello.
2.	Em IFTTT, conecte-se ao canal Maker. Anota sua chave do IFTTT. Ela será necessária para conectar-se ao IFTTT a partir do Real-Time Insights.
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
3. No {{site.data.keyword.iotrtinsights_short}}, acesse **Análise > Ações** e crie uma ação que tenha os parâmetros a seguir:
<ul>
<li>Tipo - **IFTTT**</li>
<li>Nome - `Postar cartão de solicitação de serviço`</li>
<li>Descrição - `Use o IFTTT para postar um cartão na lista de solicitações de serviço no Trello.`</li>
<li>Chave - Sua chave do IFTTT</li>
<li>Evento - `post-Trello-card`</li>
<li>Opcionalmente, inclua valores para o Valor de 1 a 3. **Dica:** é possível usar a [substituição de variável](actions.html#variable_substitution) para incluir dados do dispositivo dinamicamente.</li>
</ul>
4. Clique em **OK** para salvar a ação.
